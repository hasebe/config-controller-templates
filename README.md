# config-controller-templates

This repository hosts templates for config controller. All assets are work in progress.

All templates are intended to be deployed on [Config Controller](https://cloud.google.com/anthos-config-management/docs/concepts/config-controller-overview).

## Set up an environment

Follow the steps to deploy templates. The steps are tested on Cloud Shell.

### Set up Config Controller ([Ref.](https://cloud.google.com/anthos-config-management/docs/how-to/config-controller-setup#set_up))

1. Define environment variables

   Replace values to adopt your environment.

   ```sh
   export CONFIG_CONTROLLER_NAME=config-controller01
   export PROJECT_ID=project_id
   export TENANT_EMAIL=test@example.com
   ```

1. Enable required services

   ```sh
   gcloud services enable krmapihosting.googleapis.com \
     container.googleapis.com \
     cloudresourcemanager.googleapis.com
   ```

1. Create Config Controller

   ```sh
   gcloud anthos config controller create $CONFIG_CONTROLLER_NAME \
     --location=us-central1
   ```

1. Authenticate with the Config Controller cluster

   ```sh
   gcloud anthos config controller get-credentials $CONFIG_CONTROLLER_NAME \
     --location us-central1
   ```

1. Give Config Controller permission to manage Google Cloud resources

   ```sh
   export SA_EMAIL="$(kubectl get ConfigConnectorContext -n config-control \
     -o jsonpath='{.items[0].spec.googleServiceAccount}' 2> /dev/null)"
   gcloud projects add-iam-policy-binding "${PROJECT_ID}" \
     --member "serviceAccount:${SA_EMAIL}" \
     --role "roles/owner" \
     --project "${PROJECT_ID}"
   ```

### Set up a namespace to manage the project ([Ref.](https://cloud.google.com/anthos-config-management/docs/tutorials/project-namespace-blueprint))

1. Install the ResourceGroup CRD

   ```sh
   kpt live install-resource-group
   ```

1. Fetch the Project Namespace blueprint

   ```sh
   kpt pkg get \
     https://github.com/GoogleCloudPlatform/blueprints.git/catalog/project/kcc-namespace@main \
     $PROJECT_ID
   ```

1. Move into the directory

   ```sh
   cd $PROJECT_ID/
   ```

1. Configure the package by modifying the setters.yaml

   ```sh
   cat > setters.yaml << EOF
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: setters
   data:
     project-id: $PROJECT_ID
     management-project-id: $PROJECT_ID
     management-namespace: config-control
     projects-namespace: config-control
     networking-namespace: config-control
   EOF
   ```

1. Render the setter values into the templated resources

   ```sh
   kpt fn render
   ```

1. Configure tenant permissions

   ```sh
   cat > project-admin.yaml << EOF
   apiVersion: rbac.authorization.k8s.io/v1
   kind: RoleBinding
   metadata:
     name: project-admin
     namespace: $PROJECT_ID
   roleRef:
     kind: ClusterRole
     name: cnrm-admin
     apiGroup: rbac.authorization.k8s.io
   subjects:
   - kind: User
     name: $TENANT_EMAIL
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. Initialize the working directory with kpt, which creates a resource to track changes

   ```sh
   kpt live init --namespace config-control
   ```

1. Apply the resources

   ```sh
   kpt live apply
   ```

### Deploy a template

1. Fetch a template

   Specify the template number. Following command uses `template1` as a example.

   ```sh
   kpt pkg get https://github.com/hasebe/config-controller-templates/template1 template1
   ```

1. Move into the directory

   ```sh
   cd template1/
   ```

1. Update variables in `setters.yaml` on each directory to adjust your enviroment

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
