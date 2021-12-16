# compute-engine

## Description
Compute Engine instances with Instance Group Manager.

## Usage

1. Fetch a template

   ```sh
   kpt pkg get https://github.com/hasebe/config-controller-templates/template2/compute-engine compute-engine
   ```

1. Move into the directory

   ```sh
   cd compute-engine/
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
