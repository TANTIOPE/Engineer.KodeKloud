# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, create an AMI from an existing EC2 instance named `devops-ec2` with the following requirements:

- The name of the AMI should be `devops-ec2-ami`.
- Ensure the AMI is in the `available` state.

# Steps and Solution

1. **Find the Instance ID of `devops-ec2`**:

    First, find the instance ID using the following command:

    ```bash
    aws ec2 describe-instances --filters "Name=tag:Name,Values=devops-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text
    ```

    **Output**:

    ```
    i-0459c95f7abdd5adb
    ```

2. **Create the AMI**:

    Once you have the instance ID, create the AMI using the following command:

    ```bash
    aws ec2 create-image --instance-id i-0459c95f7abdd5adb --name "devops-ec2-ami" --no-reboot
    ```

    - **`--no-reboot`**: Ensures that the instance is not rebooted during the AMI creation process.

3. **Verify the AMI Creation**:

    After creating the AMI, check its status using this command:

    ```bash
    aws ec2 describe-images --filters "Name=name,Values=devops-ec2-ami" --query "Images[*].[ImageId,State]" --output table
    ```

    The state should show as `available` once the AMI is fully created.

    **Output**:

    ![image](https://github.com/user-attachments/assets/1f6d1d5c-3345-4a1c-9532-d2060df8936b)

