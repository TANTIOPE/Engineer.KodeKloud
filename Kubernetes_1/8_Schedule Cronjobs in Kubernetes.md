# Task

The Nautilus DevOps team is setting up recurring tasks on different schedules. Currently, they're developing scripts to be executed periodically. To kickstart the process, they're creating cron jobs in the Kubernetes cluster with placeholder commands. Follow the instructions below:

1. Create a `CronJob` named `xfusion`.

2. Set its schedule to `*/9 * * * *` (you can adjust the schedule as needed).

3. Name the container `cron-xfusion`.

4. Utilize the `nginx` image with the latest tag (specify as `nginx:latest`).

5. Execute the dummy command `echo Welcome to xfusioncorp!`.

6. Ensure the `restartPolicy` is set to `OnFailure`.

**Note:** The `kubectl` utility on `jump_host` is configured to work with the Kubernetes cluster.

# Explanation

A `CronJob` in Kubernetes allows you to run a job on a scheduled basis, similar to cron jobs in Unix-based systems. You define a schedule using cron syntax, and Kubernetes ensures that the specified job is executed according to this schedule. This is useful for periodic tasks such as backups, report generation, or regular maintenance tasks.

# Steps and Solution

1. **Create the CronJob YAML Definition**:

    Create a YAML file to define the `CronJob`. This file should include the necessary specifications, such as the schedule, image, container name, and command.

    Create a file named `xfusion-cronjob.yaml`:

    ```yaml
    apiVersion: batch/v1
    kind: CronJob
    metadata:
      name: xfusion
    spec:
      schedule: "*/9 * * * *"  # Adjust the schedule as needed
      jobTemplate:
        spec:
          template:
            spec:
              containers:
              - name: cron-xfusion
                image: nginx:latest
                command: ["sh", "-c", "echo Welcome to xfusioncorp!"]
              restartPolicy: OnFailure
    ```

2. **Apply the CronJob Configuration**:

    Use `kubectl` to create the `CronJob` from the YAML file:

    ```bash
    kubectl apply -f xfusion-cronjob.yaml
    ```

3. **Verify the CronJob**:

    After creating the `CronJob`, verify that it has been created successfully:

    ```bash
    kubectl get cronjob xfusion
    ```

4. **Check the Status of the Jobs**:

    List the jobs created by the `CronJob` to confirm that they are running as expected:

    ```bash
    kubectl get jobs --selector=job-name=xfusion
    ```
