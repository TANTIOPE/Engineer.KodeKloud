# Task

The Nautilus DevOps team is currently engaged in a cleanup process, focusing on removing unnecessary data and services from their AWS account. As part of the migration process, several resources were created for one-time use only, necessitating a cleanup effort to optimize their AWS environment.

**Delete an IAM group named `iamgroup_ravi`.**

# Steps and Solution

1. **Verify the Group Exists**:

    Use the following command to check if the IAM group `iamgroup_ravi` exists, and to see its members if any:

    ```bash
    aws iam get-group --group-name iamgroup_ravi
    ```

    **Output** :

    ```json
    {
    "Users": [],
    "Group": {
        "Path": "/",
        "GroupName": "iamgroup_ravi",
        "GroupId": "AGPAXYKJXMRPVUKKUXJVJ",
        "Arn": "arn:aws:iam::533267440735:group/iamgroup_ravi",
        "CreateDate": "2024-12-30T15:32:49Z"
    }
   }
    ```

    - If there are any users in the group, remove them before deleting the group. You can remove a user using:
      ```bash
      aws iam remove-user-from-group --group-name iamgroup_ravi --user-name <username>
      ```

2. **Delete the IAM Group**:

    Once you confirm the group is empty (no users attached), delete the IAM group `iamgroup_ravi`:

    ```bash
    aws iam delete-group --group-name iamgroup_ravi
    ```

3. **Verify Deletion**:

    After deletion, verify that the group no longer exists. If you run:

    ```bash
    aws iam get-group --group-name iamgroup_ravi
    ```

    ~ on ☁️  (us-east-1) ➜  aws iam get-group --group-name iamgroup_ravi

An error occurred (NoSuchEntity) when calling the GetGroup operation: The group with name iamgroup_ravi cannot be found.
