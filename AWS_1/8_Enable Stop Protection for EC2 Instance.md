# Task

As part of the migration, there were some components added to the AWS account. The team created an EC2 instance where they need to make some changes now.

There is an EC2 instance named `devops-ec2` under the `us-east-1` region. Enable stop protection for this instance.

**What is Stop Protection?**

Stop protection prevents an EC2 instance from being stopped via the AWS Management Console, API, or CLI. This is useful when you want to ensure that critical instances are not accidentally stopped during maintenance or automated operations.

# Steps and Solution

1. **Find the Instance ID**:

    The instance ID of `devops-ec2` is `i-04ba2e849aecb5f8d`. This ID can be retrieved using the following command :

    ```bash
    aws ec2 describe-instances --filters "Name=tag:Name,Values=devops-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

2. **Enable Stop Protection**:

    Enable stop protection on the EC2 instance `i-04ba2e849aecb5f8d` by using the following command:

    ```bash
    aws ec2 modify-instance-attribute --instance-id i-04ba2e849aecb5f8d --disable-api-stop
    ```

    - **`--disable-api-stop`**: This option enables stop protection, preventing the instance from being stopped via the AWS Management Console or API.

3. **Verify Stop Protection**:

    To confirm that stop protection has been enabled, describe the instance attributes using:

    ```bash
    aws ec2 describe-instance-attribute --instance-id i-04ba2e849aecb5f8d --attribute disableApiStop
    ```

    **Output**:

    ```json
    {
      "InstanceId": "i-04ba2e849aecb5f8d",
      "DisableApiStop": {
          "Value": true
      }
    }
    ```

    The value of `DisableApiStop` should be `true`, indicating that stop protection is enabled.
