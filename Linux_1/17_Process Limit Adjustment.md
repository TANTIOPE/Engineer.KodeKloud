# Task

In the Stratos Datacenter, the Storage server is encountering performance degradation due to excessive processes held by the `nfsuser` user. To mitigate this issue, we need to enforce limitations on its maximum processes:

- **Soft limit**: 1025
- **Hard limit**: 2024

# Steps and Solution

1. **SSH into the Storage Server**:

    ```bash
    ssh natasha@172.16.238.15
    ```

2. **Edit the `/etc/security/limits.conf` File**:

    Open the `/etc/security/limits.conf` file in a text editor to set the process limits for `nfsuser`.

    ```bash
    sudo nano /etc/security/limits.conf
    ```

3. **Set the Soft and Hard Limits**:

    Add the following lines to the file:

    ```plaintext
    nfsuser soft nproc 1025
    nfsuser hard nproc 2024
    ```

    - `nfsuser`: The username for which the limits are being set.
    - `soft nproc 1025`: Sets the soft limit for the maximum number of processes to 1025.
    - `hard nproc 2024`: Sets the hard limit for the maximum number of processes to 2024.


4. **Verify the Configuration**:

    You can verify the configuration by logging in as `nfsuser` and checking the limits with the `ulimit` command:

    ```bash
    sudo su - nfsuser -c "ulimit -u"
    ```
    
![image](https://github.com/user-attachments/assets/d6baaddb-dcda-4665-a8db-f8f19d986dfc)
