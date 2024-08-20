

# Task

The Nautilus DevOps team is diving into `Kubernetes` for application management. One team member has a task to create a pod according to the details below:

1. Create a pod named `pod-httpd` using the `httpd` image with the latest tag. Ensure to specify the tag as `httpd:latest`.

2. Set the `app` label to `httpd_app`, and name the container as `httpd-container`.

**Note:** The `kubectl` utility on `jump_host` is configured to operate with the Kubernetes cluster.

# Steps and Solution

1. **Create a YAML file for the pod configuration**:

    - First, create a YAML file to define the pod with the specified parameters. We will name the file `pod-httpd.yml`:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: pod-httpd
      labels:
        app: httpd_app
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
    ```

2. **Apply the configuration to create the pod**:

    - Use `kubectl` to create the pod by applying the YAML file:

    ```bash
    kubectl apply -f pod-httpd.yml
    ```

    - This command will create a pod named `pod-httpd` with the `httpd:latest` image, an `app` label of `httpd_app`, and a container named `httpd-container`.

3. **Verify the pod creation**:

    - To ensure the pod has been created successfully, run the following command to check the status:

    ```bash
    kubectl get pods
    ```

    - You should see `pod-httpd` listed among the running pods.

4. **Check pod details**:

    - For more detailed information about the pod, you can describe it using:

    ```bash
    kubectl describe pod pod-httpd
    ```

    - This will show you the full configuration and status of the `pod-httpd`.
