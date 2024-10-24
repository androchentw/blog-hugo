# # GKE Chatbot | K8s Summit 2024 GCP Workshop

## Preparation

* [Run Gemma 2 Powered Chatbot on GKE Autopilot](https://dennygoog.gitlab.io/workshops/run-gemma-chatbot-on-gke-autopilot/)
  * 主要使用這個頁面的 command, 僅使用 qwiklab 的資源

```sh
CLUSTER_NAME=my-cluster
CLUSTER_LOCATION=us-central1

gcloud container clusters create-auto ${CLUSTER_NAME} \
  --location=${CLUSTER_LOCATION}

# kubeconfig entry generated for my-cluster.
# NAME: my-cluster
# LOCATION: us-central1
# MASTER_VERSION: 1.30.5-gke.1014001
# MASTER_IP: 34.45.80.180
# MACHINE_TYPE: e2-small
# NODE_VERSION: 1.30.5-gke.1014001
# NUM_NODES: 3
# STATUS: RUNNING

kubectl cluster-info
# Kubernetes control plane is running at https://34.45.80.180
# GLBCDefaultBackend is running at https://34.45.80.180/api/v1/namespaces/kube-system/services/default-http-backend:http/proxy
# KubeDNS is running at https://34.45.80.180/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
# Metrics-server is running at https://34.45.80.180/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy

# To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## 任務 2. 部署 Ollama

```sh
kubectl apply -f ollama.yaml
# Warning: autopilot-default-resources-mutator:Autopilot updated StatefulSet default/ollama: defaulted unspecified 'nvidia.com/gpu' resource for containers [ollama] (see http://g.co/gke/autopilot-defaults).
# statefulset.apps/ollama created
# service/ollama created

kubectl get pods -w
# 等待 ollama-0 Pod 變成 Running 狀態，表示 Ollama 已成功部署。

kubectl get nodes
# NAME                                        STATUS   ROLES    AGE     VERSION
# gk3-my-cluster-nap-1l47y8kj-033ca61f-rgvm   Ready    <none>   2m54s   v1.30.5-gke.1014001
# gk3-my-cluster-nap-nwlb0qz1-ea6bcb2c-b44d   Ready    <none>   2m9s    v1.30.5-gke.1014001
```

## 任務 3. 使用 Ollama CLI 與 Gemma 2 互動

```sh
# 安裝 Ollama CLI：在 Cloud Shell 中執行以下指令安裝 Ollama CLI：
curl -fsSL https://ollama.com/install.sh | sh

# 將 Ollama 服務端口轉發到本地： 執行以下指令，將 Ollama 服務的 11434 端口轉發到本地 (Cloud Shell) 的 11434 端口：
kubectl port-forward svc/ollama 11434:11434

# 在新分頁中執行 Gemma 2 模型： 在新的終端分頁中，設定 OLLAMA_HOST 環境變數，指定 Ollama API 的地址，然後使用 ollama run 指令執行 Gemma 2 模型：
OLLAMA_HOST=http://localhost:11434 ollama run gemma2

>>> 你好！

# 你好！👋  有什么我可以帮你的吗？😊
```

## 任務 4. 部署 Open WebUI，打造更友善的 Chatbot 互動介面

`openwebui.yaml`

```yml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: openwebui
spec:
  selector:
    matchLabels:
      app: openwebui
  serviceName: openwebui
  template:
    metadata:
      labels:
        app: openwebui
    spec:
      containers:
      - name: openwebui
        image: ghcr.io/open-webui/open-webui:main
        ports:
        - containerPort: 8080
        env:
        - name: OLLAMA_BASE_URL
          value: http://ollama:11434
        - name: WEBUI_AUTH
          value: "False"
        resources:
          requests:
            cpu: "1"
            memory: 1Gi
          limits:
            cpu: "1"
            memory: 1Gi
        volumeMounts:
        - name: openwebui
          mountPath: /app/backend/data
  volumeClaimTemplates:
  - metadata:
      name: openwebui
    spec:
      accessModes:
      - ReadWriteOnce
      storageClassName: standard-rwo
      resources:
        requests:
          storage: 10Gi
---
apiVersion: v1
kind: Service
metadata:
  name: openwebui
spec:
  type: LoadBalancer
  selector:
    app: openwebui
  ports:
  - port: 80
    targetPort: 8080
```

```sh
# 部署 Open WebUI： 儲存 openwebui.yaml 檔案後，在 Cloud Shell 中執行以下指令部署 Open WebUI：
kubectl apply -f openwebui.yaml
# statefulset.apps/openwebui created
# service/openwebui created


# 取得 Load Balancer IP 地址： 執行以下指令取得 Load Balancer 的外部 IP 地址：
kubectl get service openwebui
# NAME        TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)        AGE
# openwebui   LoadBalancer   34.118.229.145   34.28.179.30   80:31505/TCP   45s
```

透過瀏覽器訪問 Open WebUI： 開啟瀏覽器，並在網址列輸入 http://<EXTERNAL-IP> (將 <EXTERNAL-IP> 替換成您取得的 Load Balancer IP 地址)。

<http://34.28.179.30>

## Ref: Serving an Open-source Generative AI Model with GKE | SAW047

* 參考 [Serving an Open-source Generative AI Model with GKE | SAW047](https://explore.qwiklabs.com/classrooms/16150/labs/95675)

This lab is intended for MLOps or DevOps engineers or platform administrator that want to use Google Kubernetes Engine (GKE) orchestration capabilities to serve large language models (LLMs).

In this lab you will learn how to:

* Provision a complete Kubernetes cluster using GKE
* Serve the open [Gemma 2B](https://www.kaggle.com/models/google/gemma) LLM using the Hugging Face [Text Generation Inference](https://huggingface.co/docs/text-generation-inference/en/index) toolkit
* Deploy a web-based chat application to interact with the deployed model using [Gradio](https://www.gradio.app/docs/gradio/interface)

```sh
gcloud auth list

gcloud config list project
```

### Get Access to Gemma

* Sign the license consent agreement: Access the [model consent page](https://www.kaggle.com/models/google/gemma) on Kaggle.com.

### Generate an access token

```txt
2024-10-23-k8s-summit-gcp-1
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
```

```sh
export HF_TOKEN=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

git clone https://github.com/gke-demos/serving-gemma-2b.git
cd serving-gemma-2b
ls -l *.yaml
```

## Create Google Kubernetes Engine Cluster

```sh
gcloud container clusters create-auto ml-cluster --release-channel rapid \
  --region "us-east4"

kubectl cluster-info
```

## Review the Deployment Manifests

### `gemma-2b-deployment.yaml`

TGI has support for multiple open text generation models. This manifest uses the container image provide by Hugging Face to serve the Falcon 7B model. This same deployment can be used to serve other models by simply replacing the MODEL_ID environment variable. Also note that this deployment uses a single NVIDIA L4 GPU for acceleration. The L4 is a great choice for serving models with memory requirements less than 24GB. TGI also support sharding larger models, allowing you to serve a model with multiple GPUs. For example, you can serve the larger Falcon 40B model by enabling sharding and using two L4 GPUs in the deployment.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tgi-gemma-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: gemma-server
  template:
    metadata:
      labels:
        app: gemma-server
        ai.gke.io/model: gemma-2b-it
        ai.gke.io/inference-server: text-generation-inference
        examples.ai.gke.io/source: user-guide
    spec:
      containers:
      - name: inference-server
        image: us-docker.pkg.dev/vertex-ai/vertex-vision-model-garden-dockers/pytorch-hf-tgi-serve:20240220_0936_RC01
        resources:
          requests:
            cpu: "2"
            memory: "7Gi"
            ephemeral-storage: "20Gi"
            nvidia.com/gpu: 1
          limits:
            cpu: "2"
            memory: "7Gi"
            ephemeral-storage: "20Gi"
            nvidia.com/gpu: 1
        args:
        - --model-id=$(MODEL_ID)
        - --num-shard=1
        env:
        - name: MODEL_ID
          value: google/gemma-2b-it
        - name: PORT
          value: "8000"
        - name: HUGGING_FACE_HUB_TOKEN
          valueFrom:
            secretKeyRef:
              name: hf-secret
              key: hf_api_token
        volumeMounts:
        - mountPath: /dev/shm
          name: dshm
      volumes:
      - name: dshm
        emptyDir:
          medium: Memory
      nodeSelector:
        cloud.google.com/gke-accelerator: nvidia-l4
```

### `gemma-2b-service.yaml`

This manifest simply exposes the TGI deployment externally using a TCP load balancer. Note the name: llm-service field as this will be used by Gradio to communicate with the serving endpoint later.

```sh
apiVersion: v1
kind: Service
metadata:
  name: llm-service
spec:
  selector:
    app: gemma-server
  type: LoadBalancer
  ports:
  - protocol: TCP
    port: 8000
    targetPort: 8000
```

### `gemma-2b-monitoring.yaml`

TGI provides a Prometheus-compatible endpoint on its default port. Here we configure Managed Prometheus to scrape the metrics from the TGI deployment every 30 seconds.

```yml
apiVersion: monitoring.googleapis.com/v1
kind: PodMonitoring
metadata:
  name: gemma-2b-tgi-monitor
spec:
  selector:
    matchLabels:
      app: gemma-server
  endpoints:
  - port: 8000
    interval: 30s
```

### `gradio.yaml`

Gradio is an OSS framework for building chat applications for GenAI models. This manifest deploys a prebuilt Gradio sample application which connects to the Falcon 7B model deployment and exposes it via a TCP load balancer.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: gradio
  labels:
    app: gradio
spec:
  replicas: 1
  selector:
    matchLabels:
      app: gradio
  template:
    metadata:
      labels:
        app: gradio
    spec:
      containers:
      - name: gradio
        image: us-docker.pkg.dev/google-samples/containers/gke/gradio-app:v1.0.0
        resources:
          requests:
            cpu: "512m"
            memory: "512Mi"
          limits:
            cpu: "1"
            memory: "512Mi"
        env:
        - name: CONTEXT_PATH
          value: "/generate"
        - name: HOST
          value: "http://llm-service:8000"
        - name: LLM_ENGINE
          value: "tgi"
        - name: MODEL_ID
          value: "gemma"
        - name: USER_PROMPT
          value: "user\nprompt\n"
        - name: SYSTEM_PROMPT
          value: "model\nprompt\n"
        ports:
        - containerPort: 7860
---
apiVersion: v1
kind: Service
metadata:
  name: gradio
spec:
  selector:
    app: gradio
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 7860
  type: LoadBalancer
```

## Check Cluster Creation Status

[AI/ML on GKE](https://explore.qwiklabs.com/classrooms/16150/labs/g.co/cloud/gke-aiml)
[ ] TODO 連結 Page not found
https://cloud.google.com/kubernetes-engine/docs/integrations/ai-infra

## Deploy Gemma 2B

### Serve Gemma 2B using TGI

```sh
kubectl create secret generic hf-secret \
  --from-literal=hf_api_token=${HF_TOKEN} \
  --dry-run=client -o yaml | kubectl apply -f -

kubectl apply -f gemma-2b-deployment.yaml

kubectl apply -f gemma-2b-service.yaml
```

### Check Deployment Status

```sh
watch kubectl get pods
```

### Deploy the Gradio Chat App

```sh
kubectl apply -f gradio.yaml

watch kubectl get deployments gradio

watch kubectl get service gradio
```

## Chat with Gemma

```sh
kubectl get service gradio -o json | jq -r .status.loadBalancer.ingress[].ip
# 34.125.152.184
# http://GRADIO_IP:8080
```

## (Optional) Monitor TGI

```sh
kubectl apply -f gemma-2b-monitoring.yaml
```

## Ref

* [AI/ML orchestration on GKE](https://cloud.google.com/kubernetes-engine/docs/integrations/ai-infra)
* [ai-on-gke](https://github.com/GoogleCloudPlatform/ai-on-gke)
