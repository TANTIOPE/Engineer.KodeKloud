# Task

The Nautilus DevOps team needs to take a snapshot of an existing volume named `datacenter-vol` in the `us-east-1` region as part of their backup strategy. The following requirements must be met:

1) The name of the snapshot must be `datacenter-vol-ss`.
2) The description must be `datacenter Snapshot`.
3) Ensure the snapshot status is `completed` before submitting the task.

# Steps and Solution

1. **Find the volume ID of `datacenter-vol`**:

    First, identify the volume ID of `datacenter-vol` using the following command:

    ```bash
    aws ec2 describe-volumes --filters "Name=tag:Name,Values=datacenter-vol" --query "Volumes[*].VolumeId" --output text
    ```

    **Output**:

    ```
    vol-0b7c2eed5e5dbb1ca
    ```

2. **Create a snapshot**:

    Use the volume ID to create a snapshot with the required name and description:

    ```bash
    aws ec2 create-snapshot --volume-id vol-0b7c2eed5e5dbb1ca --description "datacenter Snapshot" --tag-specifications 'ResourceType=snapshot,Tags=[{Key=Name,Value=datacenter-vol-ss}]'
    ```

    This command creates a snapshot with the name `datacenter-vol-ss` and description `datacenter Snapshot`.

     ![image](https://github.com/user-attachments/assets/e9d0637a-64a0-4888-b5da-5cf8b6ce4619)


4. **Verify the snapshot creation status**:

    Use the snapshot ID `snap-048c75b7fdae5abea` to verify its status:

    ```bash
    aws ec2 describe-snapshots --snapshot-ids snap-048c75b7fdae5abea --query "Snapshots[*].{ID:SnapshotId,State:State}" --output table
    ```

    **Output**:

    ![image](https://github.com/user-attachments/assets/47c3309e-fd15-4eb3-a88e-ac859fe414a4)
