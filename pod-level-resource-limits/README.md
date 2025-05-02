# Pod-Level Resource Limits

## Overview

Kubernetes 1.32 introduces support for setting resource limits at the pod level, allowing multiple containers in a pod to share a collective resource quota.

## Use Case

In CI/CD pipelines or complex applications with multiple containers (e.g., sidecars), containers can dynamically share CPU and memory from a common pool, optimizing overall resource utilization and avoiding unnecessary throttling.

## Breakdown of `resource-pod.yaml`

### 🚀 Pod Spec with Shared Limits

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-shared-pod
spec:
  containers:
    - name: container-a
      image: your-app-image
    - name: container-b
      image: your-app-image
  resources:
    limits:
      cpu: "2"
      memory: "4Gi"
    requests:
      cpu: "1"
      memory: "2Gi"
```

- Defines a pod with two containers.
- Both containers share the same **total CPU and memory** limits.
- The system enforces limits at the pod level instead of per-container.

## Notes

- Ensure the `PodResources` feature gate is enabled.
- Useful for reducing over-provisioning and improving density.

## Summary

- Promotes better resource utilization across containers.
- Great for CI pipelines, logging sidecars, and proxy-based apps.

## Manifest

- `resource-pod.yaml`
