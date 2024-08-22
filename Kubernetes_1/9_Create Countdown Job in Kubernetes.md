# Task

The Nautilus DevOps team is crafting jobs in the Kubernetes cluster. While they're developing actual scripts/commands, they're currently setting up templates and testing jobs with dummy commands. Please create a job template as per the details given below:

- Create a job named `countdown-nautilus`.
- The spec template should be named `countdown-nautilus` (under metadata), and the container should be named `container-countdown-nautilus`.
- Utilize the image `ubuntu` with the latest tag (ensure to specify as `ubuntu:latest`), and set the restart policy to `Never`.
- Execute the command `sleep 5`.

**Note:** The `kubectl` utility on `jump_host` is set up to operate with the Kubernetes cluster.

# Explanation

A Kubernetes `Job` is a controller that creates one or more pods and ensures that a specified number of them successfully terminate. Jobs are useful for running tasks or scripts that need to be executed to completion, such as batch processing or initialization tasks. The `restartPolicy: Never` ensures that the job's pods are not restarted upon failure, which is suitable for short-lived tasks.

# Steps and Solution

1. **Create the Job YAML Definition**:

    First, create a YAML file to define the `Job`. The file should include the necessary specifications such as the container image, command, and restart policy.

    Create a file named `countdown-nautilus-job.yaml`:

    ```yaml
    apiVersion: batch/v1
    kind: Job
    metadata:
      name: countdown-nautilus
    spec:
      template:
        metadata:
          name: countdown-nautilus
        spec:
          containers:
          - name: container-countdown-nautilus
            image: ubuntu:latest
            command: ["sleep", "5"]
          restartPolicy: Never
    ```

2. **Apply the Job Configuration**:

    Use `kubectl` to create the `Job` from the YAML file:

    ```bash
    kubectl apply -f countdown-nautilus-job.yaml
    ```

3. **Verify the Job**:

    After creating the `Job`, verify its status to ensure it is running as expected:

    ```bash
    kubectl get jobs
    ```

    Check the status of the pods created by the job:

    ```bash
    kubectl get pods -l job-name=countdown-nautilus
    ```

