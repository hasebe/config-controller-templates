# kpttest

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] kpttest`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree kpttest`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init kpttest
kpt live apply kpttest --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
