# Task

The Nautilus DevOps team is presently immersed in data migrations, transferring data from on-premise storage systems to AWS S3 buckets. They have recently received some data that they intend to copy to one of the S3 buckets.

For this task, **copy the file** `/tmp/xfusion.txt` to the existing S3 bucket named `xfusion-cp-4772`.

# Steps and Solution

1. **Verify the S3 Bucket Exists** *(optional check)*:

    Although optional, you can confirm the bucket `xfusion-cp-4772` exists:

    ```bash
    aws s3 ls s3://xfusion-cp-4772
    ```
    - If the command returns an error such as `NoSuchBucket`, the bucket may not exist or you might not have permission to access it.

2. **Copy the File to the S3 Bucket**:

    Use the `aws s3 cp` command to upload `/tmp/xfusion.txt` to the `xfusion-cp-4772` bucket:

    ```bash
    aws s3 cp /tmp/xfusion.txt s3://xfusion-cp-4772/
    ```
    - **`aws s3 cp`**: Copies a file to or from S3.
    - **`/tmp/xfusion.txt`**: The local file path to be copied.
    - **`s3://xfusion-cp-4772/`**: The S3 bucket destination. A trailing slash implies the root of the bucket.

3. **Verify the File Upload**:

    List objects in the `xfusion-cp-4772` bucket to ensure the file exists:

    ```bash
    aws s3 ls s3://xfusion-cp-4772/
    ```
