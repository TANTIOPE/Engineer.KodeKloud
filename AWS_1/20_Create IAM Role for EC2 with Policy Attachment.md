# Task

When establishing infrastructure on the AWS cloud, Identity and Access Management (IAM) is among the first and most critical services to configure. IAM facilitates the creation and management of user accounts, groups, roles, policies, and other access controls. The Nautilus DevOps team is currently in the process of configuring these resources and has outlined the following requirements:

- **IAM Role Name**: `iamrole_john`
- **Entity Type**: AWS Service (EC2)
- **Attach Policy**: `iampolicy_john`

# Updated Steps and Solution

Due to permission issues encountered when attaching an inline policy using the `PutRolePolicy` command, an alternative approach is required. Follow the updated steps below:

1. **Create a Trust Policy for EC2**:

    IAM roles require a trust policy to define which entities can assume the role. Create a file named `trust-policy.json` with the following content:

    ```bash
    # Create a trust policy file
    cat > trust-policy.json <<EOL
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "Service": "ec2.amazonaws.com"
          },
          "Action": "sts:AssumeRole"
        }
      ]
    }
    EOL
    ```

2. **Create the IAM Role**:

    Use the following command to create the `iamrole_john` role with the trust policy:

    ```bash
    aws iam create-role --role-name iamrole_john --assume-role-policy-document file://trust-policy.json
    ```

    **Output**:

    ```json
    {
        "Role": {
            "Path": "/",
            "RoleName": "iamrole_john",
            "RoleId": "AROA2UC3AEUZEY4YASIWE",
            "Arn": "arn:aws:iam::730335290674:role/iamrole_john",
            "CreateDate": "2024-12-04T16:21:13Z",
            "AssumeRolePolicyDocument": {
                "Version": "2012-10-17",
                "Statement": [
                    {
                        "Effect": "Allow",
                        "Principal": {
                            "Service": "ec2.amazonaws.com"
                        },
                        "Action": "sts:AssumeRole"
                    }
                ]
            }
        }
    }
    ```

3. **Attach the Managed Policy to the Role**:

    Since inline policies cannot be added due to permission restrictions, attach the managed policy `iampolicy_john` directly to the role:

    ```bash
    aws iam attach-role-policy --role-name iamrole_john --policy-arn arn:aws:iam::730335290674:policy/iampolicy_john
    ```

4. **Verify the Role and Attached Policy**:

    Use the following commands to verify the role creation and attached policies:

    ```bash
    # Verify the IAM role
    aws iam get-role --role-name iamrole_john

    # Verify attached managed policies
    aws iam list-attached-role-policies --role-name iamrole_john
    ```

    **Role Verification Output**:

    ```json
    {
        "Role": {
            "Path": "/",
            "RoleName": "iamrole_john",
            "RoleId": "AROA2UC3AEUZEY4YASIWE",
            "Arn": "arn:aws:iam::730335290674:role/iamrole_john",
            "CreateDate": "2024-12-04T16:21:13Z",
            "AssumeRolePolicyDocument": {
                "Version": "2012-10-17",
                "Statement": [
                    {
                        "Effect": "Allow",
                        "Principal": {
                            "Service": "ec2.amazonaws.com"
                        },
                        "Action": "sts:AssumeRole"
                    }
                ]
            },
            "MaxSessionDuration": 3600,
            "RoleLastUsed": {}
        }
    }
    ```

    **Policy Verification Output**:

    ```json
    {
        "AttachedPolicies": [
            {
                "PolicyName": "iampolicy_john",
                "PolicyArn": "arn:aws:iam::730335290674:policy/iampolicy_john"
            }
        ]
    }
    ```
