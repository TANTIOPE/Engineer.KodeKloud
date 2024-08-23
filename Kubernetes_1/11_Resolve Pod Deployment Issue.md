# Task

A junior DevOps team member encountered difficulties deploying a stack on the Kubernetes cluster. The pod fails to start, presenting errors. Let's troubleshoot and rectify the issue promptly.

1. **Pod Name:** `webserver`
2. **Containers:**
   - **Primary Container:** `nginx-container`, utilizing the `nginx:latest` image.
   - **Sidecar Container:** `sidecar-container`, using the `ubuntu:latest` image.

**Note:** The `kubectl` utility on `jump_host` is configured to interact with the Kubernetes cluster.

# Explanation

The task is to troubleshoot and fix issues with a pod that is failing to start. This involves identifying potential problems with the pod's configuration, the containers within it, and their interactions. This process includes checking pod status, container logs, and configuration details to ensure the pod becomes operational and the application is accessible.

# Steps and Solution

1. **Check the Pod Status:**

    First, check the status of the pod to understand why it's failing to start:

    ```bash
    kubectl get pods webserver
    ```

    - This command provides details about the pod status, including whether it's running, pending, or failed.

2. **Inspect Pod Events:**

    Review the pod's events for any errors or issues related to the pod's lifecycle:

    ```bash
    kubectl describe pod webserver
    ```

    - This command provides a detailed description of the pod, including events and conditions that might explain why the pod is failing to start.
   
    ![image](https://github.com/user-attachments/assets/356f5bf5-7d3a-466c-8d07-1d1d155acee5)
    ![image](https://github.com/user-attachments/assets/2a5d0f51-a86a-403f-9164-d940ac46648f)



4. **Check Container Logs:**

    Examine the logs of both containers to diagnose issues:

    ```bash
    # Check logs of the nginx-container
    kubectl logs webserver -c nginx-container

    # Check logs of the sidecar-container
    kubectl logs webserver -c sidecar-container
    ```

    - These commands show the logs for each container, which can reveal errors or issues encountered during their execution.

6. **Verify Container Configurations:**

    Ensure the containers are properly configured in the pod specification:

    ```bash
    kubectl get pod webserver -o yaml
    ```

    - This command outputs the pod's YAML configuration, allowing you to verify the correctness of container settings, image names, and other specifications.

6. **Fix Issues:**

    Based on the information gathered, make necessary adjustments to the pod's configuration or container settings in our case, edit the yaml configuration file and correct the image name : `nginx:latest`

    ```bash
    kubectl edit pod webserver
    ```

7. **Verify the Fix:**

    After making corrections, verify that the pod is running correctly and that the application is accessible:

    ```bash
    kubectl get pods webserver
    ```
    ![image](https://github.com/user-attachments/assets/4c1c44ba-8bb9-41be-806a-1c2548f2d703)

    - Check the pod status again to confirm that it is now running as expected.
