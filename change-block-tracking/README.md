# Change Block Tracking (CBT)

## Overview

Change Block Tracking (CBT) is a new alpha feature in Kubernetes 1.32 that enables more efficient snapshots by tracking only the blocks that have changed since the last snapshot.

## Use Case

In environments with large databases or file systems, taking full snapshots frequently is time-consuming and storage-intensive. CBT allows incremental snapshots by focusing only on modified data blocks, reducing snapshot size and backup time.

## Breakdown of `cbt-pvc.yaml`

### 💾 PersistentVolumeClaim with CBT

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cbt-pvc
  annotations:
    snapshot.storage.kubernetes.io/change-block-tracking: "true"
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 100Gi
  storageClassName: csi-cbt-enabled
```

- Creates a **100Gi PVC** with CBT enabled.
- The annotation tells the CSI driver to track block changes.
- `csi-cbt-enabled` must be a supported storage class that implements CBT.

## Notes

- The storage backend and CSI driver must support CBT.
- Ensure the `VolumeSnapshotDataSource` and `EnableCBT` feature gates are enabled.

## Summary

- Enables fast, storage-efficient incremental backups.
- Useful for production databases and large persistent volumes.
- Reduces downtime and improves disaster recovery speed.

## Manifest

- `cbt-pvc.yaml`
