# Task

The Nautilus DevOps team is gearing up to deploy applications on a `Kubernetes` cluster for migration purposes. A team member has been tasked with creating a `ReplicaSet` outlined below:

1. Create a `ReplicaSet` using the `httpd` image with the latest tag (ensure to specify as `httpd:latest`) and name it `httpd-replicaset`.

2. Apply the following labels:
   - `app` as `httpd_app`
   - `type` as `front-end`

3. Name the container `httpd-container` and ensure the replica count is `4`.

**Note:** The `kubectl` utility on `jump_host` is set up to interact with the Kubernetes cluster.

# Explanation

A `ReplicaSet` in Kubernetes ensures that a specified number of pod replicas are running at all times. It automatically replaces any pods that fail or are deleted to maintain the desired number of replicas, thus providing high availability and fault tolerance for applications.

# Steps and Solution

1. **Create the ReplicaSet YAML Definition**:

    First, create a YAML file to define the `ReplicaSet`. This file will specify the image, labels, and replica count.

    Create a file named `httpd-replicaset.yaml`:

    ```yaml
    apiVersion: apps/v1
    kind: ReplicaSet
    metadata:
      name: httpd-replicaset
      labels:
        app: httpd_app
        type: front-end
    spec:
      replicas: 4
      selector:
        matchLabels:
          app: httpd_app
      template:
        metadata:
          labels:
            app: httpd_app
        spec:
          containers:
          - name: httpd-container
            image: httpd:latest
    ```

2. **Apply the ReplicaSet Configuration**:

    Use `kubectl` to create the `ReplicaSet` from the YAML file:

    ```bash
    kubectl apply -f httpd-replicaset.yaml
    ```

3. **Verify the ReplicaSet**:

    After creating the `ReplicaSet`, verify that it is running as expected with the correct number of replicas:

    ```bash
    kubectl get replicaset
    ```

    Ensure that the `httpd-replicaset` has 4 replicas.

4. **Check the Pods**:

    List the pods to confirm that they are running:

    ```bash
    kubectl get pods -l app=httpd_app
    ```

    This command filters the pods with the label `app=httpd_app` to check that 4 pods are created and running.
