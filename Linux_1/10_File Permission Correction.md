# Task

After conducting a security audit within the Stratos DC, the Nautilus security team discovered misconfigured permissions on critical files. To address this, corrective actions are being taken by the production support team. Specifically, the file named `/etc/hostname` on Nautilus App 2 server requires adjustments to its Access Control Lists (ACLs) as follows:

1. The file's user owner and group owner should be set to `root`.
2. Others should possess read-only permissions on the file.
3. User `ammar` must not have any permissions on the file.
4. User `ryan` should be granted read-only permission on the file.

# Solution

1. **SSH into App Server 2**:

    ```bash
    ssh steve@172.16.238.11
    ```

2. **Check ACL of the file**:

    ```bash
    getfacl /etc/hostname
    ```

![image](https://github.com/user-attachments/assets/d8f996c9-63d1-46e1-8de3-1ce87f75a3fd)


    - `# owner: root`: Indicates the owner of the file is the root user.
    - `# group: root`: Indicates the group owner of the file is the root group.
    - `user::rw-`: Represents the permissions for the file owner (root). `rw-` means read and write permissions.
    - `group::r--`: Represents the permissions for the group owner (root). `r--` means read-only permissions.
    - `other::r--`: Represents the permissions for other users. `r--` means read-only permissions.

3. **Set User Owner and Group Owner to `root`**:

    To ensure that the user owner and group owner of the file are set to `root`, run the following command:

    ```bash
    sudo chown root:root /etc/hostname
    ```

4. **Set Read-Only Permissions for Others**:

    To ensure that others have read-only permissions on the file, run the following command:

    ```bash
    sudo chmod o=r /etc/hostname
    ```

5. **Remove All Permissions for User `ammar`**:

    To modify the access control list (ACL) and set permissions for the user "ammar" to have no access on the file, run the following command:

    ```bash
    sudo setfacl -m u:ammar:--- /etc/hostname
    ```

6. **Grant Read-Only Permission to User `ryan`**:

    To grant read-only permission to user "ryan", run the following command:

    ```bash
    sudo setfacl -m u:ryan:r-- /etc/hostname
    ```

7. **Verify the Result**:

    Finally, to verify the ACLs, run the following command:

    ```bash
    getfacl /etc/hostname
    ```
![image](https://github.com/user-attachments/assets/b8d8cd95-73b0-4605-b8d5-2b96369852e4)
