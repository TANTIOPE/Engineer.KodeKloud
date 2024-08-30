# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition.

For this task, your objective is to create a subnet with the following requirements:

### Requirements:
- **Subnet Name**: `xfusion-subnet`
- **VPC**: Default VPC in the `us-east-1` region

### AWS Credentials:
- **Console URL**: [https://975050354644.signin.aws.amazon.com/console?region=us-east-1](https://975050354644.signin.aws.amazon.com/console?region=us-east-1)
- **Username**: `kk_labs_user_127541`
- **Password**: `*b@uyZyDNRO6`
- **Start Time**: Fri Aug 30 10:58:50 UTC 2024
- **End Time**: Fri Aug 30 11:58:50 UTC 2024

**Note:** Ensure that all resources are created in the `us-east-1` region.

# Steps and Solution

1. **Identify the Default VPC**:

    Retrieve the Default VPC in the `us-east-1` region using the `describe-vpcs` command.

    ```bash
    # Describe VPCs in the us-east-1 region to find the default VPC
    aws ec2 describe-vpcs --filters Name=isDefault,Values=true --region us-east-1
    ```

    **Output**:

    ```json
    {
        "Vpcs": [
            {
                "CidrBlock": "172.31.0.0/16",
                "DhcpOptionsId": "dopt-06d252515e7caecb6",
                "State": "available",
                "VpcId": "vpc-0eab6046a015b832a",
                "OwnerId": "975050354644",
                "InstanceTenancy": "default",
                "CidrBlockAssociationSet": [
                    {
                        "AssociationId": "vpc-cidr-assoc-036dc611d52f94f3d",
                        "CidrBlock": "172.31.0.0/16",
                        "CidrBlockState": {
                            "State": "associated"
                        }
                    }
                ],
                "IsDefault": true
            }
        ]
    }
    ```

2. **List Existing Subnets**:

    Retrieve details about existing subnets in the Default VPC to find available IP ranges for creating the new subnet.

    ```bash
    # Describe subnets in the default VPC to find available IP ranges
    aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-0eab6046a015b832a" --region us-east-1
    ```

    **Output**:

    ```json
    {
        "Subnets": [
            {
                "AvailabilityZone": "us-east-1b",
                "AvailabilityZoneId": "use1-az1",
                "AvailableIpAddressCount": 4091,
                "CidrBlock": "172.31.0.0/20",
                "DefaultForAz": true,
                "MapPublicIpOnLaunch": true,
                "MapCustomerOwnedIpOnLaunch": false,
                "State": "available",
                "SubnetId": "subnet-0c706f45ea75cdb63",
                "VpcId": "vpc-0eab6046a015b832a",
                "OwnerId": "975050354644",
                "AssignIpv6AddressOnCreation": false,
                "Ipv6CidrBlockAssociationSet": [],
                "SubnetArn": "arn:aws:ec2:us-east-1:975050354644:subnet/subnet-0c706f45ea75cdb63",
                "EnableDns64": false,
                "Ipv6Native": false,
                "PrivateDnsNameOptionsOnLaunch": {
                    "HostnameType": "ip-name",
                    "EnableResourceNameDnsARecord": false,
                    "EnableResourceNameDnsAAAARecord": false
                }
            },
            {
                "AvailabilityZone": "us-east-1e",
                "AvailabilityZoneId": "use1-az3",
                "AvailableIpAddressCount": 4091,
                "CidrBlock": "172.31.48.0/20",
                "DefaultForAz": true,
                "MapPublicIpOnLaunch": true,
                "MapCustomerOwnedIpOnLaunch": false,
                "State": "available",
                "SubnetId": "subnet-044372bdc4d6354c1",
                "VpcId": "vpc-0eab6046a015b832a",
                "OwnerId": "975050354644",
                "AssignIpv6AddressOnCreation": false,
                "Ipv6CidrBlockAssociationSet": [],
                "SubnetArn": "arn:aws:ec2:us-east-1:975050354644:subnet/subnet-044372bdc4d6354c1",
                "EnableDns64": false,
                "Ipv6Native": false,
                "PrivateDnsNameOptionsOnLaunch": {
                    "HostnameType": "ip-name",
                    "EnableResourceNameDnsARecord": false,
                    "EnableResourceNameDnsAAAARecord": false
                }
            },
            {
                "AvailabilityZone": "us-east-1f",
                "AvailabilityZoneId": "use1-az5",
                "AvailableIpAddressCount": 4091,
                "CidrBlock": "172.31.64.0/20",
                "DefaultForAz": true,
                "MapPublicIpOnLaunch": true,
                "MapCustomerOwnedIpOnLaunch": false,
                "State": "available",
                "SubnetId": "subnet-0b50919bef03467c6",
                "VpcId": "vpc-0eab6046a015b832a",
                "OwnerId": "975050354644",
                "AssignIpv6AddressOnCreation": false,
                "Ipv6CidrBlockAssociationSet": [],
                "SubnetArn": "arn:aws:ec2:us-east-1:975050354644:subnet/subnet-0b50919bef03467c6",
                "EnableDns64": false,
                "Ipv6Native": false,
                "PrivateDnsNameOptionsOnLaunch": {
                    "HostnameType": "ip-name",
                    "EnableResourceNameDnsARecord": false,
                    "EnableResourceNameDnsAAAARecord": false
                }
            },
            {
                "AvailabilityZone": "us-east-1d",
                "AvailabilityZoneId": "use1-az4",
                "AvailableIpAddressCount": 4091,
                "CidrBlock": "172.31.16.0/20",
                "DefaultForAz": true,
                "MapPublicIpOnLaunch": true,
                "MapCustomerOwnedIpOnLaunch": false,
                "State": "available",
                "SubnetId": "subnet-0062b834772debe87",
                "VpcId": "vpc-0eab6046a015b832a",
                "OwnerId": "975050354644",
                "AssignIpv6AddressOnCreation": false,
                "Ipv6CidrBlockAssociationSet": [],
                "SubnetArn": "arn:aws:ec2:us-east-1:975050354644:subnet/subnet-0062b834772debe87",
                "EnableDns64": false,
                "Ipv6Native": false,
                "PrivateDnsNameOptionsOnLaunch": {
                    "HostnameType": "ip-name",
                    "EnableResourceNameDnsARecord": false,
                    "EnableResourceNameDnsAAAARecord": false
                }
            },
            {
                "AvailabilityZone": "us-east-1a",
                "AvailabilityZoneId": "use1-az6",
                "AvailableIpAddressCount": 4091,
                "CidrBlock": "172.31.32.0/20",
                "DefaultForAz": true,
                "MapPublicIpOnLaunch": true,
                "MapCustomerOwnedIpOnLaunch": false,
                "State": "available",
                "SubnetId": "subnet-06225bc7242021297",
                "VpcId": "vpc-0eab6046a015b832a",
                "OwnerId": "975050354644",
                "AssignIpv6AddressOnCreation": false,
                "Ipv6CidrBlockAssociationSet": [],
                "SubnetArn": "arn:aws:ec2:us-east-1:975050354644:subnet/subnet-06225bc7242021297",
                "EnableDns64": false,
                "Ipv6Native": false,
                "PrivateDnsNameOptionsOnLaunch": {
                    "HostnameType": "ip-name",
                    "EnableResourceNameDnsARecord": false,
                    "EnableResourceNameDnsAAAARecord": false
                }
            },
            {
                "AvailabilityZone": "us-east-1c",
                "AvailabilityZoneId": "use1-az2",
                "AvailableIpAddressCount": 4091,
                "CidrBlock": "172.31.80.0/20",
                "DefaultForAz": true,
                "MapPublicIpOnLaunch": true,
                "MapCustomerOwnedIpOnLaunch": false,
                "State": "available",
                "SubnetId": "subnet-05da69d844c0b17fa",
                "VpcId": "vpc-0eab6046a015b832a",
                "OwnerId": "975050354644",
                "AssignIpv6AddressOnCreation": false,
                "Ipv6CidrBlockAssociationSet": [],
                "SubnetArn": "arn:aws:ec2:us-east-1:975050354644:subnet/subnet-05da69d844c0b17fa",
                "EnableDns64": false,
                "Ipv6Native": false,
                "PrivateDnsNameOptionsOnLaunch": {
                    "HostnameType": "ip-name",
                    "EnableResourceNameDnsARecord": false,
                    "EnableResourceNameDnsAAAARecord": false
                }
            }
        ]
    }
    ```

    **Available IP Ranges**:
    Based on the output, you can select an available CIDR block for your new subnet. In this case, `172.31.96.0/20` is available and can be used.

3. **Create the Subnet**:

    Use the `aws ec2 create-subnet` command to create the subnet within the Default VPC.

    ```bash
    # Create a subnet named xfusion-subnet in the default VPC
    aws ec2 create-subnet --vpc-id vpc-0eab6046a015b832a --cidr-block 172.31.96.0/20 --availability-zone us-east-1a --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=xfusion-subnet}]' --region us-east-1
    ```

    **Output**:

    ```json
    {
        "Subnet": {
            "AvailabilityZone": "us-east-1a",
            "AvailabilityZoneId": "use1-az6",
            "AvailableIpAddressCount": 4091,
            "CidrBlock": "172.31.96.0/20",
            "DefaultForAz": false,
            "MapPublicIpOnLaunch": false,
            "State": "available",
            "SubnetId": "subnet-03d8d014ef2eef424",
            "VpcId": "vpc-0eab6046a015b832a",
            "OwnerId": "975050354644",
            "AssignIpv6AddressOnCreation": false,
            "Ipv6CidrBlockAssociationSet": [],
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "xfusion-subnet"
                }
            ],
            "SubnetArn": "arn:aws:ec2:us-east-1:975050354644:subnet/subnet-03d8d014ef2eef424",
            "EnableDns64": false,
            "Ipv6Native": false,
            "PrivateDnsNameOptionsOnLaunch": {
                "HostnameType": "ip-name",
                "EnableResourceNameDnsARecord": false,
                "EnableResourceNameDnsAAAARecord": false
            }
        }
    }
    ```
