# Task

The Nautilus DevOps team has been creating several services on the AWS cloud. They have been breaking down the migration into smaller tasks, allowing for better control, risk mitigation, and optimization of resources throughout the migration process. Recently, they came up with the following requirements:

An instance named `nautilus-ec2` and an Elastic Network Interface (ENI) named `nautilus-eni` already exist in the `us-east-1` region. 

- Attach the `nautilus-eni` network interface to the `nautilus-ec2` instance.
- Ensure that the status is **attached** before submitting the task.
- Ensure that instance initialization has been completed before proceeding with the task.

**What is an Elastic Network Interface (ENI)?**

An ENI is a virtual network interface that can be attached to an EC2 instance. It allows you to manage network settings and maintain separate IPs for different services. ENIs can be detached and reattached to different instances within the same availability zone, making them useful for dynamic configurations.

# Steps and Solution

1. **Find the Instance ID of the `nautilus-ec2` Instance**:

    Retrieve the instance ID using the following command:

    ```bash
    aws ec2 describe-instances --filters "Name=tag:Name,Values=nautilus-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

    **Output**:

    ```text
    i-0b7f44ab31a31d753
    ```

2. **Find the Network Interface ID of the `nautilus-eni` ENI**:

    Retrieve the ENI ID using the following command:

    ```bash
    aws ec2 describe-network-interfaces --filters "Name=tag:Name,Values=nautilus-eni" --query "NetworkInterfaces[*].NetworkInterfaceId" --output text
    ```

    **Output**:

    ```text
    eni-066a847aaba289060
    ```

3. **Attach the Network Interface to the EC2 Instance**:

    Attach the network interface `eni-066a847aaba289060` to the instance `i-0b7f44ab31a31d753`:

    ```bash
    aws ec2 attach-network-interface --instance-id i-0b7f44ab31a31d753 --network-interface-id eni-066a847aaba289060 --device-index 1
    ```

    - **`--device-index 1`**: Specifies the device index, indicating where to attach the ENI on the instance. Index 1 is typically used for additional ENIs.

4. **Verify the Attachment Status**:

    Check if the network interface has been attached successfully by running the following command:

    ```bash
    aws ec2 describe-network-interfaces --network-interface-ids eni-066a847aaba289060 --query "NetworkInterfaces[*].Status" --output text
    ```

    The output should return `in-use`, indicating that the ENI is attached.

5. **Ensure EC2 Initialization is Complete**:

    Verify that the `nautilus-ec2` instance initialization has completed:

    ```bash
    aws ec2 describe-instance-status --instance-id i-0b7f44ab31a31d753 --query "InstanceStatuses[*].InstanceStatus.Status" --output text
    ```

    The output should show `ok`, indicating that the instance has completed initialization.
