# Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. Recently they started working on creating and configuring some database instances on AWS.

For this task, **create a publicly accessible RDS instance** using a free-tier template (where possible), with the following details:

1. The name of the RDS instance must be `nautilus-rds`.
2. The engine type must be **MySQL v8.0.36**, and the instance class must be **db.t3.micro**.
3. The master username must be **nautilus_admin**, and set an appropriate password.
4. The **RDS storage type** must be **gp2** and storage size must be **5GiB**.
5. Keep the rest of the configurations as default.
6. Finally, ensure the instance is in **available** state before submitting this task.

# Steps and Solution

1. **Create the RDS MySQL Instance**:

    Use the `create-db-instance` command to launch a MySQL instance with the required settings:

    ```bash
    aws rds create-db-instance \
        --db-instance-identifier nautilus-rds \
        --engine mysql \
        --engine-version 8.0.36 \
        --db-instance-class db.t3.micro \
        --master-username nautilus_admin \
        --master-user-password Passw0rd \
        --allocated-storage 5 \
        --storage-type gp2 \
        --publicly-accessible \
        --no-multi-az
    ```

    - **`--db-instance-identifier nautilus-rds`**: Sets the name of the RDS instance.
    - **`--engine mysql --engine-version 8.0.36`**: Chooses MySQL engine, version 8.0.36.
    - **`--db-instance-class db.t3.micro`**: Specifies the free-tier–eligible instance class.
    - **`--master-username nautilus_admin`** and **`--master-user-password Passw0rd`**: Sets the admin credentials.
    - **`--allocated-storage 5`**: Allocates 5GiB of storage.
    - **`--storage-type gp2`**: Uses gp2 storage type.
    - **`--publicly-accessible`**: Makes the instance accessible from the public internet.
    - **`--no-multi-az`**: Ensures it is a single-AZ deployment (default free-tier setting).


2. **Wait for the DB Instance to Become Available**:

    The instance creation process can take several minutes. Use `wait db-instance-available` to hold the CLI until the instance status is `available`:

    ```bash
    aws rds wait db-instance-available \
        --db-instance-identifier nautilus-rds
    ```

3. **Verify the RDS Instance**:

    Once the wait command completes, confirm that the instance is in the `available` state:

    ```bash
    aws rds describe-db-instances \
        --db-instance-identifier nautilus-rds \
        --query "DBInstances[0].DBInstanceStatus"
    ```
