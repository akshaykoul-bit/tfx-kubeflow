## Chest X-ray pneumonia classification

The dataset has been downloaded from this Kaggle link - https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia

TL;DR - I am trying to classify chest xray images into 2 categories i.e. NORMAL and PNEUMONIA using CNN - Convolution neural networks

## Pipeline Flow (Local Deployment)

A kubernetes cluster was generated using [kind](https://kind.sigs.k8s.io/) and using [kubectl](https://kubernetes.io/docs/tasks/tools/), ml-pipeline-ui service was accessed.

The pipeline consists of 2 components:
- download_and_build_and_train_model component which downloads the data from kaggle, augments it and trains a CNN on it.
- eval_component which logs the evaluation metrics using the model and history artifacts from the previous component


