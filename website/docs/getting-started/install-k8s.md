---
title: Quick Kubernetes Install
sidebar_position: 1
description: Discover and experiment with Tetragon in a Kubernetes environment
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Quick Kubernetes Install

## Create a Cluster

<Tabs>
<TabItem value="gke" label="GKE">

```bash
export NAME="$(whoami)-$RANDOM"
export ZONE="us-west2-a"
gcloud container clusters create "${NAME}" --zone ${ZONE} --num-nodes=1
gcloud container clusters get-credentials "${NAME}" --zone ${ZONE}
```

</TabItem>

<TabItem value="aks" label="AKS">

```bash
export NAME="$(whoami)-$RANDOM"
export AZURE_RESOURCE_GROUP="${NAME}-group"
az group create --name "${AZURE_RESOURCE_GROUP}" -l westus2
az aks create --resource-group "${AZURE_RESOURCE_GROUP}" --name "${NAME}"
az aks get-credentials --resource-group "${AZURE_RESOURCE_GROUP}" --name "${NAME}"
```

</TabItem>

<TabItem value="eks" label="EKS">

```bash
export NAME="$(whoami)-$RANDOM"
eksctl create cluster --name "${NAME}"
```

</TabItem>

<TabItem value="kind" label="Kind">

```bash
cat <<EOF > kind-config.yaml
apiVersion: kind.x-k8s.io/v1alpha4
kind: Cluster
nodes:
- role: control-plane
  extraMounts:
  - hostPath: /proc
    containerPath: /procHost
EOF

kind create cluster --config kind-config.yaml
```

</TabItem>
</Tabs>

## Deploy Tetragon

```bash
helm repo add cilium https://helm.cilium.io
helm repo update
helm install tetragon cilium/tetragon -n kube-system
kubectl rollout status -n kube-system ds/tetragon -w
```

## Deploy Demo Application

```bash
kubectl get pods
```

## What's Next

Check for execution events.
