# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. To ensure a smooth migration, you need to create an RSA key pair with the following requirements:

- **Key Pair Name**: `xfusion-kp`
- **Key Pair Type**: `rsa`

### AWS Credentials
- **Console URL**: [AWS Console](https://905418286783.signin.aws.amazon.com/console?region=us-east-1)
- **Username**: `kk_labs_user_686563`
- **Password**: `*****`
- **Start Time**: Mon Aug 26 07:15:10 UTC 2024
- **End Time**: Mon Aug 26 08:15:10 UTC 2024

**Note:** Ensure that all resources are created in the `us-east-1` region.

# Steps and Solution

1. **Create the RSA Key Pair**:

    Use the AWS CLI to create a new RSA key pair named `xfusion-kp` in the `us-east-1` region.

    ```bash
    # Create the RSA key pair named xfusion-kp
    aws ec2 create-key-pair --key-name xfusion-kp --key-type rsa --region us-east-1
    ```

    - **`--key-name xfusion-kp`**: Specifies the name of the key pair.
    - **`--key-type rsa`**: Specifies that the key pair type is RSA.
    - **`--region us-east-1`**: Ensures the key pair is created in the `us-east-1` region.

    This command will output the private key in PEM format, which you should save securely.

2. **Verify the Key Pair Creation**:

    After creating the key pair, verify its existence using the following command:

    ```bash
    # Verify that the key pair xfusion-kp exists
    aws ec2 describe-key-pairs --key-name xfusion-kp --region us-east-1
    ```

    - **`--key-name xfusion-kp`**: Specifies the key pair to describe.
    - **`--region us-east-1`**: Ensures the command checks the `us-east-1` region.

    This command will return details about the `xfusion-kp` key pair if it exists.
   
   ![image](https://github.com/user-attachments/assets/82ffb24e-d741-433c-888a-4552b5ff3090)

   
