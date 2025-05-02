# Custom Resource Field Selectors

## Overview

Field selectors can now filter Custom Resource definitions.

## Use Case

Select only running custom resources using `status.phase=Running`.

## Example

```bash
kubectl get myresources --field-selector=status.phase=Running
```

No manifest required.
