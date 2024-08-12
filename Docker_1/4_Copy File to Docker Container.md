# Task

The Nautilus DevOps team possesses confidential data on App Server 1 in the Stratos Datacenter. A container named `ubuntu_latest` is running on the same server.

- Copy an encrypted file `/tmp/nautilus.txt.gpg` from the docker host to the `ubuntu_latest` container located at `/opt/`. Ensure the file is not modified during this operation.

# Solution

1. **SSH into App Server 1:**

    Start by logging into App Server 1 (stapp01) using the provided credentials.

    ```bash
    ssh tony@172.16.238.10
    sudo su -
    ```

2. **Copy the File to the Container:**

    Use the `docker cp` command to copy the encrypted file from the host to the container. The `docker cp` command preserves the file's attributes and ensures it is not modified during the copy process.

    ```bash
    docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/opt/
    ```
![image](https://github.com/user-attachments/assets/e402c272-64b5-4ace-aa99-4c74917e58d2)
