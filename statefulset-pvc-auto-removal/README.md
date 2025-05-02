# Auto-Removal of PVCs in StatefulSets

## Overview

StatefulSets now support automatic deletion of PersistentVolumeClaims (PVCs) when they are no longer in use.

## Use Case

A development team deploys ephemeral stateful workloads for testing. With auto-removal, PVCs associated with these StatefulSets are automatically deleted when no longer in use, simplifying storage management and preventing resource wastage.

## Breakdown of `statefulset.yaml`

### 📦 StatefulSet: `data-processor`

- Defines a StatefulSet named `data-processor`.
- Used for applications that need stable identities and persistent storage.

### 🔁 Replicas and Identity

- Creates 3 pods: `data-processor-0`, `data-processor-1`, `data-processor-2`.
- Connects through a headless service named `data-service`.

### 🔐 Retention Policy

```yaml
persistentVolumeClaimRetentionPolicy:
  whenDeleted: Delete
  whenScaled: Delete
```

- **Deletes PVCs** when pods are deleted or scaled down.
- A new feature in Kubernetes 1.32 to simplify storage cleanup.

### 📦 Pod Template

- Runs a container using `your-data-processor-image`.
- Mounts a volume at `/data`.

### 💾 Volume Claim Template

```yaml
volumeClaimTemplates:
  - metadata:
      name: data-storage
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 10Gi
```

- Creates separate PVCs per pod.
- Each PVC is named dynamically per pod identity.

## Summary

- 3 stateful pods are created, each with its own 10Gi volume.
- New retention policy ensures automatic cleanup of PVCs.
- Great for test environments and ephemeral stateful workloads.

## Manifest

- `statefulset.yaml`
