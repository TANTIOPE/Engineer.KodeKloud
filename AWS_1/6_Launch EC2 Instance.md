# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units.

For this task, create an EC2 instance with the following requirements:

1. The name of the instance must be `devops-ec2`.
2. Use the Amazon Linux AMI to launch this instance.
3. The instance type must be `t2.micro`.
4. Create a new RSA key pair named `devops-kp`.
5. Attach the default (available by default) security group.
6. All resources should be created in the `us-east-1` region.

# Steps and Solution

1. **Create an RSA Key Pair**:

    First, create a new RSA key pair named `devops-kp` to be used with the EC2 instance.

    ```bash
    # Create a new RSA key pair named devops-kp and save it to a file
    aws ec2 create-key-pair --key-name devops-kp --query 'KeyMaterial' --output text > devops-kp.pem --region us-east-1
    ```

    - **`--key-name devops-kp`**: Specifies the name of the key pair.
    - **`--query 'KeyMaterial' --output text > devops-kp.pem`**: Saves the private key to a file named `devops-kp.pem`.
    - **`--region us-east-1`**: Ensures the key pair is created in the `us-east-1` region.

    **Expected Output**:
    
    Command will generate and output the key material (private key), which will be saved into the `devops-kp.pem` file.

2. **Identify the Amazon Linux AMI**:

    To launch the EC2 instance, first identify the Amazon Linux AMI ID available in the `us-east-1` region.

    ```bash
    # Describe the Amazon Linux 2 AMI to find its ID
    aws ec2 describe-images --filters "Name=name,Values=amzn2-ami-hvm-*-x86_64-gp2" "Name=owner-alias,Values=amazon" --query 'Images[0].ImageId' --output text --region us-east-1
    ```
    - **`--filters "Name=name,Values=amzn2-ami-hvm-*-x86_64-gp2"`**: Filters the results to only include Amazon Linux 2 AMIs with the specified pattern in the name.
    - **`"Name=owner-alias,Values=amazon"`**: Further filters the results to only include AMIs owned by Amazon.
    - **`--query 'Images[0].ImageId'`**: Retrieves the `ImageId` of the first AMI in the filtered list.
    - **`--output text`**: Returns the output as plain text.
    - **`--region us-east-1`**: Ensures the command runs in the `us-east-1` region.

    **Output**:

    ```text
    ami-007868005aea67c54
   ```

3. **Launch the EC2 Instance**:

    Now, launch the EC2 instance with the specified requirements.

    ```bash
    # Launch the EC2 instance with the specified parameters
    aws ec2 run-instances \
        --image-id ami-007868005aea67c54 \
        --count 1 \
        --instance-type t2.micro \
        --key-name devops-kp \
        --security-groups default \
        --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=devops-ec2}]' \
        --region us-east-1
    ```

    - **`--image-id ami-007868005aea67c54`**: Specifies the AMI ID for Amazon Linux.
    - **`--count 1`**: Launches a single instance.
    - **`--instance-type t2.micro`**: Specifies the instance type.
    - **`--key-name devops-kp`**: Associates the EC2 instance with the created RSA key pair.
    - **`--security-groups default`**: Attaches the default security group to the instance.
    - **`--tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=devops-ec2}]'`**: Tags the instance with the name `devops-ec2`.
    - **`--region us-east-1`**: Launches the instance in the `us-east-1` region.

    **Output**:

```json
{
    "Groups": [],
    "Instances": [
        {
            "AmiLaunchIndex": 0,
            "ImageId": "ami-007868005aea67c54",
            "InstanceId": "i-005ab314673377889",
            "InstanceType": "t2.micro",
            "KeyName": "devops-kp",
            "LaunchTime": "2024-09-02T08:09:27.000Z",
            "Monitoring": {
                "State": "disabled"
            },
            "Placement": {
                "AvailabilityZone": "us-east-1a",
                "GroupName": "",
                "Tenancy": "default"
            },
            "PrivateDnsName": "ip-172-31-16-215.ec2.internal",
            "PrivateIpAddress": "172.31.16.215",
            "ProductCodes": [],
            "PublicDnsName": "",
            "State": {
                "Code": 0,
                "Name": "pending"
            },
            "StateTransitionReason": "",
            "SubnetId": "subnet-07d2d990c4b70aca2",
            "VpcId": "vpc-0c86e7651a1abe217",
            "Architecture": "x86_64",
            "BlockDeviceMappings": [],
            "ClientToken": "009bb33a-6c5e-4394-8f23-a5f4644b2581",
            "EbsOptimized": false,
            "EnaSupport": true,
            "Hypervisor": "xen",
            "NetworkInterfaces": [
                {
                    "Attachment": {
                        "AttachTime": "2024-09-02T08:09:27.000Z",
                        "AttachmentId": "eni-attach-088355ca66269f4a8",
                        "DeleteOnTermination": true,
                        "DeviceIndex": 0,
                        "Status": "attaching",
                        "NetworkCardIndex": 0
                    },
                    "Description": "",
                    "Groups": [
                        {
                            "GroupName": "default",
                            "GroupId": "sg-09d705eae54f622f3"
                        }
                    ],
                    "Ipv6Addresses": [],
                    "MacAddress": "0a:ff:cb:c9:89:a5",
                    "NetworkInterfaceId": "eni-08cfded198eaa151b",
                    "OwnerId": "533267040025",
                    "PrivateDnsName": "ip-172-31-16-215.ec2.internal",
                    "PrivateIpAddress": "172.31.16.215",
                    "PrivateIpAddresses": [
                        {
                            "Primary": true,
                            "PrivateDnsName": "ip-172-31-16-215.ec2.internal",
                            "PrivateIpAddress": "172.31.16.215"
                        }
                    ],
                    "SourceDestCheck": true,
                    "Status": "in-use",
                    "SubnetId": "subnet-07d2d990c4b70aca2",
                    "VpcId": "vpc-0c86e7651a1abe217",
                    "InterfaceType": "interface"
                }
            ],
            "RootDeviceName": "/dev/xvda",
            "RootDeviceType": "ebs",
            "SecurityGroups": [
                {
                    "GroupName": "default",
                    "GroupId": "sg-09d705eae54f622f3"
                }
            ],
            "SourceDestCheck": true,
            "StateReason": {
                "Code": "pending",
                "Message": "pending"
            },
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "devops-ec2"
                }
            ],
            "VirtualizationType": "hvm",
            "CpuOptions": {
                "CoreCount": 1,
                "ThreadsPerCore": 1
            },
            "CapacityReservationSpecification": {
                "CapacityReservationPreference": "open"
            },
            "MetadataOptions": {
                "State": "pending",
                "HttpTokens": "optional",
                "HttpPutResponseHopLimit": 1,
                "HttpEndpoint": "enabled",
                "HttpProtocolIpv6": "disabled",
                "InstanceMetadataTags": "disabled"
            },
            "EnclaveOptions": {
                "Enabled": false
            },
            "PrivateDnsNameOptions": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            },
            "MaintenanceOptions": {
                "AutoRecovery": "default"
            },
            "CurrentInstanceBootMode": "legacy-bios"
        }
    ],
    "OwnerId": "533267040025",
    "ReservationId": "r-0d407f85c33c043e1"
}

```
