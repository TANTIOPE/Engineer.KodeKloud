# Task

An application currently running on the `Kubernetes` cluster employs the `nginx` web server. The Nautilus application development team has introduced some recent changes that need deployment. They've crafted an image `nginx:1.19` with the latest updates.

- Execute a rolling update for the application, integrating the `nginx:1.19` image.
- The deployment is named `nginx-deployment`.
- Ensure all pods are operational post-update.

**Note:** The `kubectl` utility on `jump_host` is set up to operate with the Kubernetes cluster.

# Steps and Solution

1. **Execute the Rolling Update**:

    To update the `nginx-deployment` to use the new `nginx:1.19` image, use the following `kubectl` command:

    ```bash
    kubectl set image deployment/nginx-deployment nginx-container=nginx:1.19
    ```

    This command updates the image for the container named `nginx-container` within the `nginx-deployment` deployment.

2. **Monitor the Rolling Update**:

    Ensure that the rolling update progresses smoothly and that all pods are updated without downtime:

    ```bash
    kubectl rollout status deployment/nginx-deployment
    ```

    This command will display the status of the rolling update, ensuring all pods are updated and operational.

3. **Verify the Update**:

    After the update, verify that the deployment is using the correct image:

    ```bash
    kubectl get deployment nginx-deployment -o yaml | grep image
    ```

    You should see the updated image `nginx:1.19` in the output.

    Additionally, confirm that all pods are running and healthy:

    ```bash
    kubectl get pods
    ```
    ![image](https://github.com/user-attachments/assets/3509be2c-aba8-4cd8-bb15-1357f2022f6d)
