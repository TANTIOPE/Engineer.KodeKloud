# Task

During the migration process, the Nautilus DevOps team created several EC2 instances in different regions. They are currently in the process of identifying the correct resources and utilization and are making continuous changes to ensure optimal resource utilization. Recently, they discovered that one of the EC2 instances was underutilized, prompting them to decide to change the instance type. Please make sure the Status check is completed (if its still in Initializing state) before making any changes to the instance.

1) Change the instance type from `t2.micro` to `t2.nano` for `devops-ec2` instance.

2) Make sure the EC2 instance `devops-ec2` is in running state after the change.

# Steps and Solution

1. **Find the Instance ID of the Instance with the Tag `devops-ec2`**:

    Use the AWS CLI to retrieve the instance ID of the instance with the tag `Name=devops-ec2`.

    ```bash
    # Retrieve the instance ID of the instance with the tag Name=devops-ec2
    aws ec2 describe-instances --filters "Name=tag:Name,Values=devops-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

    - **`--filters "Name=tag:Name,Values=devops-ec2"`**: Filters instances based on the tag `Name=devops-ec2`.
    - **`--query "Reservations[*].Instances[*].InstanceId"`**: Extracts the instance ID from the response.
    - **`--output text`**: Formats the output as plain text.

2. **Stop the EC2 Instance**:

    Stop the EC2 instance to prepare it for the instance type modification.

    ```bash
    # Stop the EC2 instance with the retrieved instance ID
    aws ec2 stop-instances --instance-ids i-02db9cdd29ccb1fdb
    ```

    - **`--instance-ids i-02db9cdd29ccb1fdb`**: Specifies the instance ID to stop.

3. **Change the Instance Type to `t2.nano`**:

    Modify the instance type of the stopped instance.

    ```bash
    # Change the instance type to t2.nano for the stopped instance
    aws ec2 modify-instance-attribute --instance-id i-02db9cdd29ccb1fdb --instance-type "{\"Value\":\"t2.nano\"}"
    ```

    - **`--instance-id i-02db9cdd29ccb1fdb`**: Specifies the instance ID to modify.
    - **`--instance-type "{\"Value\":\"t2.nano\"}"`**: Sets the new instance type.

4. **Start the EC2 Instance**:

    Start the instance again after modifying its type.

    ```bash
    # Start the EC2 instance with the modified type
    aws ec2 start-instances --instance-ids i-02db9cdd29ccb1fdb
    ```

    - **`--instance-ids i-02db9cdd29ccb1fdb`**: Specifies the instance ID to start.

5. **Verify the Instance Type**:

    Check that the instance type has been updated and the instance is running.

    ```bash
    # Describe the instance to verify its type
    aws ec2 describe-instances --instance-ids i-02db9cdd29ccb1fdb --query "Reservations[*].Instances[*].[InstanceId,InstanceType]" --output table
    ```

    - **`--instance-ids i-02db9cdd29ccb1fdb`**: Specifies the instance ID to describe.
    - **`--query "Reservations[*].Instances[*].[InstanceId,InstanceType]"`**: Retrieves the instance ID and type.
    - **`--output table`**: Formats the output as a table for easy reading.

    ![image](https://github.com/user-attachments/assets/336f0476-6078-4ef8-9df0-6cbb5a26608b)
