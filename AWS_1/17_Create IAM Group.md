# Task

The Nautilus DevOps team has been creating services on the AWS cloud and breaking down the migration into smaller tasks for better control and resource optimization. The following requirement has been outlined:

- Create an IAM group named `iamgroup_ammar` in the `us-east-1` region.

# Steps and Solution

1. **Create the IAM group**:

    Use the following command to create the IAM group `iamgroup_ammar`:

    ```bash
    aws iam create-group --group-name iamgroup_ammar
    ```

    This command will create a new IAM group with the specified name.
   
   ![image](https://github.com/user-attachments/assets/e3d30bd7-9413-4ff0-a02e-b354cc9d6219)
