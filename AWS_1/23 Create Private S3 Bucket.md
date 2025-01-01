# Task

As part of the data migration process, the Nautilus DevOps team is actively creating several S3 buckets on AWS. They plan to utilize both private and public S3 buckets to store relevant data. Given the ongoing migration of other infrastructure to AWS, it is logical to consolidate data storage within the AWS environment as well.

For this task, create an S3 bucket with the following details:

1. The name of the S3 bucket must be `devops-s3-18593`.
2. The S3 bucket must block all public access, ensuring it is private.

# Steps and Solution

1. **Create the S3 Bucket**:

    Use the `aws s3api create-bucket` command to create the bucket named `devops-s3-18593`. Make sure you specify the region if needed (e.g., `us-east-1`).

    ```bash
    aws s3api create-bucket \
        --bucket devops-s3-18593 \
        --region us-east-1 \
    ```

    - **`--bucket devops-s3-18593`**: Sets the bucket name.
    - **`--region us-east-1`**: Specifies the AWS region.

2. **Block All Public Access**:

    To ensure the bucket is private, configure the Block Public Access settings:

    ```bash
    aws s3api put-public-access-block \
        --bucket devops-s3-18593 \
        --public-access-block-configuration \
        "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"
    ```

    - **`--public-access-block-configuration`**: Specifies the public access block settings.
    - Setting all values to `true` ensures the bucket is fully private.

3. **Verify the Bucket Configuration**:

    - **Check the Bucket ACL**:
      ```bash
      aws s3api get-bucket-acl --bucket devops-s3-18593
      ```
      This should show the owner as the only entity with access.

    - **Check the Public Access Block**:
      ```bash
      aws s3api get-public-access-block --bucket devops-s3-18593
      ```
      This command will return the current public access block configuration :
      ```json
      {
        "PublicAccessBlockConfiguration": {
          "BlockPublicAcls": true,
          "IgnorePublicAcls": true,
          "BlockPublicPolicy": true,
          "RestrictPublicBuckets": true
        }
      }
      ```
