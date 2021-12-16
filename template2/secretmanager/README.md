# secretmanager

## Description
Secret Manager with a sample secret data.

## Usage

1. Fetch a template

   ```sh
   kpt pkg get https://github.com/hasebe/config-controller-templates/template2/secretmanager secretmanager
   ```

1. Move into the directory

   ```sh
   cd secretmanager/
   ```

1. Update variables in `setters.yaml` to adjust your enviroment

1. Initialize the working directory with kpt, which creates a resource to track changes

   ```sh
   kpt live init --namespace $PROJECT_ID
   ```

1. Render the setter values into the templated resources

   ```sh
   kpt fn render
   ```

1. Apply the resources

   ```sh
   kpt live apply --namespace $PROJECT_ID
   ```
