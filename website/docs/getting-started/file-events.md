---
title: File Access Monitoring
sidebar_position: 4
description: File access traces with Tetragon
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# File Access Monitoring

Tracing policies can be added to Tetragon through YAML configuration files that extend Tetragon's tracing capabilities.

## Apply the tracing policy

<Tabs>
<TabItem value="k8s-single" label="Kubernetes (single node)">

```bash
kubectl apply -f https://raw.githubusercontent.com/cilium/tetragon/main/examples/quickstart/file_monitoring.yaml
```

</TabItem>

<TabItem value="k8s-multi" label="Kubernetes (multiple nodes)">

```bash
kubectl apply -f https://raw.githubusercontent.com/cilium/tetragon/main/examples/quickstart/file_monitoring.yaml
```

</TabItem>

<TabItem value="docker" label="Docker">

```bash
wget https://raw.githubusercontent.com/cilium/tetragon/main/examples/quickstart/file_monitoring.yaml
```

</TabItem>
</Tabs>

## Observe Tetragon file access events

<Tabs>
<TabItem value="docker" label="Docker">

```bash
docker exec -ti tetragon tetra getevents -o compact
```

</TabItem>
</Tabs>

This file was converted from Hugo format. Replace any remaining Hugo references with Docusaurus links if needed.
