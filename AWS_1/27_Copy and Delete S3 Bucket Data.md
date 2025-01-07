# Task

The Nautilus DevOps team is currently engaged in a cleanup process, focusing on removing unnecessary data and services from their AWS account. As part of the migration process, several resources were created for one-time use only, necessitating a cleanup effort to optimize their AWS environment.

A **S3 bucket** named `devops-bck-14045` already exists. The following actions must be taken:

1. **Copy the contents** of `devops-bck-14045` S3 bucket to the `/opt` directory on the `aws-client` host.
2. **Delete the S3 bucket** `devops-bck-14045`.

# Steps and Solution

1. **Copy the Contents from the S3 Bucket to `/opt`**:

    - Use the `aws s3 cp` or `aws s3 sync` command to download the entire contents from the bucket to the local `/opt` directory on the `aws-client` host.
    - **`--recursive`** (for `cp`) or using `sync` will ensure all objects are copied.

    ```bash
    # Option 1: Using cp with --recursive
    aws s3 cp s3://devops-bck-14045 /opt/ --recursive

    # Option 2: Using sync
    aws s3 sync s3://devops-bck-14045 /opt/
    ```

    - **`s3://devops-bck-14045`**: The S3 bucket source.
    - **`/opt/`**: The local destination directory.
    - Using `sync` is generally recommended when dealing with multiple files and directories.

2. **Delete the S3 Bucket**:

    After confirming you have copied the necessary data, delete the bucket:

    ```bash
    aws s3 rb s3://devops-bck-14045 --force
    ```

    - **`aws s3 rb`**: Removes the S3 bucket.
    - **`--force`**: Deletes all objects in the bucket before removing the bucket itself.

3. **Verify the Cleanup**:

    - **Check `/opt`**: Ensure that all expected files have been downloaded.
    - **List Buckets**: Confirm that `devops-bck-14045` no longer appears in the bucket list.
      ```bash
      aws s3 ls
      ```
