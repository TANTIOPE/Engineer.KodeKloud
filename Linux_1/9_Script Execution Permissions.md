# Task

In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named `xfusioncorp.sh`. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 3 within the Stratos Datacenter.

Your task is to grant executable permissions to the `/tmp/xfusioncorp.sh` script on App Server 3. Additionally, ensure that all users have the capability to execute it.

# Solution

1. **SSH into App Server 3**:

    ```bash
    ssh banner@172.16.238.12
    ```

2. **Grant Executable Permissions**:

Check files: `cd /tmp`

Change permissions: `sudo chmod +rx xfusioncorp.sh`

- `chmod`: The command used to change file permissions.
- `+rx`: The `+` sign grants the specified permissions, and `r` and `x` represent read and execute permissions, respectively. By using `+rx`, you are granting both read and execute permissions to the file.
- `file_name`: The name of the file you want to modify the permissions for.

Note: To make a file executable, it must also be readable.

3. **Verify the Permissions**:

    Check the permissions of the script to ensure that it is executable by all users.

    - The `ls -l` command lists the file details, showing the permissions in the format `-rwxr-xr-x`, where `x` indicates executable permissions.

    ```bash
    ls -l /tmp/xfusioncorp.sh
    ```
![image](https://github.com/user-attachments/assets/66ec8096-3710-4128-8be2-807f5b348a84)
