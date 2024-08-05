# Task

In alignment with security compliance standards, the Nautilus project team has opted to impose restrictions on crontab access. Specifically, only designated users will be permitted to create or update cron jobs.

Configure crontab access on App Server 2 as follows: Allow crontab access to the `mark` user while denying access to the `jerome` user.

# Solution

1. **SSH into App Server 2**:

    First, you need to SSH into App Server 2 using the provided credentials:

    ```bash
    ssh steve@172.16.238.11
    ```

2. **Edit the Crontab Access Files**:

    To configure crontab access, you will need to edit the `/etc/cron.allow` and `/etc/cron.deny` files.

    - **Allow crontab access to the `mark` user**:

      Add the `mark` user to the `/etc/cron.allow` file. This file specifies which users are allowed to use cron.

      ```bash
      echo "mark" | sudo tee -a /etc/cron.allow
      ```

      Explanation:
      - `echo "mark"`: This command outputs the string "mark".
      - `| sudo tee -a /etc/cron.allow`: This appends the string "mark" to the `/etc/cron.allow` file with root privileges.

    - **Deny crontab access to the `jerome` user**:

      Add the `jerome` user to the `/etc/cron.deny` file. This file specifies which users are denied access to cron.

      ```bash
      echo "jerome" | sudo tee -a /etc/cron.deny
      ```

      Explanation:
      - `echo "jerome"`: This command outputs the string "jerome".
      - `| sudo tee -a /etc/cron.deny`: This appends the string "jerome" to the `/etc/cron.deny` file with root privileges.

3. **Verify the Configuration**:

    To verify that the configurations have been applied correctly, you can check the contents of the `/etc/cron.allow` and `/etc/cron.deny` files.

    - Check `/etc/cron.allow`:

      ```bash
      cat /etc/cron.allow
      ```

    - Check `/etc/cron.deny`:

      ```bash
      cat /etc/cron.deny
      ```
