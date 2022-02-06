## Multi-task recommender model using tensorflow recommenders

This is an implementation of a two tower recommender system (joint model) with both the stages ie. Retrieval and Ranking using kubeflow pipeline. (As per Tensorflow recommenders official documentation)

The retrieval stage is responsible for selecting an initial set of hundreds of candidates from all possible candidates. The ranking stage takes the outputs of the retrieval model and fine-tunes them to select the best possible handful of recommendations.

## Pipeline Flow (Local Deployment)

A kubernetes cluster was generated using [kind](https://kind.sigs.k8s.io/) and using [kubectl](https://kubernetes.io/docs/tasks/tools/), ml-pipeline-ui service was accessed.

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
