# Task

During the migration process, several resources were created under the AWS account. Some of these resources became obsolete as alternative solutions were implemented. Among these is an EC2 instance that is no longer in use and needs to be deleted.

1) **Delete the EC2 instance** named `xfusion-ec2` present in the `us-east-1` region.
2) Ensure the instance is in the `terminated` state before submitting the task.

# Steps and Solution

1. **Find the instance ID of `xfusion-ec2`**:

    First, find the instance ID using the following command:

    ```bash
    aws ec2 describe-instances --filters "Name=tag:Name,Values=xfusion-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

    **Output**:

    ```
    i-0aed6b190d31a3fc7
    ```

2. **Stop the instance (if running)**:

    Ensure the instance is in the `stopped` state before deleting it.

    ```bash
    aws ec2 stop-instances --instance-ids i-0aed6b190d31a3fc7
    ```

3. **Delete the instance**:

    Once the instance is stopped, you can terminate it using the following command:

    ```bash
    aws ec2 terminate-instances --instance-ids i-0aed6b190d31a3fc7
    ```

4. **Verify the instance is terminated**:

    After terminating the instance, verify its state to ensure it has been fully terminated.

    ```bash
    aws ec2 describe-instances --instance-ids i-0aed6b190d31a3fc7 --query "Reservations[*].Instances[*].State.Name" --output text
    ```

    The output should show the instance in the `terminated` state:

    **Output**:

    ```
    terminated
    ```
