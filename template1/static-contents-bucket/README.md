# static-contents-bucket

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] static-contents-bucket`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree static-contents-bucket`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init static-contents-bucket
kpt live apply static-contents-bucket --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
