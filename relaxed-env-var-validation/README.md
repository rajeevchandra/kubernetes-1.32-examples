# Relaxed Environment Variable Validation

## Overview

Kubernetes 1.32 relaxes restrictions on environment variable names, allowing a broader set of characters — as long as they do not include the equals sign (`=`).

## Use Case

Some applications (e.g., legacy .NET apps or systems with machine-generated environment keys) rely on non-standard env var names like `MY_VAR.NAME`. These used to be invalid but are now allowed thanks to this change.

## Breakdown of `env-var-pod.yaml`

### 🧪 Sample Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: env-var-pod
spec:
  containers:
    - name: app
      image: your-app-image
      env:
        - name: "MY_VAR.NAME"
          value: "example"
```

- Defines a pod with an environment variable named `MY_VAR.NAME`.
- Would previously be rejected; now it’s allowed.

## Notes

- The only disallowed character in env var names is `=`.
- You must enable the `RelaxedEnvironmentVariableValidation` feature gate on the kubelet.

## Summary

- Adds compatibility for apps that use dot-separated or hyphenated env vars.
- Reduces config errors in platform migrations (especially .NET apps).
- Improves developer experience with fewer manual workarounds.

## Manifest

- `env-var-pod.yaml`
