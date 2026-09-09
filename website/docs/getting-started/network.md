---
title: Network Monitoring
sidebar_position: 5
description: Network access traces with Tetragon
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Network Monitoring

## Monitoring Kubernetes Network Access

First, capture the Pod CIDR:

```bash
export PODCIDR=$(kubectl get nodes -o jsonpath='{.items[*].spec.podCIDR}')
```

Capture the Service CIDR:

<Tabs>
<TabItem value="gke" label="GKE">

```bash
export SERVICECIDR=$(gcloud container clusters describe ${NAME} --zone ${ZONE} | awk '/servicesIpv4CidrBlock/ { print $2; }')
```

</TabItem>
<TabItem value="kind" label="Kind">

```bash
export SERVICECIDR=$(kubectl describe pod -n kube-system -l component=kube-apiserver | awk -F= '/--service-cluster-ip-range/ {print $2; }')
```

</TabItem>
<TabItem value="eks" label="EKS">

```bash
export SERVICECIDR=$(aws eks describe-cluster --name ${NAME} | jq -r '.cluster.kubernetesNetworkConfig.serviceIpv4Cidr')
```

</TabItem>
<TabItem value="aks" label="AKS">

```bash
export SERVICECIDR=$(az aks show --name ${NAME} --resource-group ${AZURE_RESOURCE_GROUP} | jq -r '.networkProfile.serviceCidr')
```

</TabItem>
</Tabs>

Apply the policy:

```bash
wget https://raw.githubusercontent.com/cilium/tetragon/main/examples/quickstart/network_egress_cluster.yaml
envsubst < network_egress_cluster.yaml | kubectl apply -f -
```

## Observe Events

```bash
kubectl exec -ti -n kube-system ds/tetragon -c tetragon -- tetra getevents -o compact --pods xwing --processes curl
```

Generate traffic:

```bash
kubectl exec -ti xwing -- bash -c 'curl https://ebpf.io/applications/#tetragon'
```

## Docker Example

```bash
export PODCIDR="127.0.0.1/32"
export SERVICECIDR="127.0.0.1/32"
```

```bash
docker exec -ti tetragon tetra getevents -o compact
```

## What's Next

Learn about enforcement policies and advanced concepts.
