# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, allocate an Elastic IP address and name it as `devops-eip`.

### AWS Credentials:
- **Console URL**: https://654654589397.signin.aws.amazon.com/console?region=us-east-1
- **Username**: `kk_labs_user_726354`
- **Password**: `******`
- **Start Time**: Sat Aug 31 11:43:44 UTC 2024
- **End Time**: Sat Aug 31 12:43:44 UTC 2024

**Notes**:
- Create the resources only in the `us-east-1` region.

# Steps and Solution

1. **Allocate an Elastic IP Address**:

    Use the AWS CLI to allocate a new Elastic IP address in the `us-east-1` region.

    ```bash
    # Allocate an Elastic IP in the us-east-1 region
    aws ec2 allocate-address --domain vpc --region us-east-1
    ```

    - **`--domain vpc`**: Indicates that the Elastic IP is for use in a VPC.
    - **`--region us-east-1`**: Specifies the region where the Elastic IP will be allocated.

    **Output**:

    ```json
   {
    "PublicIp": "52.20.27.11",
    "AllocationId": "eipalloc-0ceacc3bb795d237b",
    "PublicIpv4Pool": "amazon",
    "NetworkBorderGroup": "us-east-1",
    "Domain": "vpc"
   }
    ```

2. **Tag the Elastic IP with the Name `devops-eip`**:

    After allocating the Elastic IP, tag it with the name `devops-eip`.

    ```bash
    # Tag the Elastic IP with the name "devops-eip"
    aws ec2 create-tags --resources eipalloc-0ceacc3bb795d237b --tags Key=Name,Value=devops-eip --region us-east-1
    ```

    - **`--resources eipalloc-0ceacc3bb795d237b`**: Specifies the Allocation ID of the Elastic IP.
    - **`--tags Key=Name,Value=devops-eip`**: Adds a tag with the key `Name` and the value `devops-eip`.
    - **`--region us-east-1`**: Ensures the tag is applied in the `us-east-1` region.
