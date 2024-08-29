# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, your objective is to create an EBS volume with the following requirements:

### Requirements:
- **Volume Name**: `xfusion-volume`
- **Volume Type**: `gp3`
- **Volume Size**: `2 GiB`

### AWS Credentials:
- **Console URL**: [https://058264486951.signin.aws.amazon.com/console?region=us-east-1](https://058264486951.signin.aws.amazon.com/console?region=us-east-1)
- **Username**: `kk_labs_user_988420`
- **Password**: `*****`
- **Start Time**: Thu Aug 29 11:15:05 UTC 2024
- **End Time**: Thu Aug 29 12:15:05 UTC 2024

**Note:** Ensure that all resources are created in the `us-east-1` region.

# Steps and Solution

1. **Create the EBS Volume**:

    Use the `aws ec2 create-volume` command to create the volume with the specified requirements.

    ```bash
    # Create a gp3 volume of size 2 GiB in the us-east-1 region
    aws ec2 create-volume --volume-type gp3 --size 2 --availability-zone us-east-1a --tag-specifications 'ResourceType=volume,Tags=[{Key=Name,Value=xfusion-volume}]' --region us-east-1
    ```

    - **--volume-type gp3** - Specifies the volume type as General Purpose SSD (gp3).
    - **--size 2** - Sets the volume size to 2 GiB.
    - **--availability-zone us-east-1a** - Specifies the availability zone where the volume will be created (replace with appropriate AZ if necessary).
    - **--tag-specifications** - Tags the volume with the name `xfusion-volume`.

2. **Verify the Volume**:

    After creating the volume, verify its details using the `describe-volumes` command.

    ```bash
    # Describe the created volume to verify its details
    aws ec2 describe-volumes --filters Name=tag:Name,Values=xfusion-volume --region us-east-1
    ```

    - **--filters Name=tag:Name,Values=xfusion-volume** - Filters the volume by its name tag to ensure it was created correctly.
   
   ![image](https://github.com/user-attachments/assets/c8f250f5-8aaf-4f58-8ca2-cfc477d1da86)
