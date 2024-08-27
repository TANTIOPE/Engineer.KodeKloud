# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, create a security group under the default VPC with the following requirements:

- **Security Group Name**: `devops-sg`
- **Description**: `Security group for Nautilus App Servers`
- **Inbound Rules**:
  - HTTP (Port 80, Source: 0.0.0.0/0)
  - SSH (Port 22, Source: 0.0.0.0/0)
    
### AWS Credentials
- **Console URL**: [AWS Console](https://975049942609.signin.aws.amazon.com/console?region=us-east-1)
- **Username**: `kk_labs_user_575034`
- **Password**: `***********`
- **Start Time**: Tue Aug 27 14:09:22 UTC 2024
- **End Time**: Tue Aug 27 15:09:22 UTC 2024

**Note:** Ensure that all resources are created in the `us-east-1` region.

# Steps and Solution

1. **Create the Security Group**:

    Use the AWS CLI to create a new security group named `devops-sg` under the default VPC in the `us-east-1` region.

    ```bash
    # Create the security group named devops-sg
    aws ec2 create-security-group --group-name devops-sg --description "Security group for Nautilus App Servers" --vpc-id $(aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[0].VpcId" --output text) --region us-east-1
    ```

    - **`--group-name devops-sg`**: Specifies the name of the security group.
    - **`--description "Security group for Nautilus App Servers"`**: Provides a description for the security group.
    - **`--vpc-id $(...)`**: Automatically retrieves the ID of the default VPC in the `us-east-1` region.
    - **`--region us-east-1`**: Ensures the security group is created in the `us-east-1` region.
      
    ![image](https://github.com/user-attachments/assets/40e1dd45-34ad-4c43-bb82-b3804afbdeab)


2. **Add Inbound Rules**:

    After creating the security group, add the required inbound rules for HTTP and SSH.

    ```bash
    # Add HTTP rule to allow traffic on port 80 from any IP
    aws ec2 authorize-security-group-ingress --group-name devops-sg --protocol tcp --port 80 --cidr 0.0.0.0/0 --region us-east-1

    # Add SSH rule to allow traffic on port 22 from any IP
    aws ec2 authorize-security-group-ingress --group-name devops-sg --protocol tcp --port 22 --cidr 0.0.0.0/0 --region us-east-1
    ```

    - **`--protocol tcp`**: Specifies the TCP protocol.
    - **`--port 80`**: Specifies the port for the HTTP rule.
    - **`--port 22`**: Specifies the port for the SSH rule.
    - **`--cidr 0.0.0.0/0`**: Allows access from any IP address.
   
    ![image](https://github.com/user-attachments/assets/cf5e2e4e-e165-47b1-a728-f508c423a4a1)
    ![image](https://github.com/user-attachments/assets/6208ea2f-fa81-461d-b071-abfe273719e2)

3. **Verify the Security Group**:

    Finally, verify that the security group and its inbound rules have been created successfully.

    ```bash
    # Describe the security group to verify its configuration
    aws ec2 describe-security-groups --group-names devops-sg --region us-east-1
    ```

    - **`--group-names devops-sg`**: Specifies the security group to describe.
    - **`--region us-east-1`**: Ensures the command checks the `us-east-1` region.
      
~ on ☁️  (us-east-1) ➜  `aws ec2 describe-security-groups --group-names devops-sg --region us-east-1`
```json
{
    "SecurityGroups": [
        {
            "Description": "Security group for Nautilus App Servers",
            "GroupName": "devops-sg",
            "IpPermissions": [
                {
                    "FromPort": 80,
                    "IpProtocol": "tcp",
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "Ipv6Ranges": [],
                    "PrefixListIds": [],
                    "ToPort": 80,
                    "UserIdGroupPairs": []
                },
                {
                    "FromPort": 22,
                    "IpProtocol": "tcp",
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "Ipv6Ranges": [],
                    "PrefixListIds": [],
                    "ToPort": 22,
                    "UserIdGroupPairs": []
                }
            ],
            "OwnerId": "975049942609",
            "GroupId": "sg-0bfd906435c7529a3",
            "IpPermissionsEgress": [
                {
                    "IpProtocol": "-1",
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "Ipv6Ranges": [],
                    "PrefixListIds": [],
                    "UserIdGroupPairs": []
                }
            ],
            "VpcId": "vpc-0cd0729b5b932689e"
        }
    ]
}
