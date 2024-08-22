# Task

Earlier today, the Nautilus DevOps team deployed a new release for an application. However, a customer has reported a bug related to this recent release. Consequently, the team aims to revert to the previous version.

- There exists a deployment named `nginx-deployment`; initiate a rollback to the previous revision.

**Note:** The `kubectl` utility on `jump_host` is configured to interact with the Kubernetes cluster.

# Steps and Solution

1. **Initiate the Rollback**:

    To revert the `nginx-deployment` to the previous revision, use the following `kubectl` command:

    ```bash
    kubectl rollout undo deployment/nginx-deployment
    ```

    This command rolls back the `nginx-deployment` to its previous state.

2. **Monitor the Rollback**:

    After initiating the rollback, monitor its progress to ensure it completes successfully:

    ```bash
    kubectl rollout status deployment/nginx-deployment
    ```

    This will display the status of the rollback, confirming that all pods are reverted to the previous version.

3. **Verify the Rollback**:

    Verify that the deployment has reverted to the previous revision:

    ```bash
    kubectl describe deployment nginx-deployment | grep "Image"
    ```

    This command helps ensure that the image used in the deployment has been rolled back to the previous version.

4. **Check the Pod Status**:

    After the rollback, check that all pods are running correctly:

    ```bash
    kubectl get pods
    ```
    ![image](https://github.com/user-attachments/assets/c831ffb8-f3dc-415b-8e50-1790cd3333e9)

