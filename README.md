# Kubernetes 1.32: Real-World Use Cases & YAML Templates

This repository provides practical examples and YAML templates for the key features introduced in Kubernetes 1.32.

## Features Covered

1. [Dynamic Resource Allocation (DRA)](./dynamic-resource-allocation/)
2. [Node Feature Discovery (NFD)](./node-feature-discovery/)
3. [Auto-Removal of PVCs](./statefulset-pvc-auto-removal/)
4. [Graceful Shutdown for Windows Nodes](./graceful-shutdown-windows/)
5. [Change Block Tracking (CBT)](./change-block-tracking/)
6. [Volume Group Snapshots](./volume-group-snapshots/)
7. [Pod-Level Resource Limits](./pod-level-resource-limits/)
8. [Enhanced Observability](./enhanced-observability/)
9. [Custom Resource Field Selectors](./custom-resource-field-selectors/)
10. [Relaxed Environment Variable Validation](./relaxed-env-var-validation/)

## Getting Started

To apply any manifest:

```bash
kubectl apply -f path/to/file.yaml
```

> Kubernetes v1.32 or later is required.
