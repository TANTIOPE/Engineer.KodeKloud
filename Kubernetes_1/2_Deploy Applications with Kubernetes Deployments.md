# Task

The Nautilus DevOps team is delving into `Kubernetes` for app management. One team member needs to create a deployment following these details:

- Create a deployment named `httpd` to deploy the application `httpd` using the image `httpd:latest` (ensure to specify the tag).

**Note:** The `kubectl` utility on `jump_host` is set up to interact with the Kubernetes cluster.

# Steps and Solution

1. **Create the Deployment**:

    Use the following `kubectl` command to create a deployment named `httpd` with the `httpd:latest` image:

    ```bash
    kubectl create deployment httpd --image=httpd:latest
    ```

2. **Verify the Deployment**:

    Check the status of the deployment to ensure it was created successfully:

    ```bash
    kubectl get deployments
    ```

    To see more details about the deployment:

    ```bash
    kubectl describe deployment httpd
    ```
