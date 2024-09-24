# Task

The Nautilus DevOps team is currently configuring Identity and Access Management (IAM) to establish their infrastructure on the AWS cloud. IAM is essential for managing user accounts, groups, roles, and access controls. The following requirement has been outlined:

- Create an IAM user named `iamuser_jim`.

# Steps and Solution

1. **Create the IAM user**:

    Use the following command to create the IAM user `iamuser_jim`:

    ```bash
    aws iam create-user --user-name iamuser_jim
    ```

    This command will create a new IAM user with the specified username.

2. **Verify the IAM user creation**:

    After creating the user, verify that the user has been created successfully with the following command:

    ```bash
    aws iam get-user --user-name iamuser_jim --query "User.{UserName:UserName,UserId:UserId}" --output table
    ```

    **Output**:

     ![image](https://github.com/user-attachments/assets/d9a0eba9-6cad-4f19-9e24-786009dcd087)
