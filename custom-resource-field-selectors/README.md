# Custom Resource Field Selectors

## Overview

Starting in Kubernetes 1.32, field selectors are now supported for **Custom Resources**. This means you can now filter custom resources based on specific fields — just like you already do with built-in Kubernetes resources.

## Use Case

Operators or developers managing custom CRDs (like `MyResource`, `BackupJob`, or `DataPipeline`) can now **query specific subsets** using `--field-selector`. This is especially useful for automation and scripting.

## Example Scenario

Let’s say you have a custom resource `BackupJob` with a `.status.phase` field. You want to fetch only those jobs in the `Running` state.

### ✅ Command

```bash
kubectl get backupjobs --field-selector=status.phase=Running
```

This will return only the CRs with status.phase = Running.

## Notes

- Works for all CRDs — no changes required to the CRD spec.
- Fields must exist and be populated in the CR's status or metadata.

## Summary

- Adds parity with built-in resources like Pods, Nodes.
- Enables more efficient CRD querying and scripting.
- Great for CI/CD, operators, and observability tools.

## Manifest

- None required (server-side enhancement).
