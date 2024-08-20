# Task

The Nautilus DevOps team has noticed performance issues in some `Kubernetes`-hosted applications due to resource constraints. To address this, they plan to set limits on resource utilization. Here are the details:

- Create a pod named `httpd-pod` with a container named `httpd-container`.
- Use the `httpd` image with the latest tag (specify as `httpd:latest`).
- Set the following resource limits:
  - **Requests**: Memory: `15Mi`, CPU: `100m`
  - **Limits**: Memory: `20Mi`, CPU: `100m`

**Note:** The `kubectl` utility on `jump_host` is configured to operate with the Kubernetes cluster.

# Steps and Solution

1. **Create a Pod with Resource Limits**:

    Use the following YAML configuration to create a pod named `httpd-pod` with a container named `httpd-container` and the specified resource limits. Save the configuration to a file named `httpd-pod.yaml`:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: httpd-pod
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
        resources:
          requests:
            memory: "15Mi"
            cpu: "100m"
          limits:
            memory: "20Mi"
            cpu: "100m"
    ```

2. **Apply the Configuration**:

    Use the `kubectl` command to create the pod from the configuration file:

    ```bash
    kubectl apply -f httpd-pod.yaml
    ```

3. **Verify the Pod**:

    Check the status of the pod to ensure it was created successfully:

    ```bash
    kubectl get pods
    ```

    To see more details about the pod:

    ```bash
    kubectl describe pod httpd-pod
    ```
