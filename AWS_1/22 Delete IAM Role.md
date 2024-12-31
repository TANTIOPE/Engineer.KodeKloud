# Task

The Nautilus DevOps team is currently engaged in a cleanup process, focusing on removing unnecessary data and services from their AWS account. As part of the migration process, several resources were created for one-time use only, necessitating a cleanup effort to optimize their AWS environment.

**Delete the IAM role named `iamrole_mark`.**

# Steps and Solution

1. **Verify the Role Exists**:

    First, check if the IAM role `iamrole_mark` exists by running:

    ```bash
    aws iam get-role --role-name iamrole_mark
    ```

    - If the role does not exist, you’ll receive a `NoSuchEntity` error.
    - If it does exist, proceed to the next step.

2. **Detach Any Policies from the Role**:

    To delete a role, you must remove any attached policies (both managed and inline).

    1. **List Attached Managed Policies**:

        ```bash
        aws iam list-attached-role-policies --role-name iamrole_mark
        ```

        If you have any attached managed policies, detach them using:

        ```bash
        aws iam detach-role-policy --role-name iamrole_mark --policy-arn <policy_arn>
        ```

    2. **List and Delete Inline Policies**:

        ```bash
        aws iam list-role-policies --role-name iamrole_mark
        ```

        For each inline policy returned, remove it:

        ```bash
        aws iam delete-role-policy --role-name iamrole_mark --policy-name <inline_policy_name>
        ```

3. **Delete the Role**:

    Once all policies are detached or deleted, you can remove the IAM role:

    ```bash
    aws iam delete-role --role-name iamrole_mark
    ```

4. **Verify Deletion**:

    Confirm that the role has been deleted by running:

    ```bash
    aws iam get-role --role-name iamrole_mark
    ```

    You should receive a `NoSuchEntity` error indicating the role no longer exists.
