# private-service-access

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] private-service-access`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree private-service-access`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init private-service-access
kpt live apply private-service-access --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
