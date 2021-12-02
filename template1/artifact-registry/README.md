# artifact-registry

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] artifact-registry`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree artifact-registry`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init artifact-registry
kpt live apply artifact-registry --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
