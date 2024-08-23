# Task

The Nautilus DevOps team is establishing a `ReplicationController` to deploy multiple pods for hosting applications that require a highly available infrastructure. Follow the specifications below to create the `ReplicationController`:

1. **Create a `ReplicationController`** using the `nginx` image, preferably with the latest tag (specify as `nginx:latest`), and name it `nginx-replicationcontroller`.

2. **Assign Labels**:
   - `app` as `nginx_app`
   - `type` as `front-end`

3. **Ensure**:
   - The container is named `nginx-container`
   - The replica count is set to `3`

4. **Verify** that all pods are in the running state post-deployment.

**Note:** The `kubectl` utility on `jump_host` is configured to operate with the Kubernetes cluster.

# Explanation

A `ReplicationController` in Kubernetes ensures that a specified number of identical pods are running at all times. If a pod fails or is deleted, the `ReplicationController` automatically creates new pods to maintain the desired number of replicas, providing high availability and scaling for applications.

# Steps and Solution

1. **Create the ReplicationController YAML Definition**:

    Create a YAML file to define the `ReplicationController` with the required specifications:

    Create a file named `nginx-replicationcontroller.yaml`:

    ```yaml
    apiVersion: v1
    kind: ReplicationController
    metadata:
      name: nginx-replicationcontroller
      labels:
        app: nginx_app
        type: front-end
    spec:
      replicas: 3
      selector:
        app: nginx_app
        type: front-end
      template:
        metadata:
          labels:
            app: nginx_app
            type: front-end
        spec:
          containers:
          - name: nginx-container
            image: nginx:latest
    ```

2. **Apply the ReplicationController Configuration**:

    Use `kubectl` to create the `ReplicationController` from the YAML file:

    ```bash
    kubectl apply -f nginx-replicationcontroller.yaml
    ```

3. **Verify the ReplicationController and Pods**:

    After creating the `ReplicationController`, ensure it is running and all pods are in the running state:

    ```bash
    # Verify the ReplicationController
    kubectl get replicationcontroller

    # Check that the pods are running and have the correct labels
    kubectl get pods -l app=nginx_app,type=front-end
    ```
    
    ![image](https://github.com/user-attachments/assets/3d0d6ed4-9a40-4352-91f3-83ee5ee6098e)
