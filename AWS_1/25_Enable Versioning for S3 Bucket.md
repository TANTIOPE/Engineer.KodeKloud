# Task

Data protection and recovery are fundamental aspects of data management. It's essential to have systems in place to ensure that data can be recovered in case of accidental deletion or corruption. The DevOps team has received a requirement to enable versioning on one of their S3 buckets to meet these data protection needs.

For this task, **enable versioning** on the S3 bucket named `nautilus-s3-21390`.

# Steps and Solution

1. **Verify the Bucket Exists**:

    Check if the bucket `nautilus-s3-21390` exists. Although optional, it’s a good practice to confirm:

    ```bash
    aws s3api head-bucket --bucket nautilus-s3-21390
    ```
    - If no error is returned, the bucket exists.
    - If you receive a `404` or similar error, the bucket does not exist or you lack permission to access it.

2. **Enable Versioning**:

    Enable versioning on the bucket `nautilus-s3-21390`:

    ```bash
    aws s3api put-bucket-versioning \
        --bucket nautilus-s3-21390 \
        --versioning-configuration Status=Enabled
    ```
    - **`Status=Enabled`**: Turns on versioning for the bucket.

3. **Verify Versioning**:

    Confirm that versioning is enabled:

    ```bash
    aws s3api get-bucket-versioning --bucket nautilus-s3-21390
    ```

    **Output** :
    ```json
    {
      "Status": "Enabled"
    }
    ```
