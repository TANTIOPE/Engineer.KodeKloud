# Task

A Nautilus developer has stored confidential data on the jump host within Stratos DC. To ensure security and compliance, this data must be transferred to one of the app servers. Given developers lack direct access to these servers, the system admin team has been enlisted for assistance.

Copy `/tmp/nautilus.txt.gpg` file from jump server to App Server 2 placing it in the directory `/home/webdata`.

# Solution

1. **SSH into the Jump Host**:

    First, you need to SSH into the jump host using the provided credentials:

    ```bash
    ssh thor@jump_host.stratos.xfusioncorp.com
    ```

2. **Securely Copy the File to App Server 2**:

    Use the `scp` (secure copy) command to transfer the file from the jump host to App Server 2. The `scp` command will securely transfer files between hosts on a network.

    ```bash
    scp /tmp/nautilus.txt.gpg steve@172.16.238.11:/home/webdata/
    ```

    Explanation:
    - `scp`: Command to securely copy files between hosts.
    - `/tmp/nautilus.txt.gpg`: Source file on the jump host.
    - `steve@172.16.238.11:/home/webdata/`: Destination path on App Server 2. The format is `user@hostname:/path/to/destination`.

3. **Verify the File on App Server 2**:

    SSH into App Server 2 to verify that the file has been successfully copied:

    ```bash
    ssh steve@172.16.238.11

    ls -l /home/webdata/nautilus.txt.gpg
    ```

   ![image](https://github.com/user-attachments/assets/e55c9091-5222-484d-afcd-4eed7db10bf0)
