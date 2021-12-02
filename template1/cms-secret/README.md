# cms-secret

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cms-secret`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cms-secret`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cms-secret
kpt live apply cms-secret --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
