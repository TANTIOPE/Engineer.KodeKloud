# Task

The Nautilus DevOps team is planning to deploy some microservices on the `Kubernetes` platform. The team has already set up a `Kubernetes` cluster and now they want to set up some namespaces, deployments, etc. Based on the current requirements, the team has shared some details as below:

- Create a namespace named `dev` and deploy a POD within it.
- Name the pod `dev-nginx-pod` and use the `nginx` image with the latest tag. Ensure to specify the tag as `nginx:latest`.

**Note:** The `kubectl` utility on `jump_host` is configured to operate with the Kubernetes cluster.

# Steps and Solution

1. **Create the Namespace**:

    Use the following `kubectl` command to create a namespace named `dev`:

    ```bash
    kubectl create namespace dev
    ```

2. **Deploy the Pod**:

    Create a `Pod` in the `dev` namespace using the `nginx:latest` image. Use the following `kubectl` command:

    ```bash
    kubectl run dev-nginx-pod --image=nginx:latest --namespace=dev
    ```

3. **Verify the Pod**:

    Check the status of the pod to ensure it was created successfully:

    ```bash
    kubectl get pods --namespace=dev
    ```

    To see more details about the pod:

    ```bash
    kubectl describe pod dev-nginx-pod --namespace=dev
    ```

    ![image](https://github.com/user-attachments/assets/66a11f84-75d1-4634-b24d-ec768d9787f9)
