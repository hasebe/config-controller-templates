# cms-db

## Description
sample description

## Usage

### Fetch the package
`kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] cms-db`
Details: https://kpt.dev/reference/cli/pkg/get/

### View package content
`kpt pkg tree cms-db`
Details: https://kpt.dev/reference/cli/pkg/tree/

### Apply the package
```
kpt live init cms-db
kpt live apply cms-db --reconcile-timeout=2m --output=table
```
Details: https://kpt.dev/reference/cli/live/
