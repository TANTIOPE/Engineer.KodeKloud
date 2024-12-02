# Task

When establishing infrastructure on the AWS cloud, Identity and Access Management (IAM) is among the first and most critical services to configure. IAM facilitates the creation and management of user accounts, groups, roles, policies, and other access controls. The Nautilus DevOps team is currently in the process of configuring these resources and has outlined the following requirements:

- Create an IAM policy named `iampolicy_mariyam` in the `us-east-1` region.
- The policy must allow read-only access to the EC2 console, enabling users to view all instances, AMIs, and snapshots.

# Steps and Solution

1. **Define the Policy Document**:

    Create a JSON file, `ec2-readonly-policy.json`, to define the policy permissions:

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ec2:Describe*"
                ],
                "Resource": "*"
            }
        ]
    }
    ```

    - **`"ec2:Describe*"`**: Grants permissions to view all EC2 resources such as instances, AMIs, and snapshots.
    - **`"Resource": "*"`**: Applies this permission to all resources.

2. **Create the IAM Policy**:

    Use the following command to create the policy `iampolicy_mariyam` with the permissions defined in the JSON file:

    ```bash
    aws iam create-policy --policy-name iampolicy_mariyam --policy-document file://ec2-readonly-policy.json
    ```

3. **Verify the IAM Policy Creation**:

    After creating the policy, verify its details using the following command:

    ```bash
    aws iam get-policy --policy-arn arn:aws:iam::aws:policy/iampolicy_mariyam
    ```

4. **List All Policies to Confirm**:

    List all policies to ensure that `iampolicy_mariyam` exists:

    ```bash
    aws iam list-policies --query "Policies[?PolicyName=='iampolicy_mariyam']" --output table
    ```

    **Output**:

    ```
    -------------------------------------
    |           ListPolicies           |
    -------------------------------------
    | PolicyName        | PolicyId       |
    -------------------------------------
    | iampolicy_mariyam | ANPAEXAMPLE    |
    -------------------------------------
    ```
