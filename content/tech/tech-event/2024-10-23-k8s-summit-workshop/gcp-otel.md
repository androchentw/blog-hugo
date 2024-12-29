# GCP OTel | K8s Summit 2024 GCP Workshop

Ref

* [OpenTelemetry 可觀測性的未來](https://github.com/marcustung/obervability-opentelemetry/blob/main/OpenTelemetry%20%E5%8F%AF%E8%A7%80%E6%B8%AC%E6%80%A7%E7%9A%84%E6%9C%AA%E4%BE%86.md)

## Preparation

* [Application Monitoring with OpenTelemetry](https://explore.qwiklabs.com/classrooms/16111/labs/95466)

OpenTelemetry是CNCF推廣的[容器平台監控技術](https://github.com/open-telemetry/opentelemetry-collector-contrib)，針對SRE常用的Metrics, Log, 以及Trace提供了完整的支援。其廣大生態圈，不但可在無侵入的狀態下，廣泛支持各種的程式語言(e.g. Python, Java, .NET, JS等），也提供讓SRE可彈性客制監控標的。

雖然OpenTelemetry社群推出了OpenTelemetry Operator，希望簡化整個的Collector安裝流程。在第一個Lab，我們會學習如何通過OpenTelemetry Operator部署[完整支援第三方Exporter/Receiver的完整Collector](https://www.cncf.io/blog/2021/08/26/opentelemetry-becomes-a-cncf-incubating-project/)，而非僅有核心模組的Collector，並加上Auto-Instrumentation部署，這樣的部署能在不額外添加任何程式碼下，通過OpenTelemetry直接收集呼叫軌跡(Trace)。Metrics的部分，Lab1會教大家如果通過引入基於語言Prometheus函式庫，快速產生服務使用到API的效能統計資訊。

<img style="width:80%;" src="https://cdn.qwiklabs.com/97gl2aYFHR7jVj1d7qHLw9oW5%2FaUugd7rd98Q9St%2BkI%3D">
<p align="center"><sub><sup>
  OTel 架構
</sup></sub></p>

### What will you learn?

這個 Workshop 希望讓大家了解 OpenTelemetry Collector Core Library 的能力：

1. 如何通過OpenTelemetry Operator搭建OpenTelemetry Collector
2. 設定Telemetry ＋ Metrics 的Collector Pipeline
3. 在不增加任何程式碼下，通過OpenTelemetry Auto-Instrumentation得到服務的呼叫軌跡
4. 通過Google Managed Prometheus以及Cloud Trace來展示結果

### Setup and Requirements

* Activate Cloud Shell
* 開發程式碼產生：按下 `Command + Shift + P` 組合鍵，在搜尋列中打上 `New Application`，選擇 `Kubernetes Application` ，再由中間挑選想開發的語言: 『`Python (Flask): GuestBook`』，由Cloud Code生成模板。今天我們選擇Python Flask，我們使用預設的專案名稱『guestbook-1』，按下 `Create New Applications`

```sh
Command + Shift + P
Cloud Code: New Application 
> Kubernetes Application 
> Python (Flask): GuestBook
> guestbook-1
> Create New Applications
```

### 設定 Console 專案

```sh
export PROJECT_ID="qwiklabs-gcp-01-0cda8821429a" 
gcloud config set project ${PROJECT_ID} 
gcloud config set compute/region asia-east1
gcloud config set compute/zone asia-east1-c
```

### 確認GKE叢集

```sh
# Lab創建時已經通過Terraform，預將GKE叢集建立完畢，請依照下方指令取得GKE控制檔案：
gcloud container clusters list
# NAME: lab-cluster
# LOCATION: asia-east1-a
# MASTER_VERSION: 1.30.5-gke.1014001
# MASTER_IP: 34.80.48.118
# MACHINE_TYPE: e2-standard-4
# NODE_VERSION: 1.30.5-gke.1014001
# NUM_NODES: 3
# STATUS: RUNNING

# 取得GKE控制用檔案(kubeconfig)
gcloud container clusters get-credentials lab-cluster --zone asia-east1-a
# Fetching cluster endpoint and auth data.
# kubeconfig entry generated for lab-cluster.

kubectl get node
# NAME                                              STATUS   ROLES    AGE   VERSION
# gke-lab-cluster-default-node-pool-31204075-7rct   Ready    <none>   13m   v1.30.5-gke.1014001
# gke-lab-cluster-default-node-pool-31204075-ck5t   Ready    <none>   13m   v1.30.5-gke.1014001
# gke-lab-cluster-default-node-pool-31204075-d8h3   Ready    <none>   13m   v1.30.5-gke.1014001
```

## Auto-Instrumentation with OpenTelemetry Operator

### 安裝OpenTelemetry Operator與Collector

OpenTelemetry(a.k.a otel) 的 K8S 安裝，主要由 OpenTelemetry Operator (aka otel operator) 與 Collector(aka otel collector) 兩個部分組成，其中 otel Operator 的部署，主要是為了生成(保護）otel Collector，同時，對於想要監控的服務，提供自動的 sidecar注入控制，讓開發者在不需要手動進行任何的代碼改動，就可以看到想追蹤的軌跡。

以下我們在GKE安裝Opentelemetry, 主要分為三塊安裝：Cert-Manger, Operator & Collector。

### 部署Cert Manager: Cert-Manager為了OTEL Operator提供憑證

在OTEL的運作過程中，當希望不修改現有程式，直接提供呼叫軌跡時，OTEL通過Mutation Webhook的呼叫，完成sidecar的注入。Mutation webhook的生成就需要通過[cert-manager提供API server](https://trstringer.com/admission-control-cert-manager/)可以相信的憑證資訊。

```sh
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install \
  --create-namespace \
  --namespace cert-manager \
  --set installCRDs=true \
  --set global.leaderElection.namespace=cert-manager \
  --set extraArgs={--issuer-ambient-credentials=true} \
  cert-manager jetstack/cert-manager

# "jetstack" has been added to your repositories
# Hang tight while we grab the latest from your chart repositories...
# ...Successfully got an update from the "jetstack" chart repository
# Update Complete. ⎈Happy Helming!⎈
# NAME: cert-manager
# LAST DEPLOYED: Thu Oct 24 00:45:45 2024
# NAMESPACE: cert-manager
# STATUS: deployed
# REVISION: 1
# TEST SUITE: None
# NOTES:
# ⚠️  WARNING: `installCRDs` is deprecated, use `crds.enabled` instead.
# cert-manager v1.16.1 has been deployed successfully!

# In order to begin issuing certificates, you will need to set up a ClusterIssuer
# or Issuer resource (for example, by creating a 'letsencrypt-staging' issuer).

# More information on the different types of issuers and how to configure them
# can be found in our documentation:

# https://cert-manager.io/docs/configuration/

# For information on how to configure cert-manager to automatically provision
# Certificates for Ingress resources, take a look at the `ingress-shim`
# documentation:

# https://cert-manager.io/docs/usage/ingress/
```

Note: 此次使用的GKE叢集為Public Cluster，若未來若使用Private Cluster，受限於Master節點訪問mutation webhook需要通過內部VPC網路，需開放 `9443` 防火牆。

### 部署Opentelemetry Operator

<img style="width:80%;" src="https://cdn.qwiklabs.com/JOZGAFxce0aKvQidRC6aNF2CN%2Baiks1E9b8TBkehOYw%3D">
<p align="center"><sub><sup>
  OTel Operator
</sup></sub></p>

```sh
# 這個元件具有兩個主要功能，Opentelemetry Collector的CRD生成與保護，以及Instrumentation的auto-injection。部署命令如下：
kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/latest/download/opentelemetry-operator.yaml

# namespace/opentelemetry-operator-system created
# customresourcedefinition.apiextensions.k8s.io/instrumentations.opentelemetry.io created
# customresourcedefinition.apiextensions.k8s.io/opampbridges.opentelemetry.io created
# customresourcedefinition.apiextensions.k8s.io/opentelemetrycollectors.opentelemetry.io created
# serviceaccount/opentelemetry-operator-controller-manager created
# role.rbac.authorization.k8s.io/opentelemetry-operator-leader-election-role created
# clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-manager-role created
# clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-metrics-reader created
# clusterrole.rbac.authorization.k8s.io/opentelemetry-operator-proxy-role created
# rolebinding.rbac.authorization.k8s.io/opentelemetry-operator-leader-election-rolebinding created
# clusterrolebinding.rbac.authorization.k8s.io/opentelemetry-operator-manager-rolebinding created
# clusterrolebinding.rbac.authorization.k8s.io/opentelemetry-operator-proxy-rolebinding created
# service/opentelemetry-operator-controller-manager-metrics-service created
# service/opentelemetry-operator-webhook-service created
# deployment.apps/opentelemetry-operator-controller-manager created
# certificate.cert-manager.io/opentelemetry-operator-serving-cert created
# issuer.cert-manager.io/opentelemetry-operator-selfsigned-issuer created
# mutatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-mutating-webhook-configuration created
# validatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-validating-webhook-configuration created

# 部署成功的訊息裡，我們可以快速瀏覽，找尋到以下的訊息，即可得知cert-manager所扮演的角色。
certificate.cert-manager.io/opentelemetry-operator-serving-cert created

issuer.cert-manager.io/opentelemetry-operator-selfsigned-issuer created

mutatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-mutating-webhook-configuration created

validatingwebhookconfiguration.admissionregistration.k8s.io/opentelemetry-operator-validating-webhook-configuration created
```

### 部署 OpenTelemetry Collector

接下來，我們部署OpenTelemetry Collector用以收集服務產生出的監控資訊。OpenTelemetry Controller是一個特別的CRD物件，會由OpenTelemetry Operator收到後，部署出對應的Collector pod在指定的名稱空間中。

底下我們先創建名稱空間: otel-collector，作為Collector的instance使用，為了使用Workload Identity讓這個Collector pod有足夠的權限寫入GoogleManagedPrometheus, CloudTrace, 跟Cloud Logging，我們必須先製作一個serviceAccount: otel-collector-demo，同時因為我們會使用到prometheus scrape的能力，這個serviceAccount還要加上能夠列出pod,service的RBAC。如下所示：

```sh
export K8S_SA="otel-collector-demo"
export K8S_NS="otel-collector"
export GSA="otel-collector"

kubectl create ns ${K8S_NS}

cat << EOF | kubectl apply -f -
apiVersion: v1
kind: ServiceAccount
metadata:
  name: ${K8S_SA}
  namespace: ${K8S_NS}
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: otel-collector-demo
  namespace: ${K8S_NS}
rules:
  - apiGroups: ['']
    resources: ['nodes/stats', 'pods', 'services']
    verbs: ['get', 'watch', 'list']
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: otel-collector-demo
  namespace: ${K8S_NS}
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: otel-collector-demo
subjects:
  - kind: ServiceAccount
    name: ${K8S_SA}
    namespace: ${K8S_NS}
EOF
```

response:

```sh
# namespace/otel-collector created
# serviceaccount/otel-collector-demo created
# clusterrole.rbac.authorization.k8s.io/otel-collector-demo created
# clusterrolebinding.rbac.authorization.k8s.io/otel-collector-demo created
```

由於我們等等希望將資料送到Cloud Trace, Google Managed Prometheus,跟Cloud Logging，需要設定otel-collector pod對於這三個服務的權限。我們通過workload identity設定如下

```sh
# 確認專案 PROJECT_ID變數
gcloud config set project ${PROJECT_ID}

# 設定Google Service Account: otel-collector
gcloud iam service-accounts create ${GSA}

# 綁定Cloud Trace, GMP, 以及Cloud Logging的寫入權限。
gcloud projects add-iam-policy-binding ${PROJECT_ID}\
  --member=serviceAccount:${GSA}@${PROJECT_ID}.iam.gserviceaccount.com \
  --role=roles/monitoring.metricWriter

gcloud projects add-iam-policy-binding ${PROJECT_ID}\
  --member=serviceAccount:${GSA}@${PROJECT_ID}.iam.gserviceaccount.com \
  --role=roles/cloudtrace.agent

gcloud projects add-iam-policy-binding ${PROJECT_ID}\
  --member=serviceAccount:${GSA}@${PROJECT_ID}.iam.gserviceaccount.com \
  --role=roles/logging.logWriter

# 設定Workload Identity
gcloud iam service-accounts add-iam-policy-binding \
  --role roles/iam.workloadIdentityUser \
  --member "serviceAccount:${PROJECT_ID}.svc.id.goog[${K8S_NS}/${K8S_SA}]" \
  ${GSA}@${PROJECT_ID}.iam.gserviceaccount.com \

kubectl annotate serviceaccount \
  --namespace ${K8S_NS} \
  ${K8S_SA} \
  iam.gke.io/gcp-service-account=${GSA}@${PROJECT_ID}.iam.gserviceaccount.com
```

response:

```yml
Updated property [core/project].
Created service account [otel-collector].
Updated IAM policy for project [qwiklabs-gcp-01-0cda8821429a].
bindings:
- members:
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/bigquery.admin
- members:
  - serviceAccount:250649173090@cloudbuild.gserviceaccount.com
  role: roles/cloudbuild.builds.builder
- members:
  - serviceAccount:service-250649173090@gcp-sa-cloudbuild.iam.gserviceaccount.com
  role: roles/cloudbuild.serviceAgent
- members:
  - serviceAccount:service-250649173090@compute-system.iam.gserviceaccount.com
  role: roles/compute.serviceAgent
- members:
  - serviceAccount:service-250649173090@container-engine-robot.iam.gserviceaccount.com
  role: roles/container.serviceAgent
- members:
  - serviceAccount:250649173090-compute@developer.gserviceaccount.com
  - serviceAccount:250649173090@cloudservices.gserviceaccount.com
  role: roles/editor
- members:
  - serviceAccount:otel-collector@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/monitoring.metricWriter
- members:
  - serviceAccount:admiral@qwiklabs-services-prod.iam.gserviceaccount.com
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  - user:student-03-c40dfb54bf6e@qwiklabs.net
  role: roles/owner
- members:
  - serviceAccount:service-250649173090@serverless-robot-prod.iam.gserviceaccount.com
  role: roles/run.serviceAgent
- members:
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/storage.admin
- members:
  - user:student-03-c40dfb54bf6e@qwiklabs.net
  role: roles/viewer
etag: BwYlLlgifis=
version: 1
Updated IAM policy for project [qwiklabs-gcp-01-0cda8821429a].
bindings:
- members:
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/bigquery.admin
- members:
  - serviceAccount:250649173090@cloudbuild.gserviceaccount.com
  role: roles/cloudbuild.builds.builder
- members:
  - serviceAccount:service-250649173090@gcp-sa-cloudbuild.iam.gserviceaccount.com
  role: roles/cloudbuild.serviceAgent
- members:
  - serviceAccount:otel-collector@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/cloudtrace.agent
- members:
  - serviceAccount:service-250649173090@compute-system.iam.gserviceaccount.com
  role: roles/compute.serviceAgent
- members:
  - serviceAccount:service-250649173090@container-engine-robot.iam.gserviceaccount.com
  role: roles/container.serviceAgent
- members:
  - serviceAccount:250649173090-compute@developer.gserviceaccount.com
  - serviceAccount:250649173090@cloudservices.gserviceaccount.com
  role: roles/editor
- members:
  - serviceAccount:otel-collector@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/monitoring.metricWriter
- members:
  - serviceAccount:admiral@qwiklabs-services-prod.iam.gserviceaccount.com
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  - user:student-03-c40dfb54bf6e@qwiklabs.net
  role: roles/owner
- members:
  - serviceAccount:service-250649173090@serverless-robot-prod.iam.gserviceaccount.com
  role: roles/run.serviceAgent
- members:
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/storage.admin
- members:
  - user:student-03-c40dfb54bf6e@qwiklabs.net
  role: roles/viewer
etag: BwYlLlhY3L0=
version: 1
Updated IAM policy for project [qwiklabs-gcp-01-0cda8821429a].
bindings:
- members:
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/bigquery.admin
- members:
  - serviceAccount:250649173090@cloudbuild.gserviceaccount.com
  role: roles/cloudbuild.builds.builder
- members:
  - serviceAccount:service-250649173090@gcp-sa-cloudbuild.iam.gserviceaccount.com
  role: roles/cloudbuild.serviceAgent
- members:
  - serviceAccount:otel-collector@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/cloudtrace.agent
- members:
  - serviceAccount:service-250649173090@compute-system.iam.gserviceaccount.com
  role: roles/compute.serviceAgent
- members:
  - serviceAccount:service-250649173090@container-engine-robot.iam.gserviceaccount.com
  role: roles/container.serviceAgent
- members:
  - serviceAccount:250649173090-compute@developer.gserviceaccount.com
  - serviceAccount:250649173090@cloudservices.gserviceaccount.com
  role: roles/editor
- members:
  - serviceAccount:otel-collector@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/logging.logWriter
- members:
  - serviceAccount:otel-collector@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/monitoring.metricWriter
- members:
  - serviceAccount:admiral@qwiklabs-services-prod.iam.gserviceaccount.com
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  - user:student-03-c40dfb54bf6e@qwiklabs.net
  role: roles/owner
- members:
  - serviceAccount:service-250649173090@serverless-robot-prod.iam.gserviceaccount.com
  role: roles/run.serviceAgent
- members:
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com
  role: roles/storage.admin
- members:
  - user:student-03-c40dfb54bf6e@qwiklabs.net
  role: roles/viewer
etag: BwYlLliOQ4A=
version: 1
Updated IAM policy for serviceAccount [otel-collector@qwiklabs-gcp-01-0cda8821429a.iam.gserviceaccount.com].
bindings:
- members:
  - serviceAccount:qwiklabs-gcp-01-0cda8821429a.svc.id.goog[otel-collector/otel-collector-demo]
  role: roles/iam.workloadIdentityUser
etag: BwYlLljFTgM=
version: 1
serviceaccount/otel-collector-demo annotated
```

<img style="width:80%;" src="https://cdn.qwiklabs.com/Vuy9Gse8A08Sils90J%2BJHCYuUdarczVZ1pzvepPt%2B5I%3D">
<p align="center"><sub><sup>
  OTel Instrumentation
</sup></sub></p>

Collector的設定，主要分為serviceAccount 、image以及config三個欄位：

1. serviceAccount：是為了使用workload identity，因此不能用controller自行產生的serviceAccount而需要額外設定。
2. image欄位：是為了讓我們可以使用到第三方的Receiver + Exporter (e.g. googlecloud, googlemanagedprometheus)。
3. 剩下的Collector config設定：設定元素分為Receiver, Processor, 跟Exporter三層，可使用其組成多條的Pipeline，作為為Metric, Log,跟Trace的傳遞之用。下方config為例，該Controller會組成Metric, Trace兩條Pipeline，每條pipeline均以Opentelemetry receiver接入，以log的方式輸出於屏幕。

```yml
cat << EOF | kubectl apply -f -
apiVersion: opentelemetry.io/v1alpha1
kind: OpenTelemetryCollector
metadata:
 name: otel
 namespace: ${K8S_NS}
 labels:
   app: otel-collector
spec:
 serviceAccount: ${K8S_SA}
 image: otel/opentelemetry-collector-contrib:latest
 config: |
   receivers:
     otlp:
       protocols:
         grpc:
         http:
     prometheus:
       config:
         scrape_configs:
         - job_name: 'k8s_pods'
           scrape_interval: 30s
           kubernetes_sd_configs:
           - role: pod
           relabel_configs:
           - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
             action: "keep"
             regex: "true"
           - source_labels: [__meta_kubernetes_pod_label_k8s_app]
             action: "drop"
             regex: "cilium"
           - source_labels: [__meta_kubernetes_pod_label_istio_io_rev]
             action: "drop"
             regex: "asm-managed"
           - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
             action: replace
             target_label: __metrics_path__
             regex: (.+)
           - source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
             action: replace
             regex: ([^:]+)(?::\d+)?;(\d+)
             replacement: \$\$1:\$\$2
             target_label: __address__
           - action: labelmap
             regex: __meta_kubernetes_pod_label_(.+)
   processors:
     batch:
       send_batch_max_size: 100
       send_batch_size: 100
       timeout: 5s
     resourcedetection:
       detectors: [gcp]
       timeout: 10s

   exporters:
     debug:
       verbosity: detailed
     googlemanagedprometheus:
       project: ${PROJECT_ID}
     googlecloud:

   service:
     telemetry:
       logs:
         level: "debug"
       metrics:
         address: ":8888"
     pipelines:
       traces:
         receivers: [otlp]
         processors: [batch]
         exporters: [debug, googlecloud]
       metrics:
         receivers: [prometheus]
         processors: [batch, resourcedetection]
         exporters: [googlemanagedprometheus]
EOF
```

validation

```sh
kubectl -n otel-collector get pod
# NAME                             READY   STATUS    RESTARTS   AGE
# otel-collector-bbf668879-d57h6   1/1     Running   0          8m12s
```

## 部署 Instrumentation 物件

最後部署Instrumentation的物件，本物件同樣由OpenTelemetry-Operator進行管理，主要是為了讓注入時，能夠有正確的環境參數，如:exporter endpoint (OTEL Collector 服務）的位置，以及traceidratio的取樣比率 0.25等。Propagators主要當有產生所指定的軌跡Header時，(如：tracecontext (W3C)，或是b3(Zipkin)，Baggage的軌跡相關描述，必須被[保存並往後傳遞](https://opentelemetry.io/docs/specs/otel/context/api-propagators/#propagators-distribution)。

```yml
cat << EOF | kubectl apply -f -
apiVersion: opentelemetry.io/v1alpha1
kind: Instrumentation
metadata:
  name: my-instrumentation
spec:
  exporter:
    endpoint: http://otel-collector.otel-collector.svc.cluster.local:4317
  propagators:
    - tracecontext
    - baggage
    - b3
  sampler:
    type: parentbased_traceidratio
    argument: "0.25"

  python:
    env:
    # Needed until https://github.com/open-telemetry/opentelemetry-python-contrib/issues/1361
    # is fixed
    - name: OTEL_METRICS_EXPORTER
      value: none
    # Python autoinstrumentation only supports OTLP/HTTP which the collector runs on port 4318,
    # see https://github.com/open-telemetry/opentelemetry-operator/issues/924
    - name: OTEL_EXPORTER_OTLP_ENDPOINT
      value: http://otel-collector.otel-collector.svc.cluster.local:4318
EOF
```

## 部署測試用服務

Create Artifact Docker Registry:
我們建置一個 my-repo 的Docker registry提供給Cloud run使用。我們同時設定讓本機可以存取Artifact Docker Registry(容器鏡像庫）。

```sh
gcloud artifacts repositories create my-repo \
    --repository-format=docker \
    --location=asia-east1 \
    --async

gcloud auth configure-docker asia-east1-docker.pkg.dev
```

可以開一個新分頁，選擇Artifact Registry，查看剛剛我們通過CLI建置出來的my-repo鏡像庫。等等我們部署時會用到它，

## GuestBook back.py 的程式碼修改

這個Guestbook程式，具有frontend與backend兩塊，均包含在 src/檔案夾下。其中backend部分，主要負責API和與後端MongoDB溝通，而frontend主要是UI操作，通過使用者擊點留言，呼叫後端POST API。

我們首先針對backend 資料夾下的 back.py 與 requirements.txt 進行修改，為了引進prometheus的API的效能統計數值，因為我們使用的程式使用Flask框架，我們選擇引入：prometheus_flask_exporter，修改如下：

| Filename | Fix Content | 修改原因 |
| --- | --- | --- |
| `back.py` | 1. Import bleach下方，加上 `from prometheus_flask_exporter import PrometheusMetrics`. 2. `app = Flask(__name__)` 下方，加上 `metrics = PrometheusMetrics(app)` | 引入 prometheus metrics |
| `requirements.txt` | 新增 `prometheus_flask_exporter` 在檔案最後 | |

## GuestBook 開發+部署的設定碼修改

主要的CI設定檔，在 frontend/ 和 backend/ 檔案夾內部的 Dockerfile, skaffold.yaml ，部署檔案則在各自 frontend/ 和backend檔案夾內的deployment.yaml。

請進行以下的置換，${PROJECT_ID}請更換為您專案的名稱 (e.g.: qwiklabs-gcp-00-bf7484a22018) :

1. 修改原因：鏡像位置，包含 skaffold.yaml 與 deployment.yaml

`${PROJECT_ID}` 替換成 `qwiklabs-gcp-01-0cda8821429a`

| Filename | Replace Location | Replace Content |
| --- | --- | --- |
| `src/frontend/skaffold.yaml` | build.artifacts.image | 由 `python-guestbook-frontend` 改為 `asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook-frontend` |
| `src/backend/skaffold.yaml` | build.artifacts.image | 由 `python-guestbook-backend` 改為 `asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook-backend` |
| `src/frontend/kubernetes-manifests/guestbook-frontend.deployment.yaml` | spec.template.spec.containers.image | 由 `python-guestbook-frontend` 改為 `asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook-frontend` |
| `src/backend/kubernetes-manifests/guestbook-backend.deployment.yaml` | spec.template.spec.containers.image | 由 `python-guestbook-backendend` 改為 `asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook` |

2. 修改原因：通過新增Annotation，將Auto-Instrumentation的程式碼通過sidecar container注入容器

| Filename | Replace Location | Replace Content |
| --- | --- | --- |
| `src/frontend/kubernetes-manifests/guestbook-frontend.deployment.yaml` | spec.template.metadata | 加上 "img 1" |
| `src/backend/kubernetes-manifests/guestbook-backend.deployment.yaml` | spec.template.metadata | 加上 "img 2" |

<img style="width:80%;" src="https://cdn.qwiklabs.com/GO8i8RM9YMSfhcqJP0xXVR6sDV0j9g%2Fj4xKfie2Pm3I%3D"></img>
<p align="center"><sub><sup>
  "img 1"
</sup></sub></p>

```yml
annotations:
  sidecar.opentelemetry.io/inject: "true"
  prometheus.io/scrape: "true"
  prometheus.io/path: "/metrics"
  prometheus.io/port: "8080"
  instrumentation.opentelemetry.io/inject-python: "true"
```

<img style="width:80%;" src="https://cdn.qwiklabs.com/LwLcLiV1ygVXYxmWmWdlbACm%2FNkck5AhEvhTVXBEkSE%3D">
<p align="center"><sub><sup>
  "img 2"
</sup></sub></p>

```yml
annotations: 
  sidecar.opentelemetry.io/inject: "true"
  instrumentation.opentelemetry.io/inject-python: "true"
```

3. 修改原因：基礎鏡像若為alpine-based，目前在Auto-Injection會有錯誤發生。

| Filename | Replace Location | Replace Content |
| --- | --- | --- |
| `src/frontend/Dockerfile` | 第一行 | `FROM python:3.11-alpine` 改為 `FROM python:3.11-slim` |
| `src/backend/Dockerfile` | 第一行 | `FROM python:3.11-alpine` 改為 `FROM python:3.11-slim` |

## Skaffold 打包容器並部署服務

由於Guestbook專案是由Cloud Code產生，裏面自然也繼承了Google對於CI/CD的堅持，通過 Skaffold 簡化整個容器開發流程，不用再通過 docker build, push 打包容器，也不再需要 kubectl 手動部署，所有的設定都濃縮在 skaffold.yaml 裡，有興趣的捧油可以參考 skaffold.yaml 的內容，如果想更了解，可以看 Skaffold 的網站

* [Build](https://skaffold.dev/docs/builders/)
* [Deploy](https://skaffold.dev/docs/deployers/)。

我們可以在 guestbook-1 檔案夾下，通過以下指令快速打包容器，並部署服務到GKE上：

```sh
cd ~/guestbook-1
skaffold build --file-output ./out.json && skaffold deploy --build-artifacts ./out.json

# 部署的過程中，可以留意以下訊息，可以了解 Auto-Instrumentation 是通過 init container 發動的。
Waiting for deployments to stabilize...
 - deployment/python-guestbook-frontend: waiting for init container opentelemetry-auto-instrumentation to start
```

* Response 2024-10-24: 有時候執行一次會失敗, 再執行一次就好

```sh
kubectl get ns
NAME                            STATUS   AGE
anthos-identity-service         Active   80m
cert-manager                    Active   65m
default                         Active   81m
gke-managed-cim                 Active   80m
gke-managed-system              Active   80m
gmp-public                      Active   79m
gmp-system                      Active   79m
kube-node-lease                 Active   81m
kube-public                     Active   81m
kube-system                     Active   81m
opentelemetry-operator-system   Active   64m
otel-collector                  Active   64m

kubectl get all
NAME                                             READY   STATUS    RESTARTS   AGE
pod/python-guestbook-backend-f5797bf64-kcsf4     1/1     Running   0          6m31s
pod/python-guestbook-frontend-5798979774-78vfq   1/1     Running   0          6m36s
pod/python-guestbook-mongodb-57b9469ff5-twbp4    1/1     Running   0          6m31s

NAME                                TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)        AGE
service/kubernetes                  ClusterIP      192.168.32.1     <none>         443/TCP        77m
service/python-guestbook-backend    ClusterIP      192.168.32.144   <none>         8080/TCP       12m
service/python-guestbook-frontend   LoadBalancer   192.168.32.237   35.189.161.8   80:30881/TCP   13m
service/python-guestbook-mongodb    ClusterIP      192.168.32.196   <none>         27017/TCP      12m

NAME                                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/python-guestbook-backend    1/1     1            1           12m
deployment.apps/python-guestbook-frontend   1/1     1            1           13m
deployment.apps/python-guestbook-mongodb    1/1     1            1           12m

NAME                                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/python-guestbook-backend-86d4ccd755    0         0         0       8m42s
replicaset.apps/python-guestbook-backend-c4b6b56fb     0         0         0       12m
replicaset.apps/python-guestbook-backend-f5797bf64     1         1         1       6m31s
replicaset.apps/python-guestbook-frontend-5798979774   1         1         1       6m36s
replicaset.apps/python-guestbook-frontend-677564c4c    0         0         0       13m
replicaset.apps/python-guestbook-frontend-76fc8b67b5   0         0         0       13m
replicaset.apps/python-guestbook-frontend-7b45f984d5   0         0         0       8m46s
replicaset.apps/python-guestbook-mongodb-57b9469ff5    1         1         1       6m31s
replicaset.apps/python-guestbook-mongodb-777cbb8d5b    0         0         0       8m41s
replicaset.apps/python-guestbook-mongodb-bcb448b76     0         0         0       12m


# Tags used in deployment:
#  - asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook-frontend -> asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook-frontend:latest@sha256:4f60fcf58e57b8d46054b291eec2f2afc92500b9c2db753e800ddbeb4789b14a
#  - asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook-backend -> asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/python-guestbook-backend:latest@sha256:2230b1786c7f68242b3ae82dac07993aca6e7395a74ddffbfa6daf76540658af
# Starting deploy...
#  - deployment.apps/python-guestbook-frontend configured
#  - service/python-guestbook-frontend configured
# Waiting for deployments to stabilize...
#  - deployment/python-guestbook-frontend is ready.
# Deployments stabilized in 3.273 seconds
#  - deployment.apps/python-guestbook-backend configured
#  - service/python-guestbook-backend configured
#  - deployment.apps/python-guestbook-mongodb configured
#  - service/python-guestbook-mongodb configured
# Waiting for deployments to stabilize...
#  - deployment/python-guestbook-mongodb is ready. [1/2 deployment(s) still pending]
#  - deployment/python-guestbook-backend: waiting for init container init-db-ready to start
#     - pod/python-guestbook-backend-86d4ccd755-gghwc: waiting for init container init-db-ready to start
#  - deployment/python-guestbook-backend is ready.
# Deployments stabilized in 18.656 seconds
```

## 製造 Traffic

我們可以連到Guestbook網站，進行幾個留言測試，Guestbook網站IP查詢可以使用以下命令：

```sh
kubectl get svc -l tier=frontend -o jsonpath='{.items[0].status.loadBalancer.ingress[0].ip}'; echo
# 35.189.161.8
=> http://35.189.161.8/
# 不知道為什麼無痕視窗裡連不到, 一般的可以
```

進入Guestbook後，請多輸入幾筆留言，因為目前我們的Trace軌跡紀錄是以25%進行設定(四個軌跡紀錄一條）。

動腦題 - 試試將Trace紀錄頻率為100%

Answer:

```yml
argument: "0.25"
=> argument: "1"
```

<img style="width:80%;" src="https://cdn.qwiklabs.com/sDTbkQYctZ5fTKSrgynqFqyo9ByNwSgRMuup8W1ioBk%3D">
<p align="center"><sub><sup>
  動腦題 - 試試將Trace紀錄頻率為100%
</sup></sub></p>

## 壓測 (Optional)

如果想看到比較多的軌跡以及Metrics，用手動留言應該是很痛苦的。這裡提供一個壓測工具Locust的快速教學，特別針對Cloud Shell的使用者，我們主要依照[GCP建議的分散式測試](https://cloud.google.com/architecture/distributed-load-testing-using-gke)來實作這一段：

### 下載分散式測試的Git專案

將專案複製(Clone)到guestbook-1檔案夾下:

```sh
cd ~/guestbook-1
git clone https://github.com/GoogleCloudPlatform/distributed-load-testing-using-kubernetes.git
```

### 修改task.py

在Cloud Shell IDE裡，我們找到 `tasks.py` ，並以下方的測試腳本取代原本的內容：

```python
from locust import HttpUser, task, between, events
import random

class QuickstartUser(HttpUser):
    wait_time = between(1, 5)

    @task(1)
    def get(self):
        self.client.get("/")
    @task(1)
    def titles(self):
        num = random.randint(1, 5)
        self.client.post("/post", data={"name": "sweet heart", "message": f"test message {num}"})
```

### 修改kubernetes-config下的模板

由於我們的專案與Git的稍許不同，我們需要先針對原始的範本（template）檔案進行兩個修改。

首先找到 `distributed-load-testing-using-kubernetes/kubernetes-config/` 目錄，修改：

1. `locust-master-service.yaml.tpl` 中：移除

```yml
#移除以下的兩行，將原本的Internal Balancer部署為External LB
  annotations:
    networking.gke.io/load-balancer-type: "Internal"
```

2. 底下兩個檔案 `locust-worker-controller.yaml.tpl` 與 `locust-master-controller.yaml.tpl` 中：

將 `value: https://${SAMPLE_APP_TARGET}` 改為 `value: ${SAMPLE_APP_TARGET}`

### 產生部署檔案，並通過skaffold部署

接下來，我們來產生部署Locust測試用的k8s-manifests的檔案。

將以下的執行檔，進行變數更換後，新增到 `distributed-load-testing-using-kubernetes/docker-image` 目錄下，命名為 `gen-locust-k8s-manifests.sh`

```sh
#!/bin/bash
export LOCUST_IMAGE_NAME=locust-tasks
export LOCUST_IMAGE_TAG=latest
export GKE_CLUSTER=gke-lt-cluster
export PROJECT="qwiklabs-gcp-01-0cda8821429a"
export AR_REPO=my-repo
export REGION=asia-east1
export SAMPLE_APP_TARGET="http://python-guestbook-frontend.default.svc"


mkdir -p k8s-manifests/
envsubst < ../kubernetes-config/locust-master-controller.yaml.tpl > k8s-manifests/master-controller.yaml
envsubst < ../kubernetes-config/locust-worker-controller.yaml.tpl > k8s-manifests/worker-controller.yaml
envsubst < ../kubernetes-config/locust-master-service.yaml.tpl > k8s-manifests/master-service.yaml
```

我們在Terminal中，切換到 `distributed-load-testing-using-kubernetes/docker-image` 目錄下，使用 `bash gen-locust-k8s-manifests.sh` 我們就在 `k8s-manifests` 目錄產生好所需的部署檔案。

```sh
cd ~/guestbook-1/distributed-load-testing-using-kubernetes/docker-image
bash gen-locust-k8s-manifests.sh

ls -lah k8s-manifests
# total 20K
# drwxrwxr-x 2 student_03_c40dfb54bf6e student_03_c40dfb54bf6e 4.0K Oct 24 01:59 .
# drwxrwxr-x 5 student_03_c40dfb54bf6e student_03_c40dfb54bf6e 4.0K Oct 24 01:59 ..
# -rw-rw-r-- 1 student_03_c40dfb54bf6e student_03_c40dfb54bf6e 1.6K Oct 24 01:59 master-controller.yaml
# -rw-rw-r-- 1 student_03_c40dfb54bf6e student_03_c40dfb54bf6e 1.3K Oct 24 01:59 master-service.yaml
# -rw-rw-r-- 1 student_03_c40dfb54bf6e student_03_c40dfb54bf6e 1.3K Oct 24 01:59 worker-controller.yaml
```

這時，按下 skaffold init，並在選擇中按下Yes，我們就可以得到完整的部署程式skaffold.yaml，最後使用前面學到的大絕招：

```sh
skaffold init
# y
# apiVersion: skaffold/v4beta11
# kind: Config
# metadata:
#   name: docker-image
# build:
#   artifacts:
#     - image: asia-east1-docker.pkg.dev/qwiklabs-gcp-01-0cda8821429a/my-repo/locust-tasks
#       docker:
#         dockerfile: Dockerfile
# manifests:
#   rawYaml:
#     - k8s-manifests/master-controller.yaml
#     - k8s-manifests/master-service.yaml
#     - k8s-manifests/worker-controller.yaml

skaffold build --file-output ./out.json && skaffold deploy --build-artifacts ./out.json
```

### 檢視Locust的壓測UI

skaffold deploy結束後，我們應該可以看到 locust-master 跟5台 locust-slave pods 都成功在 default namespace 被部署出來。這時，我們尋找`service/locust-master-web` 的 `EXTERNAL-IP` 位置（下圖為例是 35.234.5.131）

```sh
kubectl get svc,pods

NAME                                TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)             AGE
service/kubernetes                  ClusterIP      192.168.32.1     <none>         443/TCP             109m
service/locust-master               ClusterIP      192.168.32.209   <none>         5557/TCP,5558/TCP   66s
service/locust-master-web           LoadBalancer   192.168.32.94    35.234.5.131   8089:31909/TCP      65s
service/python-guestbook-backend    ClusterIP      192.168.32.144   <none>         8080/TCP            44m
service/python-guestbook-frontend   LoadBalancer   192.168.32.237   35.189.161.8   80:30881/TCP        45m
service/python-guestbook-mongodb    ClusterIP      192.168.32.196   <none>         27017/TCP           44m

NAME                                             READY   STATUS    RESTARTS   AGE
pod/locust-master-5bf5779498-nr45b               1/1     Running   0          65s
pod/locust-worker-5c68d58f49-7cnzk               1/1     Running   0          65s
pod/locust-worker-5c68d58f49-f47mh               1/1     Running   0          65s
pod/locust-worker-5c68d58f49-gx46w               1/1     Running   0          65s
pod/locust-worker-5c68d58f49-kq525               1/1     Running   0          65s
pod/locust-worker-5c68d58f49-l2ftp               1/1     Running   0          65s
pod/python-guestbook-backend-f5797bf64-kcsf4     1/1     Running   0          37m
pod/python-guestbook-frontend-5798979774-78vfq   1/1     Running   0          38m
pod/python-guestbook-mongodb-57b9469ff5-twbp4    1/1     Running   0          37m
```

打開網站連到 <http://35.234.5.131:8089> 我們將壓測 Number of users 改為 100, Spawn rate改為 5 按下Start swarming

<img style="width:80%;" src="https://cdn.qwiklabs.com/s1Dqj1WZA5VhLGDLFT4BQ0I%2BIpfS7hMbWdoAr5B1R9E%3D">

我們可以看到壓測開始發生，同時壓測的負載均勻的分散到各個 worker 節點上。

<img style="width:80%;" src="https://cdn.qwiklabs.com/rhy0he8RvdjeoATLW%2B8etvmleRKKfUp0iLSxQ9Jz8UQ%3D">

## 檢視監控結果

在Cloud Console，選取 [Cloud Trace的頁面](https://console.cloud.google.com/traces/list)，我們會先看到上方有一些小點 (1)，每個點都是被紀錄的呼叫軌跡，值得一提的是，我們是一行程式都沒有修正，就可以取得這個資訊。

點開小點之後，我們可以看到呼叫的軌跡，其中我們特別選擇 `guestbook.insert` 這一條，因為這條表示的是插入 MongoDB 所需的時間。相較於 istio side-car 的 Trace 軌跡，使用 OpenTelemetry，更強化了對『非』Restful 後端的支持，

<img style="width:80%;" src="https://cdn.qwiklabs.com/XXdPs3VA0Mfc941Ojg2K%2Bzyh63NGUNa1t7C%2Ffm%2BpmjA%3D">

我們可以先進入 `backend-guestbook` 的 Pod 裡，通過 `apt update && apt-get install -y curl`， 再通過

curl 8080 port 的 /metrics subpath，了解目前 prometheus-flask-exporter 提供的相關參數(如下）：主要包含 python garbage collector, process_cpu等運算資源的狀況，以及flask_http_request_duration的histogram 以及flask_http_request_total 針對不同status code (e.g. 201, 403, 415等）的分項統計。

```sh
kubectl exec -it pod/python-guestbook-backend-f5797bf64-kcsf4 -- apt update && sudo apt-get install -y curl

kubectl exec -it pod/python-guestbook-backend-f5797bf64-kcsf4 -- curl localhost:8080/metrics
# error: Internal error occurred: Internal error occurred: error executing command in container: failed to exec in container: failed to start exec "de2767b1591bf31152cf2e0aff32436233db0a7a63b640fb874170f7c6c3b21b": OCI runtime exec failed: exec failed: unable to start container process: exec: "curl": executable file not found in $PATH: unknown

curl localhost:8080/metrics

# HELP python_gc_objects_collected_total Objects collected during gc
# TYPE python_gc_objects_collected_total counter
python_gc_objects_collected_total{generation="0"} 86241.0
python_gc_objects_collected_total{generation="1"} 9378.0
python_gc_objects_collected_total{generation="2"} 495.0
# HELP python_gc_objects_uncollectable_total Uncollectable objects found during GC
# TYPE python_gc_objects_uncollectable_total counter
python_gc_objects_uncollectable_total{generation="0"} 0.0
python_gc_objects_uncollectable_total{generation="1"} 0.0
python_gc_objects_uncollectable_total{generation="2"} 0.0
# HELP python_gc_collections_total Number of times this generation was collected
# TYPE python_gc_collections_total counter
python_gc_collections_total{generation="0"} 536.0
python_gc_collections_total{generation="1"} 48.0
python_gc_collections_total{generation="2"} 2.0
# HELP python_info Python platform information
# TYPE python_info gauge
python_info{implementation="CPython",major="3",minor="11",patchlevel="6",version="3.11.6"} 1.0
# HELP process_virtual_memory_bytes Virtual memory size in bytes.
# TYPE process_virtual_memory_bytes gauge
process_virtual_memory_bytes 5.24079104e+08
# HELP process_resident_memory_bytes Resident memory size in bytes.
# TYPE process_resident_memory_bytes gauge
process_resident_memory_bytes 6.1812736e+07
# HELP process_start_time_seconds Start time of the process since unix epoch in seconds.
# TYPE process_start_time_seconds gauge
process_start_time_seconds 1.6964357322e+09
# HELP process_cpu_seconds_total Total user and system CPU time spent in seconds.
# TYPE process_cpu_seconds_total counter
process_cpu_seconds_total 13.49
# HELP process_open_fds Number of open file descriptors.
# TYPE process_open_fds gauge
process_open_fds 11.0
# HELP process_max_fds Maximum number of open file descriptors.
# TYPE process_max_fds gauge
process_max_fds 1.048576e+06
# HELP flask_exporter_info Information about the Prometheus Flask exporter
# TYPE flask_exporter_info gauge
flask_exporter_info{version="0.22.4"} 1.0
# HELP flask_http_request_duration_seconds Flask HTTP request duration in seconds
# TYPE flask_http_request_duration_seconds histogram
flask_http_request_duration_seconds_bucket{le="0.005",method="POST",path="/messages",status="201"} 597.0
flask_http_request_duration_seconds_bucket{le="0.01",method="POST",path="/messages",status="201"} 599.0
flask_http_request_duration_seconds_bucket{le="0.025",method="POST",path="/messages",status="201"} 599.0
flask_http_request_duration_seconds_bucket{le="0.05",method="POST",path="/messages",status="201"} 599.0
flask_http_request_duration_seconds_bucket{le="0.075",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="0.1",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="0.25",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="0.5",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="0.75",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="1.0",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="2.5",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="5.0",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="7.5",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="10.0",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_bucket{le="+Inf",method="POST",path="/messages",status="201"} 600.0
flask_http_request_duration_seconds_count{method="POST",path="/messages",status="201"} 600.0# HELP flask_http_request_duration_seconds_created Flask HTTP request duration in seconds
# HELP flask_http_request_total Total number of HTTP requests
# TYPE flask_http_request_total counter
flask_http_request_total{method="POST",status="201"} 600.0
flask_http_request_total{method="GET",status="201"} 1415.0
flask_http_request_total{method="POST",status="404"} 34.0
flask_http_request_total{method="POST",status="415"} 2.0
# HELP flask_http_request_created Total number of HTTP requests
# TYPE flask_http_request_created gauge
flask_http_request_created{method="POST",status="201"} 1.696435753173088e+09
flask_http_request_created{method="GET",status="201"} 1.6964357532112405e+09
flask_http_request_created{method="POST",status="404"} 1.6964396226003044e+09
flask_http_request_created{method="POST",status="415"} 1.696439633466002e+09
# HELP flask_http_request_exceptions_total Total number of HTTP requests which resulted in an exception
# TYPE flask_http_request_exceptions_total counter
```

接下來我們點選[Monitoring頁面](https://console.cloud.google.com/monitoring/metrics-explorer)，依照上述的metrics輸出，我們用關鍵字 flask快速找到相關統計，已經被收容到Google Managed Prometheus內。

<img style="width:80%;" src="https://cdn.qwiklabs.com/jQ6Zzu%2F%2FS7P6k65GN76xssP2%2FzQUqsLO58MB590mqgA%3D">

我們也可以通過UI 在GroupBy的地方，針對不同的Status (error code), tier, method等，進行相關的統計。

<img style="width:80%;" src="https://cdn.qwiklabs.com/NZ9Tq9jlLFtIC%2FsMbRndrXv7pQWikCBTTW7x9UZi1Gg%3D">

這個OpenTelemetry的Lab，希望讓你感受到OpenTelemetry的威力。在不需要任何額外手動添加程式下，我們得到了完整的Trace軌跡，讓開發者可以更容易的找到連線之間的bottleneck，相較於另一類的無侵入式監控工具：Istio-Proxy，OpenTelemetry對非Restful後台，有較好的支援性。同時，通過Proemtheus-Flask-Exporter的函式庫，我們可以通過新增兩行程式碼，就可以得到完整的http連線統計，這些資料都妥善的儲存在GCP的Managed Service中，免除了存儲規劃，或是軟體升級等維運需要。

### 2024-10-24 Issue

* curl 安裝了但是 curl 不出來
* Metrics 搜尋不到 flask: 要搜 prometheus > python

```sh
kubectl exec -it pod/python-guestbook-backend-f5797bf64-kcsf4
apt update && sudo apt-get install -y curl

# 直接這樣很容易 $PATH 有問題: kubectl exec -it pod/python-guestbook-backend-f5797bf64-kcsf4 -- /bin/bash -c apt update && sudo apt-get install -y curl
Defaulted container "backend" out of: backend, init-db-ready (init), opentelemetry-auto-instrumentation-python (init)
Hit:1 http://deb.debian.org/debian bookworm InRelease
Hit:2 http://deb.debian.org/debian bookworm-updates InRelease
Get:3 http://deb.debian.org/debian-security bookworm-security InRelease [48.0 kB]
Fetched 48.0 kB in 0s (123 kB/s)    
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
All packages are up to date.
********************************************************************************
You are running apt-get inside of Cloud Shell. Note that your Cloud Shell  
machine is ephemeral and no system-wide change will persist beyond session end. 

To suppress this warning, create an empty ~/.cloudshell/no-apt-get-warning file.
The command will automatically proceed in 5 seconds or on any key. 

Visit https://cloud.google.com/shell/help for more information.                 
********************************************************************************
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
curl is already the newest version (8.5.0-2ubuntu10.4).
0 upgraded, 0 newly installed, 0 to remove and 2 not upgraded.

kubectl exec -it pod/python-guestbook-backend-f5797bf64-kcsf4 -- echo $PATH
/opt/gradle/bin:/opt/maven/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/go/bin:/usr/local/node_packages/node_modules/.bin:/usr/local/rvm/bin:/google/go_appengine:/google/google_appengine:/home/student_03_c40dfb54bf6e/.gems/bin:/usr/local/rvm/bin:/home/student_03_c40dfb54bf6e/gopath/bin:/google/gopath/bin:/google/flutter/bin:/usr/local/nvm/versions/node/v20.18.0/bin:/usr/bin
```

## 結束Lab

關閉Lab，或是執行以下命令清除Lab

```sh
gcloud projects delete $PROJECT_ID
```
