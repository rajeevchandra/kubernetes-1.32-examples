# Dynamic Resource Allocation (DRA) Enhancements

## Overview

Dynamic Resource Allocation (DRA) allows Kubernetes to dynamically assign specialized hardware (e.g., GPUs) to workloads at scheduling time.

## Use Case

A financial institution runs machine learning models requiring multiple GPUs with at least 16GB memory. With DRA, the pods request GPUs using a claim template, and Kubernetes schedules them on appropriate GPU-enabled nodes dynamically.

## Breakdown of `gpu-pod.yaml`

### 🔧 ResourceClaimTemplate

```yaml
apiVersion: resource.k8s.io/v1alpha2
kind: ResourceClaimTemplate
metadata:
  name: gpu-claim-template
spec:
  metadata:
    labels:
      resource: nvidia-gpu
  spec:
    resourceClassName: nvidia.com/gpu
```

- Creates a template for GPU resource claims.
- Uses resource class `nvidia.com/gpu` (typically provided by NVIDIA device plugin).

### 🚀 Pod Definition

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: gpu-pod
spec:
  resourceClaims:
    - name: gpu
      source:
        resourceClaimTemplateName: gpu-claim-template
```

- Pod requests a resource claim based on the `gpu-claim-template`.

```yaml
  containers:
    - name: ml-trainer
      image: your-ml-image
      command: ["python", "train.py"]
      resources:
        limits:
          nvidia.com/gpu: 1
```

- Runs a container that requests 1 GPU.
- Starts a training job using `train.py`.

## Summary

- DRA simplifies scheduling workloads with specialized resource needs.
- Reduces coupling to node-specific configurations.
- Essential for AI/ML and GPU-intensive tasks.

## Manifests

- `resource-claim-template.yaml`
- `gpu-pod.yaml`
