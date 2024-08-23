# Task

An application deployed on the Kubernetes cluster requires an update with new features developed by the Nautilus application development team. The existing setup includes a deployment named `nginx-deployment` and a service named `nginx-service`. The following changes are required:

1. **Modify the Service NodePort** from `30008` to `32165`.
2. **Change the Replicas Count** from `1` to `5`.
3. **Update the Image** from `nginx:1.17` to `nginx:latest`.

**Note:** The `kubectl` utility on `jump_host` is configured to operate with the Kubernetes cluster.

# Explanation

This task involves updating both the Kubernetes `Service` and `Deployment`. The `Service` needs its `NodePort` updated to a new port. The `Deployment` needs to be scaled up to increase the number of replicas and updated to use a new container image version.

# Steps and Solution

1. **Check the Current Configuration:**

    Verify the current settings for both the `Service` and `Deployment`:

    ```bash
    kubectl describe service nginx-service
    kubectl describe deploy nginx-deployment
    ```
    ![image](https://github.com/user-attachments/assets/7dc3bcd3-d760-4e3f-a0e6-6976850b09ab)


2. **Edit the Service Configuration:**

    Modify the `nginx-service` to update the `NodePort` from `30008` to `32165`. Use `kubectl edit` to directly edit the service configuration:

    ```bash
    kubectl edit service nginx-service
    ```

    - Locate the `nodePort` field in the `spec.ports` section and change its value to `32165`.
    - Save and exit the editor.

3. **Edit the Deployment Configuration:**

    Update the `nginx-deployment` to change the replicas count from `1` to `5` and the image to `nginx:latest`. Use `kubectl edit` to directly edit the deployment configuration:

    ```bash
    kubectl edit deploy nginx-deployment
    ```

    - Locate the `spec.replicas` field and change its value to `5`.
    - Locate the `spec.template.spec.containers.image` field and update the image to `nginx:latest`.
    - Save and exit the editor.
      
    ![image](https://github.com/user-attachments/assets/08bb1655-8c8a-476b-b370-681044daa550)

4. **Verify the Updates:**

    After making the changes, check that the updates have been applied correctly. Use `kubectl get all -o wide` to see the current state of all resources:

    ```bash
    kubectl get all -o wide
    ```

    - Verify that the number of replicas for the deployment is `5`.
    - Confirm that the image for the container is `nginx:latest`.
    - Ensure that the service is using the updated `NodePort`.

    ![image](https://github.com/user-attachments/assets/4f3edc4c-99d9-4cde-b2e1-d7691fb0ba56)
