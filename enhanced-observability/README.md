# Enhanced Observability: `/statusz` and `/flagz` Endpoints

## Overview

Kubernetes 1.32 introduces new HTTP endpoints — `/statusz` and `/flagz` — in core components (like the kubelet, controller manager, etc.). These provide real-time insights into health status and runtime configuration flags.

## Use Case

DevOps and SRE teams can now monitor component health and configuration more efficiently. These endpoints make it easier to audit settings, detect misconfigurations, and ensure runtime consistency during upgrades or debugging.

## Endpoint Breakdown

### 🔍 `/statusz`

- Reports the **health status** of the component.
- Example output: `ok` if the component is functioning properly.

### ⚙️ `/flagz`

- Lists **runtime flags and configuration values** for the component.
- Helps verify the active settings on running nodes or control-plane components.

## Usage

These endpoints are available when the relevant feature gates are enabled:

- `ComponentStatusz=true`
- `ComponentFlagz=true`

You can access the endpoints using:

```bash
curl http://<component-host>:<port>/statusz
curl http://<component-host>:<port>/flagz
```

## Notes

- Requires Kubernetes components to be run with these feature gates enabled.
- Works best in **self-managed clusters** or **custom deployments**.

## Summary

- Improves real-time observability and debuggability.
- Helpful for upgrades, audits, and incident response.
- No YAML manifests required — feature is built into control-plane components.

## Manifest

- None required (feature is built-in).
