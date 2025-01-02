# Task

As part of the data migration process, the Nautilus DevOps team is actively creating several S3 buckets on AWS. They plan to utilize both private and public S3 buckets to store relevant data. Given the ongoing migration of other infrastructure to AWS, it is logical to consolidate data storage within the AWS environment as well.

For this task, **create a public S3 bucket** named `datacenter-s3-14840`. However, because `BlockPublicAcls` is preventing the use of `put-bucket-acl --acl public-read`, we will adjust the bucket’s Block Public Access settings first and then verify the ACL.

# Steps and Solution

1. **Create the S3 Bucket**:

    Since we’re working in `us-east-1`, do **not** provide a location constraint (to avoid `InvalidLocationConstraint` errors):

    ```bash
    aws s3api create-bucket \
        --bucket datacenter-s3-14840 \
        --region us-east-1
    ```

    - **`--bucket datacenter-s3-14840`**: Sets the bucket name.
    - **`--region us-east-1`**: Issues the command to the `us-east-1` endpoint.

2. **Disable Block Public Access** (if you have permission):

    Modify the bucket’s Block Public Access configuration so you can apply ACL-based public access:

    ```bash
    aws s3api put-public-access-block \
        --bucket datacenter-s3-14840 \
        --public-access-block-configuration \
        "BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false"
    ```

    - **`BlockPublicAcls=false`**: Allows bucket ACLs to grant public access.
    - **`IgnorePublicAcls=false`**: Does not ignore existing public ACLs.
    - **`BlockPublicPolicy=false`**: Permits public bucket policies.
    - **`RestrictPublicBuckets=false`**: Does not restrict the bucket from becoming public.

3. **Verify the Bucket ACL**:

    Confirm the bucket’s ACL to ensure it reflects the correct owner permissions (and any potential public read, if applied):

    ```bash
    aws s3api get-bucket-acl --bucket datacenter-s3-14840
    ```

    If you later apply a public-read ACL (separately), this command will show a grant to the `AllUsers` group with `READ` permission.
