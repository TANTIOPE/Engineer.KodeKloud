# Task

Due to an accidental data mix-up, user data was unintentionally mingled on Nautilus App Server 2 at the /home/usersdata location by the Nautilus production support team in Stratos DC. To rectify this, specific user data needs to be filtered and relocated. Here are the details:

Locate all files (excluding directories) owned by user john within the /home/usersdata directory on App Server 2. Copy these files while preserving the directory structure to the /official directory.

# Solution

1. **SSH into App Server 2**:

    ```bash
    ssh steve@172.16.238.11
    ```

2. **Locate Files Owned by `john`**:

    ```bash
    sudo find /home/usersdata -type f -user john
    ```
    Use the `find` command to identify all files owned by the user `john` in the `/home/usersdata` directory.

  
3. **Copy Files to `/official` Directory While Preserving Directory Structure**:

    - Create the `/official` directory if it doesn’t already exist:

        ```bash
        sudo mkdir -p /official
        ```

    - Use the `find` command with `-exec` to copy the files while preserving their directory structure:

        ```bash
        sudo find /home/usersdata -type f -user john -exec cp --parents {} /official \;
        ```
        Use the `cp --parents` command within the `find` command to copy the identified files to the `/official` directory, preserving their directory structure.

4. **Verify the Result**:

    - List Files in `/official` Directory to ensure they have been copied correctly:

        ```bash
        sudo ls -R /official
        ```
        This command will recursively list all files and directories in /official, allowing you to verify that the directory structure has been preserved and the files owned by john are present.
      
