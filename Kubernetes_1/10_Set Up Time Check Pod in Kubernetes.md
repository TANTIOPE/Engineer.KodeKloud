# Task

The Nautilus DevOps team needs to create a time-check pod in a specific Kubernetes namespace for logging purposes. Initially, this is for testing, but it may later be integrated into an existing cluster. The details are as follows:

1. **Create a Pod** named `time-check` in the `devops` namespace.
2. The pod should contain a container named `time-check`, utilizing the `busybox` image with the latest tag (specify as `busybox:latest`).
3. Create a ConfigMap named `time-config` with the data `TIME_FREQ=12` in the same namespace.
4. Configure the `time-check` container to execute the command: `while true; do date; sleep $TIME_FREQ; done`. Ensure the result is written to `/opt/sysops/time/time-check.log`.
5. Add an environmental variable `TIME_FREQ` in the container, fetching its value from the `ConfigMap` `TIME_FREQ` key.
6. Create a volume `log-volume` and mount it at `/opt/sysops/time` within the container.

**Note:** The `kubectl` utility on `jump_host` is configured to operate with the Kubernetes cluster.

# Explanation

The task involves creating a pod in the Kubernetes cluster within a specific namespace, `devops`. The pod will have a container running a simple loop that logs the current date and time to a file, with the frequency determined by a value stored in a `ConfigMap`. This exercise tests your understanding of Kubernetes concepts such as namespaces, pods, containers, `ConfigMaps`, environment variables, and volumes.

# Steps and Solution

1. **Create the Namespace:**

    First, ensure that the `devops` namespace exists. If it doesn't, create it:

    ```bash
    kubectl create namespace devops
    ```

2. **Create the ConfigMap:**

    Create a `ConfigMap` named `time-config` in the `devops` namespace with the required data:

    ```bash
    kubectl create configmap time-config --from-literal=TIME_FREQ=12 -n devops
    ```

3. **Create the Pod YAML Definition:**

    Next, create a YAML file to define the pod with all the necessary configurations:

    Create a file named `time-check-pod.yaml`:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: time-check
      namespace: devops
    spec:
      containers:
      - name: time-check
        image: busybox:latest
        command: ["/bin/sh", "-c"]
        args:
          - while true; do date; sleep \$TIME_FREQ; done > /opt/sysops/time/time-check.log;
        env:
        - name: TIME_FREQ
          valueFrom:
            configMapKeyRef:
              name: time-config
              key: TIME_FREQ
        volumeMounts:
        - name: log-volume
          mountPath: /opt/sysops/time
      volumes:
      - name: log-volume
        emptyDir: {}
    ```

4. **Apply the Pod Configuration:**

    Use `kubectl` to create the pod from the YAML file:

    ```bash
    kubectl apply -f time-check-pod.yaml
    ```

5. **Verify the Pod and ConfigMap:**

    Check that the pod and the `ConfigMap` are correctly configured and running:

    ```bash
    # Verify that the Pod is running
    kubectl get pods -n devops

    # Verify that the ConfigMap is correctly applied
    kubectl get configmap time-config -n devops
    ```
