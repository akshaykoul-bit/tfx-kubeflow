## Chest X-ray pneumonia classification

The dataset has been downloaded from this Kaggle link - https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia

TL;DR - I am trying to classify chest xray images into 2 categories i.e. NORMAL and PNEUMONIA using CNN - Convolution neural networks

## Pipeline Flow (Local Deployment)

A kubernetes cluster was generated using [kind](https://kind.sigs.k8s.io/) and using [kubectl](https://kubernetes.io/docs/tasks/tools/), ml-pipeline-ui service was accessed.

The pipeline consists of 2 components:
- download_and_build_and_train_model component which downloads the data from kaggle, augments it and trains a CNN on it.
- eval_component which logs the evaluation metrics using the model and history artifacts from the previous component

Windows-
spin up kind on cmd, initiate pods using kubectl on powershell, port forward to ml-pipeline-ui, upload+run pipeline on ui, delete pods on powershell, delete kind cluster on cmd

```
kind create cluster
```

```
set PIPELINE_VERSION=1.7.0
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
kubectl wait --for condition=established --timeout=60s crd/applications.app.k8s.io
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-pns?ref=$PIPELINE_VERSION"

kubectl get deploy -n kubeflow

kubectl port-forward -n kubeflow svc/ml-pipeline-ui 8080:80
```

```
set PIPELINE_VERSION=1.7.0
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
kubectl wait --for condition=established --timeout=60s crd/applications.app.k8s.io
kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-pns?ref=$PIPELINE_VERSION"
```

```
set PIPELINE_VERSION=1.7.0
kubectl delete -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-pns?ref=$PIPELINE_VERSION"
kubectl delete -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
```

```
kind delete cluster
```
