# Task

The Nautilus DevOps team has been creating several services on AWS cloud. They have been breaking down the migration into smaller tasks, allowing for better control, risk mitigation, and optimization of resources throughout the migration process. Recently, they came up with the following requirement:

- An instance named `devops-ec2` and a volume named `devops-volume` already exist in the `us-east-1` region.
- Attach the `devops-volume` to the `devops-ec2` instance, ensuring that the device name is set to `/dev/sdb` while attaching the volume.

# Steps and Solution

1. **Find the Instance ID of `devops-ec2`**:

    First, we need to find the instance ID using the following command:

    ```bash
    aws ec2 describe-instances --filters "Name=tag:Name,Values=devops-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

    **Output**:

    ```
    i-02c8476c06546ff29
    ```

2. **Find the Volume ID of `devops-volume`**:

    Similarly, find the volume ID using this command:

    ```bash
    aws ec2 describe-volumes --filters "Name=tag:Name,Values=devops-volume" --query "Volumes[*].VolumeId" --output text
    ```

    **Output**:

    ```
    vol-0112638c1ea26e1e5
    ```

3. **Attach the Volume to the EC2 Instance**:

    Now, attach the volume `vol-0112638c1ea26e1e5` to the instance `i-02c8476c06546ff29`, and set the device name to `/dev/sdb`:

    ```bash
    aws ec2 attach-volume --volume-id vol-0112638c1ea26e1e5 --instance-id i-02c8476c06546ff29 --device /dev/sdb
    ```
    ![image](https://github.com/user-attachments/assets/72bdcff3-0cda-48fe-8f26-27e23baaaea6)

4. **Verify the Attachment**:

    Finally, check if the volume is attached by describing the volume and ensuring its state is `in-use`:

    ```bash
    aws ec2 describe-volumes --volume-ids vol-0112638c1ea26e1e5 --query "Volumes[*].State" --output text
    ```

    The output should return:

    ```
    in-use
    ```
