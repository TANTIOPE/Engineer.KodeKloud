# Task

The Nautilus DevOps team has been creating a couple of services on the AWS cloud. They have been breaking down the migration into smaller tasks, allowing for better control, risk mitigation, and optimization of resources throughout the migration process. Recently they came up with the following requirements:

There is an instance named `nautilus-ec2` and an Elastic IP named `nautilus-ec2-eip` in the `us-east-1` region. Attach the `nautilus-ec2-eip` Elastic IP to the `nautilus-ec2` instance.

**What is an Elastic IP?**

An Elastic IP (EIP) is a static, public IPv4 address designed for dynamic cloud computing. Unlike regular public IPs, Elastic IPs persist even when an instance is stopped or terminated, making them useful for instances that need to maintain a consistent public IP.

# Steps and Solution

1. **Find the Instance ID**:

    The instance ID of `nautilus-ec2` is `i-05b798fd9bce1ab63`. This was retrieved using the command:

    ```bash
    aws ec2 describe-instances --filters "Name=tag:Name,Values=nautilus-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

2. **Find the Allocation ID of the Elastic IP**:

    The Allocation ID of `nautilus-ec2-eip` is `eipalloc-0365a608efe40bae3`, retrieved using the command:

    ```bash
    aws ec2 describe-addresses --filters "Name=tag:Name,Values=nautilus-ec2-eip" --query "Addresses[*].AllocationId" --output text
    ```

3. **Associate the Elastic IP with the EC2 Instance**:

    Attach the Elastic IP `eipalloc-0365a608efe40bae3` to the EC2 instance `i-05b798fd9bce1ab63` by running the following command:

    ```bash
    aws ec2 associate-address --instance-id i-05b798fd9bce1ab63 --allocation-id eipalloc-0365a608efe40bae3
    ```
    
  ![image](https://github.com/user-attachments/assets/879c11c0-6fdb-46fa-b581-5ff590edd372)

4. **Verify the Association**:

    To confirm that the Elastic IP is successfully associated with the instance, describe the instance to check its public IP:

    ```bash
    aws ec2 describe-instances --instance-id i-05b798fd9bce1ab63 --query "Reservations[*].Instances[*].PublicIpAddress" --output text
    ```
    
  ![image](https://github.com/user-attachments/assets/7dd141bc-4427-4f82-bf03-a2b7f14851e5)
