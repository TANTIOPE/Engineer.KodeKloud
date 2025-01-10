# Task

When it comes to managing databases, implementing backup and restore processes is a crucial task. It's essential to ensure that a backup process is in place to safeguard data and that restoration processes are available for disaster recovery scenarios. The Nautilus team has outlined the following requirements:

A **RDS instance** named `datacenter-rds` is already running in the `us-east-1` region. For this task, **take a snapshot** of this RDS instance and **name it** `datacenter-rds-snapshot`.

# Steps and Solution

1. **Verify the RDS Instance**:

    Before taking a snapshot, confirm that the RDS instance `datacenter-rds` exists and is in an appropriate state (such as `available`):

    ```bash
    aws rds describe-db-instances \
        --db-instance-identifier datacenter-rds \
        --query "DBInstances[0].DBInstanceStatus"
    ```

    The output should return something like `"available"` if the instance is ready.

2. **Create the RDS Snapshot**:

    Use the `create-db-snapshot` command to create a snapshot named `datacenter-rds-snapshot`:

    ```bash
    aws rds create-db-snapshot \
        --db-snapshot-identifier datacenter-rds-snapshot \
        --db-instance-identifier datacenter-rds
    ```

    - **`--db-snapshot-identifier datacenter-rds-snapshot`**: Specifies the snapshot name.
    - **`--db-instance-identifier datacenter-rds`**: Specifies the RDS instance to snapshot.

3. **Wait for the Snapshot to Complete** (Optional):

    The snapshot creation process can take a few minutes. Use `wait db-snapshot-completed` to pause the CLI until the snapshot is fully available:

    ```bash
    aws rds wait db-snapshot-completed \
        --db-snapshot-identifier datacenter-rds-snapshot
    ```

4. **Verify the RDS Snapshot**:

    After waiting (or giving it some time to complete), confirm that the snapshot exists and is in the `available` state:

    ```bash
    aws rds describe-db-snapshots \
        --db-snapshot-identifier datacenter-rds-snapshot \
        --query "DBSnapshots[0].Status"
    ```

    The output should display `"available"` once the snapshot is ready.
