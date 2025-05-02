# Graceful Shutdown for Windows Nodes

## Overview

Kubernetes 1.32 introduces improved support for gracefully terminating Windows-based pods. This ensures processes have time to clean up or shut down properly before the pod is forcefully killed.

## Use Case

Enterprise workloads running Windows containers—such as .NET Framework applications or background jobs—need time to perform cleanup or save state before being terminated. This is critical for maintaining data integrity and operational reliability.

## Breakdown of `windows-pod.yaml`

### 📦 Pod: `windows-app`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: windows-app
```

- Creates a single pod named `windows-app`.

### 🪟 Windows Node Scheduling

```yaml
nodeSelector:
  kubernetes.io/os: windows
```

- Ensures the pod is scheduled **only on Windows nodes**.
- The container image must be Windows-compatible.

### ⏱ Graceful Termination Setting

```yaml
terminationGracePeriodSeconds: 60
```

- Gives the pod **60 seconds** to exit gracefully when it's terminated.
- Prevents immediate force-kill, allowing cleanup logic to execute.

### 🖥 Container Command

```yaml
containers:
  - name: app
    image: your-windows-app-image
    command: ["powershell", "-Command", "Start-Sleep -Seconds 300"]
```

- Runs a PowerShell command to **simulate a long-running task**.
- You can safely test how termination is handled mid-execution.

## Summary

- Enables graceful termination of Windows-based workloads.
- Great for applications that need a cleanup window.
- Easy to test using `kubectl delete pod windows-app`.

## Manifest

- `windows-pod.yaml`
