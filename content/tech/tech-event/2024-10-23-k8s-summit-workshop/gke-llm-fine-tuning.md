# GKE LLM Fine-Tuning | K8s Summit 2024 GCP Workshop

## Preparation

* [Fine-tune Open Source LLMs on GKE | CE093](https://explore.qwiklabs.com/classrooms/16036/labs/95048)
  * [ai-on-gke > finetuning-llama-7b-on-l4](https://github.com/GoogleCloudPlatform/ai-on-gke/tree/main/tutorials-and-examples/genAI-LLM/finetuning-llama-7b-on-l4)
  * [dell-research-harvard/AmericanStories dataset](https://huggingface.co/datasets/dell-research-harvard/AmericanStories)
* Learning Objectives
  * Prepare your environment with a GKE cluster in standard mode.
  * Set up an autoscaling L4 GPU nodepool.
  * Run a Kubernetes Job to download Llama 2 7b and fine-tune using L4 GPUs
  * Make use of GCS for efficient storage of models.

```sh
student_03_216a983cfb25@cloudshell:~ (qwiklabs-asl-02-cd54d6e804de)$ 

gcloud auth list
# Credentialed Accounts

# ACTIVE: *
# ACCOUNT: student-03-216a983cfb25@qwiklabs.net

gcloud config list project
# [core]
# project = qwiklabs-asl-02-cd54d6e804de

# Your active configuration is: [cloudshell-23006]
```

### Step 1: Create the GKE Cluster

```sh
export CLUSTER_NAME="ml-gke"
export REGION="us-central1"
export BUCKET_NAME=${GOOGLE_CLOUD_PROJECT}-llama-l4
export SERVICE_ACCOUNT="l4-lab@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com"

gcloud container clusters create $CLUSTER_NAME \
  --enable-image-streaming \
  --addons=HttpLoadBalancing \
  --machine-type=e2-standard-2 \
  --shielded-secure-boot \
  --shielded-integrity-monitoring \
  --region=${REGION} \
  --num-nodes=1 \
  --enable-ip-alias \
  --release-channel=rapid \
  --node-locations=${REGION}-a \
  --workload-pool=${GOOGLE_CLOUD_PROJECT}.svc.id.goog \
  --addons GcsFuseCsiDriver

# Note: The Kubelet readonly port (10255) is now deprecated. Please update your workloads to use the recommended alternatives. See https://cloud.google.com/kubernetes-engine/docs/how-to/disable-kubelet-readonly-port for ways to check usage and for migration instructions.
# Creating cluster ml-gke in us-central1... Cluster is being health-checked (Kubernetes Control Plane is healthy)...done.                           
# Created [https://container.googleapis.com/v1/projects/qwiklabs-asl-02-cd54d6e804de/zones/us-central1/clusters/ml-gke].
# To inspect the contents of your cluster, go to: https://console.cloud.google.com/kubernetes/workload_/gcloud/us-central1/ml-gke?project=qwiklabs-asl-02-cd54d6e804de
```

### Step 2: Validate Cluster Readiness

```sh
gcloud container clusters list

NAME: ml-gke
LOCATION: us-central1
MASTER_VERSION: 1.31.1-gke.1146000
MASTER_IP: 34.67.21.231
MACHINE_TYPE: e2-standard-2
NODE_VERSION: 1.31.1-gke.1146000
NUM_NODES: 1
STATUS: RUNNING
```

## Get access to the model

### Sign the license consent agreement

* Request access to Meta Llama models by submitting the request access form at <https://ai.meta.com/resources/models-and-libraries/llama-downloads/>
* Accept the model terms.
* Login to Hugging Faces and find the llama2-7b-chat-hf model. <https://huggingface.co/meta-llama/Llama-2-7b-chat-hf>
* Request agree to the terms and conditions.
  * LLAMA 2 COMMUNITY LICENSE AGREEMENT

### Generate an access token

* Click Your Profile > Settings > Access Tokens.
* Select New Token.
* Specify a Name of your choice and a Role of at least Read.
* Select Generate a token.
* Copy the generated token to your clipboard.

```txt
2024-10-23-k8s-summit-gcp-1
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
```

## Prepare your environment

```sh
# Set the default environment variables:
export HF_TOKEN=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

# Create the Node Pool
gcloud container node-pools create gpupool --cluster ml-gke \
  --accelerator type=nvidia-l4,count=8,gpu-driver-version=latest \
  --machine-type g2-standard-96 \
  --ephemeral-storage-local-ssd=count=8 \
  --enable-autoscaling --enable-image-streaming \
  --num-nodes=0 --min-nodes=0 --max-nodes=3 \
  --shielded-secure-boot \
  --shielded-integrity-monitoring \
  --node-locations ${REGION}-a,${REGION}-b --region ${REGION} 

# Note: Machines with GPUs have certain limitations which may affect your workflow. Learn more at https://cloud.google.com/kubernetes-engine/docs/how-to/gpus
# Note: Starting in GKE 1.30.1-gke.115600, if you don't specify a driver version, GKE installs the default GPU driver for your node's GKE version.
# Creating node pool gpupool...done.                                                                                                                
# Created [https://container.googleapis.com/v1/projects/qwiklabs-asl-02-cd54d6e804de/zones/us-central1/clusters/ml-gke/nodePools/gpupool].

# NAME: gpupool
# MACHINE_TYPE: g2-standard-96
# DISK_SIZE_GB: 100
# NODE_VERSION: 1.31.1-gke.1146000

# Create a Kubernetes Secret that contains the Hugging Face token
kubectl create secret generic hf-secret \
  --from-literal=hf_api_token=${HF_TOKEN} \
  --dry-run=client -o yaml | kubectl apply -f -
# secret/hf-secret created
```

## Run a Kubernetes Job to Finetune Llama 2 7b

Finetuning requires a base model and a dataset. For this post, the `dell-research-harvard/AmericanStories` dataset will be used to fine-tune the Llama 2 7b base model. GCS will be used for storing the base model. GKE with GCSFuse is used to transparently save the fine-tuned model to GCS. This provides a cost efficient way to store and serve the model and only pay for the storage used by the model.

```sh
# Configuring GCS and required permissions
gcloud storage buckets create gs://${BUCKET_NAME}
# Creating gs://qwiklabs-asl-00-98aeeab1318c-llama-l4/...

gcloud iam service-accounts create l4-lab
# Created service account [l4-lab].

gcloud storage buckets add-iam-policy-binding gs://${BUCKET_NAME} \
  --member="serviceAccount:${SERVICE_ACCOUNT}" --role=roles/storage.admin

gcloud iam service-accounts add-iam-policy-binding ${SERVICE_ACCOUNT} \
  --role roles/iam.workloadIdentityUser \
  --member "serviceAccount:${GOOGLE_CLOUD_PROJECT}.svc.id.goog[default/l4-lab]"

kubectl create serviceaccount l4-lab
# serviceaccount/l4-lab created
kubectl annotate serviceaccount l4-lab iam.gke.io/gcp-service-account=l4-lab@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com
# serviceaccount/l4-lab annotated
```

* `add-iam-policy-binding` response

```yaml
bindings:
- members:
  - serviceAccount:l4-lab@qwiklabs-asl-02-cd54d6e804de.iam.gserviceaccount.com
  role: roles/storage.admin
- members:
  - projectEditor:qwiklabs-asl-02-cd54d6e804de
  - projectOwner:qwiklabs-asl-02-cd54d6e804de
  role: roles/storage.legacyBucketOwner
- members:
  - projectViewer:qwiklabs-asl-02-cd54d6e804de
  role: roles/storage.legacyBucketReader
etag: CAI=
kind: storage#policy
resourceId: projects/_/buckets/qwiklabs-asl-02-cd54d6e804de-llama-l4
version: 1
Updated IAM policy for serviceAccount [l4-lab@qwiklabs-asl-02-cd54d6e804de.iam.gserviceaccount.com].
bindings:
- members:
  - serviceAccount:qwiklabs-asl-02-cd54d6e804de.svc.id.goog[default/l4-lab]
  role: roles/iam.workloadIdentityUser
etag: BwYlLkTsN4g=
version: 1
```

### create `download-model.yaml`

Let's use Kubernetes Job to download the Llama 2 7b model from HuggingFace. The file `download-model.yaml` shows how to do this:

* Note: envsubst is used to replace ${BUCKET_NAME} inside the above yaml with your own bucket.

```yml
cat - <<'EOF' | envsubst | kubectl apply -f -
apiVersion: batch/v1
kind: Job
metadata:
  name: model-loader
  namespace: default
spec:
  template:
    metadata:
      annotations:
        kubectl.kubernetes.io/default-container: loader
        gke-gcsfuse/volumes: "true"
        gke-gcsfuse/memory-limit: 400Mi
        gke-gcsfuse/ephemeral-storage-limit: 30Gi
    spec:
      restartPolicy: OnFailure
      containers:
      - name: loader
        image: python:3.11
        command:
        - /bin/bash
        - -c
        - |
          pip install huggingface_hub
          mkdir -p /gcs-mount/llama2-7b
          python3 - << EOF
          from huggingface_hub import snapshot_download
          model_id="meta-llama/Llama-2-7b-hf"
          snapshot_download(repo_id=model_id, local_dir="/gcs-mount/llama2-7b",
                            local_dir_use_symlinks=False, revision="main",
                            ignore_patterns=["*.safetensors", "model.safetensors.index.json"])
          EOF
        imagePullPolicy: IfNotPresent
        env:
        - name: HUGGING_FACE_HUB_TOKEN
          valueFrom:
            secretKeyRef:
              name: hf-secret
              key: hf_api_token
        volumeMounts:
        - name: gcs-fuse-csi-ephemeral
          mountPath: /gcs-mount
      serviceAccountName: l4-lab
      volumes:
      - name: gcs-fuse-csi-ephemeral
        csi:
          driver: gcsfuse.csi.storage.gke.io
          volumeAttributes:
            bucketName: ${BUCKET_NAME}
            mountOptions: "implicit-dirs"
EOF
```

```sh
# job.batch/model-loader created

# Give it a minute to start running, once up you can watch the logs of the job by running:
kubectl logs -f -l job-name=model-loader
# This will take about 10 minutes.

# 實作 Note: 
# 1. HF_TOKEN 塞錯了orz
# 2. 要先收到 Hugging Face 的 Mail "[Access granted]"

#     response = _request_wrapper(
#                ^^^^^^^^^^^^^^^^^
#   File "/usr/local/lib/python3.11/site-packages/huggingface_hub/file_download.py", line 301, in _request_wrapper
#     hf_raise_for_status(response)
#   File "/usr/local/lib/python3.11/site-packages/huggingface_hub/utils/_http.py", line 423, in hf_raise_for_status
#     raise _format(GatedRepoError, message, response) from e
# huggingface_hub.errors.GatedRepoError: 401 Client Error. (Request ID: Root=1-67188f36-4a9954144b4971066a504e2d;8e2afa5e-7ef5-4ff6-97fe-768d19a4d40a)

# Cannot access gated repo for url https://huggingface.co/meta-llama/Llama-2-7b-hf/resolve/01c7f73d771dfac7d292323805ebc428287df4f9/.gitattributes.
# Access to model meta-llama/Llama-2-7b-hf is restricted. You must have access to it and be authenticated to access it. Please log in.

# Installing collected packages: urllib3, typing-extensions, tqdm, pyyaml, packaging, idna, fsspec, filelock, charset-normalizer, certifi, requests, huggingface_hub
# Successfully installed certifi-2024.8.30 charset-normalizer-3.4.0 filelock-3.16.1 fsspec-2024.10.0 huggingface_hub-0.26.1 idna-3.10 packaging-24.1 pyyaml-6.0.2 requests-2.32.3 tqdm-4.66.5 typing-extensions-4.12.2 urllib3-2.2.3
# WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

# [notice] A new release of pip is available: 24.0 -> 24.2
# [notice] To update, run: pip install --upgrade pip
# /usr/local/lib/python3.11/site-packages/huggingface_hub/file_download.py:834: UserWarning: `local_dir_use_symlinks` parameter is deprecated and will be ignored. The process to download files to a local folder has been updated and do not rely on symlinks anymore. You only need to pass a destination folder as`local_dir`.
# For more details, check out https://huggingface.co/docs/huggingface_hub/main/en/guides/download#download-files-to-local-folder.
#   warnings.warn(
# Fetching 14 files: 100%|██████████| 14/14 [04:03<00:00, 17.38s/it]
# 看到這個 100% 就是完成了

# 若要砍掉先前的 batch job, 使用: 
# kubectl get all
# kubectl delete jobs model-loader
# kubectl get all

# Once the job has finished you can verify the model has been downloaded by running:
gcloud storage ls -l gs://$BUCKET_NAME/llama2-7b/

# gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/:
#          0  2024-10-24T00:43:01Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/
#       1581  2024-10-24T00:43:10Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/.gitattributes
#       7020  2024-10-24T00:43:08Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/LICENSE.txt
#      22295  2024-10-24T00:43:08Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/README.md
#    1253223  2024-10-24T00:43:09Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/Responsible-Use-Guide.pdf
#       4766  2024-10-24T00:43:07Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/USE_POLICY.md
#        609  2024-10-24T00:43:09Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/config.json
#        188  2024-10-24T00:43:11Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/generation_config.json
# 9976634558  2024-10-24T00:47:05Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/pytorch_model-00001-of-00002.bin
# 3500315539  2024-10-24T00:45:00Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/pytorch_model-00002-of-00002.bin
#      26788  2024-10-24T00:43:13Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/pytorch_model.bin.index.json
#        414  2024-10-24T00:43:14Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/special_tokens_map.json
#    1842767  2024-10-24T00:43:14Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/tokenizer.json
#     499723  2024-10-24T00:43:15Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/tokenizer.model
#        776  2024-10-24T00:43:14Z  gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/tokenizer_config.json
#                                   gs://qwiklabs-asl-02-cd54d6e804de-llama-l4/llama2-7b/.cache/
# TOTAL: 16 objects, 13480610247 bytes (12.55GiB)
```

Let's write our finetuning job code by using the HuggingFace library for training.

### `fine-tune.py`

```python
from pathlib import Path
from datasets import load_dataset, concatenate_datasets
from transformers import AutoTokenizer, AutoModelForCausalLM, Trainer, TrainingArguments, DataCollatorForLanguageModeling
from peft import get_peft_model, LoraConfig, prepare_model_for_kbit_training
import torch

# /gcs-mount will mount the GCS bucket created earlier
model_path = "/gcs-mount/llama2-7b"
finetuned_model_path = "/gcs-mount/llama2-7b-american-stories"

tokenizer = AutoTokenizer.from_pretrained(model_path, local_files_only=True)
model = AutoModelForCausalLM.from_pretrained(
            model_path, torch_dtype=torch.float16, device_map="auto", trust_remote_code=True)

dataset = load_dataset("dell-research-harvard/AmericanStories",
    "subset_years",
    year_list=["1809", "1810", "1811", "1812", "1813", "1814", "1815"]
)
dataset = concatenate_datasets(dataset.values())

if tokenizer.pad_token is None:
    tokenizer.add_special_tokens({'pad_token': '[PAD]'})
    model.resize_token_embeddings(len(tokenizer))

data = dataset.map(lambda x: tokenizer(
    x["article"], padding='max_length', truncation=True))

lora_config = LoraConfig(
 r=16,
 lora_alpha=32,
 lora_dropout=0.05,
 bias="none",
 task_type="CAUSAL_LM"
)

model = prepare_model_for_kbit_training(model)

# add LoRA adaptor
model = get_peft_model(model, lora_config)
model.print_trainable_parameters()

training_args = TrainingArguments(
        per_device_train_batch_size=1,
        gradient_accumulation_steps=4,
        warmup_steps=2,
        num_train_epochs=1,
        learning_rate=2e-4,
        fp16=True,
        logging_steps=1,
        output_dir=finetuned_model_path,
        optim="paged_adamw_32bit",
)

trainer = Trainer(
    model=model,
    train_dataset=data,
    args=training_args,
    data_collator=DataCollatorForLanguageModeling(tokenizer, mlm=False),
)
model.config.use_cache = False  # silence the warnings. Please re-enable for inference!

trainer.train()

# Merge the fine tuned layer with the base model and save it
# you can remove the line below if you only want to store the LoRA layer
model = model.merge_and_unload()

model.save_pretrained(finetuned_model_path)
tokenizer.save_pretrained(finetuned_model_path)
# Beginning of story in the dataset
prompt = """
In the late action between Generals


Brown and Riall, it appears our men fought
with a courage and perseverance, that would
"""
input_ids = tokenizer(prompt, return_tensors="pt").input_ids
gen_tokens = model.generate(
    input_ids,
    do_sample=True,
    temperature=0.8,
    max_length=100,
)
print(tokenizer.batch_decode(gen_tokens)[0])
```

Let's review the high level of what we've included in fine-tune.py. First we load the base model from GCS using GCS Fuse. Then we load the dataset from HuggingFace. The finetuning uses PEFT which stands for Parameter-Efficient Fine-Tuning. It is a technique that allows you to fine tune an LLM using a smaller number of parameters, which makes it more efficient, flexible and less computationally expensive.

The fine-tuned model initially are saved as separate LoRA weights. In the fine-tune.py script, the base model and LoRA weights are merged so the fine-tuned model can be used as a standalone model. This does utilize more storage than needed, but in return you get better compatibility with different libraries for serving.

Now we need to run the fine-tune.py script inside a container that has all the depdencies. The container image at us-docker.pkg.dev/google-samples/containers/gke/llama-7b-fine-tune-example includes the above fine-tune.py script and all required depencies. Alternatively, you can build and publish the image yourself by using the Dockerfile in this repo: <https://github.com/GoogleCloudPlatform/ai-on-gke/tree/main/tutorials-and-examples/genAI-LLM/finetuning-llama-7b-on-l4> .

Verify your environment variables are still set correctly:

```sh
echo "Bucket: $BUCKET_NAME"
# Bucket: qwiklabs-asl-02-cd54d6e804de-llama-l4
```

Let's use a Kubernetes Job to fine-tune the model.

```yml
cat - <<'EOF' | envsubst | kubectl apply -f -
apiVersion: batch/v1
kind: Job
metadata:
  name: finetune-job
  namespace: default
spec:
  backoffLimit: 2
  template:
    metadata:
      annotations:
        kubectl.kubernetes.io/default-container: finetuner
        gke-gcsfuse/volumes: "true"
        gke-gcsfuse/memory-limit: 400Mi
        gke-gcsfuse/ephemeral-storage-limit: 30Gi
    spec:
      terminationGracePeriodSeconds: 60
      containers:
      - name: finetuner
        image: us-docker.pkg.dev/google-samples/containers/gke/llama-7b-fine-tune-example
        resources:
          limits:
            nvidia.com/gpu: 8
        volumeMounts:
        - name: gcs-fuse-csi-ephemeral
          mountPath: /gcs-mount
      serviceAccountName: l4-lab
      volumes:
      - name: gcs-fuse-csi-ephemeral
        csi:
          driver: gcsfuse.csi.storage.gke.io
          volumeAttributes:
            bucketName: $BUCKET_NAME
            mountOptions: "implicit-dirs"
      nodeSelector:
        cloud.google.com/gke-accelerator: nvidia-l4
      restartPolicy: OnFailure
EOF
```

### Verify

```sh
# Verify that the file Job was created and that $BUCKET_NAME got replaced with the correct values. A Pod should have been created, which you can verify by running:
kubectl describe pod -l job-name=finetune-job

# Warning  FailedScheduling  61s   default-scheduler   0/1 nodes are available: 1 node(s) didn't match Pod's node affinity/selector. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.
# Normal   TriggeredScaleUp  25s   cluster-autoscaler  pod triggered scale-up: [{https://www.googleapis.com/compute/v1/projects/qwiklabs-asl-02-0078ce52f2c5/zones/us-west1-a/instanceGroups/gke-ml-gke-gpupool-c0916bac-grp 0->1 (max: 3)}]
```

#### Response: 2024-10-23

這次的 lab 因為 GCE 資源不足 (GPU 仍然為珍貴資源)

```sh
Name:             finetune-job-jvqfg
Namespace:        default
Priority:         0
Service Account:  l4-lab
Node:             <none>
Labels:           batch.kubernetes.io/controller-uid=142d9a85-1172-4fa1-ba22-92d633a19b90
                  batch.kubernetes.io/job-name=finetune-job
                  controller-uid=142d9a85-1172-4fa1-ba22-92d633a19b90
                  job-name=finetune-job
Annotations:      gke-gcsfuse/ephemeral-storage-limit: 30Gi
                  gke-gcsfuse/memory-limit: 400Mi
                  gke-gcsfuse/volumes: true
                  kubectl.kubernetes.io/default-container: finetuner
Status:           Pending
IP:               
IPs:              <none>
Controlled By:    Job/finetune-job
Init Containers:
  gke-gcsfuse-sidecar:
    Image:           gke.gcr.io/gcs-fuse-csi-driver-sidecar-mounter:v1.5.0-gke.2@sha256:31233154ece95dfec98599f3ccaf1e4e51a75b6a094d8df7b05b0209ecf423fa
    Port:            <none>
    Host Port:       <none>
    SeccompProfile:  RuntimeDefault
    Args:
      --v=5
    Limits:
      ephemeral-storage:  30Gi
      memory:             400Mi
    Requests:
      cpu:                250m
      ephemeral-storage:  30Gi
      memory:             400Mi
    Environment:
      NATIVE_SIDECAR:  TRUE
    Mounts:
      /gcsfuse-buffer from gke-gcsfuse-buffer (rw)
      /gcsfuse-cache from gke-gcsfuse-cache (rw)
      /gcsfuse-tmp from gke-gcsfuse-tmp (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-plhv4 (ro)
Containers:
  finetuner:
    Image:      us-docker.pkg.dev/google-samples/containers/gke/llama-7b-fine-tune-example
    Port:       <none>
    Host Port:  <none>
    Limits:
      nvidia.com/gpu:  8
    Requests:
      nvidia.com/gpu:  8
    Environment:       <none>
    Mounts:
      /gcs-mount from gcs-fuse-csi-ephemeral (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-plhv4 (ro)
Conditions:
  Type           Status
  PodScheduled   False 
Volumes:
  gke-gcsfuse-tmp:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  gke-gcsfuse-buffer:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  gke-gcsfuse-cache:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  gcs-fuse-csi-ephemeral:
    Type:              CSI (a Container Storage Interface (CSI) volume source)
    Driver:            gcsfuse.csi.storage.gke.io
    FSType:            
    ReadOnly:          false
    VolumeAttributes:      bucketName=qwiklabs-asl-00-98aeeab1318c-llama-l4
                           mountOptions=implicit-dirs
  kube-api-access-plhv4:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              cloud.google.com/gke-accelerator=nvidia-l4
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
                             nvidia.com/gpu:NoSchedule op=Exists
Events:
  Type     Reason            Age   From                Message
  ----     ------            ----  ----                -------
  Warning  FailedScheduling  16s   default-scheduler   0/1 nodes are available: 1 node(s) didn't match Pod's node affinity/selector. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.
  Normal   TriggeredScaleUp  14s   cluster-autoscaler  pod triggered scale-up: [{https://www.googleapis.com/compute/v1/projects/qwiklabs-asl-00-98aeeab1318c/zones/us-central1-b/instanceGroups/gke-ml-gke-gpupool-08500106-grp 0->1 (max: 3)}]

Events:
  Type     Reason             Age                 From                Message
  ----     ------             ----                ----                -------
  Normal   TriggeredScaleUp   114s                cluster-autoscaler  pod triggered scale-up: [{https://www.googleapis.com/compute/v1/projects/qwiklabs-asl-00-98aeeab1318c/zones/us-central1-b/instanceGroups/gke-ml-gke-gpupool-08500106-grp 0->1 (max: 3)}]
  Warning  FailedScaleUp      81s                 cluster-autoscaler  Node scale up in zones us-central1-b associated with this pod failed: GCE out of resources. Pod is at risk of not being scheduled.
  Warning  FailedScheduling   69s (x2 over 116s)  default-scheduler   0/1 nodes are available: 1 node(s) didn't match Pod's node affinity/selector. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.
  Normal   NotTriggerScaleUp  69s                 cluster-autoscaler  pod didn't trigger scale-up: 2 in backoff after failed scale-up
```

#### Reponse: 2024-10-24

```sh
Name:             finetune-job-6k6mj
Namespace:        default
Priority:         0
Service Account:  l4-lab
Node:             <none>
Labels:           batch.kubernetes.io/controller-uid=d5f37943-309d-41dc-9697-bd43561f149d
                  batch.kubernetes.io/job-name=finetune-job
                  controller-uid=d5f37943-309d-41dc-9697-bd43561f149d
                  job-name=finetune-job
Annotations:      gke-gcsfuse/ephemeral-storage-limit: 30Gi
                  gke-gcsfuse/memory-limit: 400Mi
                  gke-gcsfuse/volumes: true
                  kubectl.kubernetes.io/default-container: finetuner
Status:           Pending
IP:               
IPs:              <none>
Controlled By:    Job/finetune-job
Init Containers:
  gke-gcsfuse-sidecar:
    Image:           gke.gcr.io/gcs-fuse-csi-driver-sidecar-mounter:v1.5.0-gke.2@sha256:31233154ece95dfec98599f3ccaf1e4e51a75b6a094d8df7b05b0209ecf423fa
    Port:            <none>
    Host Port:       <none>
    SeccompProfile:  RuntimeDefault
    Args:
      --v=5
    Limits:
      ephemeral-storage:  30Gi
      memory:             400Mi
    Requests:
      cpu:                250m
      ephemeral-storage:  30Gi
      memory:             400Mi
    Environment:
      NATIVE_SIDECAR:  TRUE
    Mounts:
      /gcsfuse-buffer from gke-gcsfuse-buffer (rw)
      /gcsfuse-cache from gke-gcsfuse-cache (rw)
      /gcsfuse-tmp from gke-gcsfuse-tmp (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-rd9gf (ro)
Containers:
  finetuner:
    Image:      us-docker.pkg.dev/google-samples/containers/gke/llama-7b-fine-tune-example
    Port:       <none>
    Host Port:  <none>
    Limits:
      nvidia.com/gpu:  8
    Requests:
      nvidia.com/gpu:  8
    Environment:       <none>
    Mounts:
      /gcs-mount from gcs-fuse-csi-ephemeral (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-rd9gf (ro)
Conditions:
  Type           Status
  PodScheduled   False 
Volumes:
  gke-gcsfuse-tmp:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  gke-gcsfuse-buffer:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  gke-gcsfuse-cache:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     
    SizeLimit:  <unset>
  gcs-fuse-csi-ephemeral:
    Type:              CSI (a Container Storage Interface (CSI) volume source)
    Driver:            gcsfuse.csi.storage.gke.io
    FSType:            
    ReadOnly:          false
    VolumeAttributes:      bucketName=qwiklabs-asl-02-cd54d6e804de-llama-l4
                           mountOptions=implicit-dirs
  kube-api-access-rd9gf:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              cloud.google.com/gke-accelerator=nvidia-l4
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
                             nvidia.com/gpu:NoSchedule op=Exists
Events:
  Type     Reason             Age                    From                Message
  ----     ------             ----                   ----                -------
  Warning  FailedScheduling   8m42s                  default-scheduler   0/1 nodes are available: 1 node(s) didn't match Pod's node affinity/selector. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.
  Warning  FailedScheduling   117s (x2 over 7m23s)   default-scheduler   0/1 nodes are available: 1 node(s) didn't match Pod's node affinity/selector. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.
  Normal   TriggeredScaleUp   2m58s (x2 over 8m39s)  cluster-autoscaler  pod triggered scale-up: [{https://www.googleapis.com/compute/v1/projects/qwiklabs-asl-02-cd54d6e804de/zones/us-central1-a/instanceGroups/gke-ml-gke-gpupool-18472bb2-grp 0->1 (max: 3)}]
  Warning  FailedScaleUp      2m14s (x2 over 8m5s)   cluster-autoscaler  Node scale up in zones us-central1-a associated with this pod failed: GCE out of resources. Pod is at risk of not being scheduled.
  Normal   NotTriggerScaleUp  102s (x27 over 7m23s)  cluster-autoscaler  pod didn't trigger scale-up: 2 in backoff after failed scale-up
```

You should see a pod triggered scale-up message under Events after about 30 seconds. Then it will take another 2 minutes for a new GKE node with 8 x L4 GPUs to spin up.

```sh
# You can observe the status of the nodes by running:
kubectl get nodes -o wide

# Once the Pod gets into running state you can watch the logs of the training:
kubectl logs -f -l job-name=finetune-job

# You can watch the training steps and observe the loss go down over time. The training took 22 minutes and 16 seconds for me when I ran it, your results might differ.
# Once Job completes, you should see a fine-tuned model in your GCS bucket under the llama2-7b-american-stories path. Verify by running:
gcloud storage ls -l gs://$BUCKET_NAME/llama2-7b-american-stories
```

## Serve the finetuned Model using TGI

In this section, you deploy the finetuned model to GKE with TGI.

```yml
cat - <<'EOF' | envsubst | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tgi-finetuned-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: finetuned-server
  template:
    metadata:
      annotations:
        kubectl.kubernetes.io/default-container: inference-server
        gke-gcsfuse/volumes: "true"
        gke-gcsfuse/memory-limit: 400Mi
        gke-gcsfuse/ephemeral-storage-limit: 30Gi
      labels:
        app: finetuned-server
        ai.gke.io/inference-server: text-generation-inference
    spec:
      serviceAccountName: l4-lab
      containers:
      - name: inference-server
        image: ghcr.io/huggingface/text-generation-inference:1.4.4
        resources:
          limits:
            nvidia.com/gpu: 8
        env:
        - name: MODEL_ID
          value: /gcs-mount/llama2-7b-american-stories
        - name: NUM_SHARD
          value: "8"
        - name: PORT
          value: "8000"
        volumeMounts:
        - mountPath: /dev/shm
          name: dshm
        - name: gcs-fuse-csi-ephemeral
          mountPath: /gcs-mount
      volumes:
      - name: gcs-fuse-csi-ephemeral
        csi:
          driver: gcsfuse.csi.storage.gke.io
          volumeAttributes:
            bucketName: $BUCKET_NAME
            mountOptions: "implicit-dirs"
      - name: dshm
        emptyDir:
          medium: Memory
      nodeSelector:
        cloud.google.com/gke-accelerator: nvidia-l4
---
apiVersion: v1
kind: Service
metadata:
  name: llm-service
spec:
  selector:
    app: finetuned-server
  type: ClusterIP
  ports:
    - protocol: TCP
      port: 8000
      targetPort: 8000
EOF
```

```sh
# Wait for the Deployment to be available:
kubectl wait --for=condition=Available --timeout=700s deployment/tgi-finetuned-deployment

# View the logs from the running Deployment:
kubectl logs -f -l app=finetuned-server
```

### Set up port forwarding

```sh
# Run the following command to set up port forwarding to the model:
kubectl port-forward service/llm-service 8000:8000
# Forwarding from 127.0.0.1:8000 -> 8000
```

### Interact with the model using curl

This section shows how you can perform a basic smoke test to verify your finetuned models.

In a new terminal session, use curl to chat with your model:

```sh
USER_PROMPT="The biggest story of the year 1811 was"

curl -X POST http://localhost:8000/generate \
  -H "Content-Type: application/json" \
  -d @- <<EOF
{
    "inputs": "<start_of_turn>user\n${USER_PROMPT}<end_of_turn>\n",
    "parameters": {
        "temperature": 0.90,
        "top_p": 0.95,
        "max_new_tokens": 128
    }
}
EOF
```

The following output shows an example of the model response:

```json
{"generated_text":"\n\nnearly closed. In theset confe-nance;sae did\nthe northern frontier of New York appear\nbefore the British troops. They seemed with\nin rifle-shot of the inhabitants. The rebel'\ngion had commenced with full sails on the\nAmerican coast; the ray of the sun had made\nits first appearance ; the followers of Fannious\nBuonapartz had shaken the ground of the\nCanadian province. All was incertainty and\napprehension. Had victory been with the\nAmericans, the hundredth"
```

## Go wild: Show your creativity

Take a look at the available guides in the GCP docs and models on the Hugging Face website and try to fine-tune a model of your choice. You can also try to deploy the model to GKE and serve it using TGI, Ray, TensorFlow Serving or vLLM.

## Ref

* <https://github.com/GoogleCloudPlatform/ai-on-gke/tree/main/tutorials-and-examples/genAI-LLM/finetuning-llama-7b-on-l4>
* <https://cloud.google.com/kubernetes-engine/docs/quickstarts/train-model-gpus-standard>
