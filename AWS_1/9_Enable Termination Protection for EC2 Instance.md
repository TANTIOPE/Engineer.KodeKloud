# Task

As part of the migration, there were some components created under the AWS account. The Nautilus DevOps team created one EC2 instance where they forgot to enable the termination protection, which is needed for this instance.

An instance named `datacenter-ec2` already exists in the `us-east-1` region. Enable termination protection for this instance.

**What is Termination Protection?**

Termination protection is a safeguard that prevents an EC2 instance from being terminated accidentally through the AWS Management Console or API. This feature ensures that critical instances are not deleted unintentionally.

# Steps and Solution

1. **Find the Instance ID**:

    First, retrieve the instance ID of `datacenter-ec2`:

    ```bash
    aws ec2 describe-instances --filters "Name=tag:Name,Values=datacenter-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

2. **Enable Termination Protection**:

    Enable termination protection on the EC2 instance using the following command:

    ```bash
    aws ec2 modify-instance-attribute --instance-id i-0ef1446311b0ce43b --disable-api-termination
    ```

    Note: **`--disable-api-termination`** should be used **without** `--no-` when enabling termination protection.

3. **Verify Termination Protection**:

    To confirm that termination protection is enabled, use the following command:

    ```bash
    aws ec2 describe-instance-attribute --instance-id i-0ef1446311b0ce43b --attribute disableApiTermination
    ```

    **Output**:

    ```json
    {
      "InstanceId": "i-0ef1446311b0ce43b",
      "DisableApiTermination": {
          "Value": true
      }
    }
    ```

    The `Value: true` indicates that termination protection is successfully enabled.
