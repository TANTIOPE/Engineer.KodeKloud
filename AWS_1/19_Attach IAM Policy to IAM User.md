# Task

The Nautilus DevOps team has been creating a couple of services on AWS cloud. They have been breaking down the migration into smaller tasks, allowing for better control, risk mitigation, and optimization of resources throughout the migration process. Recently they came up with requirements mentioned below:

- An IAM user named `iamuser_rose` and a policy named `iampolicy_rose` already exist.
- Attach the IAM policy `iampolicy_rose` to the IAM user `iamuser_rose`.

# Steps and Solution

1. **Find the ARN of the Policy**:

    First, find the ARN of the `iampolicy_rose` policy using the following command:

    ```bash
    aws iam list-policies --scope Local --query "Policies[?PolicyName=='iampolicy_rose'].Arn" --output text
    ```

    **Output**:

    ```
    arn:aws:iam::590184099977:policy/iampolicy_rose
    ```

2. **Attach the Policy to the IAM User**:

    Attach the `iampolicy_rose` policy to the `iamuser_rose` IAM user using the following command:

    ```bash
    aws iam attach-user-policy --user-name iamuser_rose --policy-arn arn:aws:iam::590184099977:policy/iampolicy_rose
    ```

    - **`--user-name iamuser_rose`**: Specifies the IAM user to which the policy is attached.
    - **`--policy-arn arn:aws:iam::590184099977:policy/iampolicy_rose`**: Specifies the ARN of the policy to attach.

3. **Verify the Policy Attachment**:

    Confirm that the policy is attached to the `iamuser_rose` user using this command:

    ```bash
    aws iam list-attached-user-policies --user-name iamuser_rose
    ```

    ** Output**:

    ```json
    {
        "AttachedPolicies": [
            {
                "PolicyName": "iampolicy_rose",
                "PolicyArn": "arn:aws:iam::590184099977:policy/iampolicy_rose"
            }
        ]
    }
    ```
