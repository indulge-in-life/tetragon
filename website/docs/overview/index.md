---
title: Overview
sidebar_position: 1
description: Discover Cilium Tetragon and its capabilities
---

# Overview

Cilium Tetragon enables powerful realtime, eBPF-based security observability and runtime enforcement.

Tetragon can detect and react to:

- Process execution events
- System call activity
- Network activity
- File access activity

When used in Kubernetes, Tetragon understands Kubernetes resources such as:

- Namespaces
- Pods
- Workloads

## Functionality Overview

### eBPF Real-Time

Tetragon applies policy and filtering directly in the Linux kernel using eBPF.

### eBPF Flexibility

Tetragon can hook into kernel functions and apply custom tracing policies.

### eBPF Kernel Awareness

Tetragon combines kernel state with Kubernetes awareness to provide powerful security observability and enforcement.

## What's Next

- Getting Started
- Concepts
- Runtime Enforcement