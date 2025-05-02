# Volume Group Snapshots (Beta)

## Overview

Volume Group Snapshots is a beta feature in Kubernetes 1.32 that allows you to create a crash-consistent snapshot across multiple PersistentVolumeClaims (PVCs) simultaneously.

## Use Case

A transactional application such as a database may span multiple PVCs for data and logs. To ensure consistency, you need to snapshot all of them together. Volume Group Snapshots solve this by creating a group snapshot of all matching volumes at the same time.

## Breakdown of `volume-group-snapshot.yaml`

### 📦 Group Snapshot Resource

```yaml
apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeGroupSnapshot
metadata:
  name: app-group-snapshot
spec:
  source:
    selector:
      matchLabels:
        app: multi-volume-app
  volumeSnapshotClassName: csi-snapshot-class
```

- Creates a **group snapshot** named `app-group-snapshot`.
- Targets all PVCs with the label `app: multi-volume-app`.
- Uses a `VolumeSnapshotClass` that must support group snapshotting.

## Notes

- Supported only by CSI drivers that implement the group snapshot feature.
- PVCs must exist and be bound to a pod or deployment using the matching label.

## Summary

- Ensures all volumes are snapshotted simultaneously with crash consistency.
- Critical for apps like PostgreSQL, MongoDB, or log-structured stores.
- Reduces manual scripting and orchestration for consistent backups.

## Manifest

- `volume-group-snapshot.yaml`
