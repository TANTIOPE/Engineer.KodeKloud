# Task

The Nautilus system admins team has rolled out a web UI application for their backup utility on the Nautilus backup server within the Stratos Datacenter. This application operates on port `8085`, and `firewalld` is active on the server. To meet operational needs, the following requirements have been identified:

- Allow all incoming connections on port `8085/tcp`.
- Ensure the zone is set to `public`.

# Steps and Solution

1. **SSH into the Backup Server**:

    ```bash
    ssh clint@172.16.238.16
    ```

2. **Allow Incoming Connections on Port 8085/tcp**:

    ```bash
    sudo firewall-cmd --zone=public --add-port=8085/tcp --permanent
    ```

    - `--zone=public`: Specifies the zone to which the rule should be added.
    - `--add-port=8085/tcp`: Allows incoming TCP traffic on port 8085.
    - `--permanent`: Ensures the rule persists across firewall reloads and reboots.

3. **Reload the Firewall to Apply Changes**:

    ```bash
    sudo firewall-cmd --reload
    ```

    This command reloads the firewall settings to apply the newly added rule.

4. **Verify the Port is Open**:

    ```bash
    sudo firewall-cmd --zone=public --query-port=8085/tcp
    ```

    This command checks if the port `8085/tcp` has been successfully opened in the `public` zone. The expected output should be `yes`.

   ![image](https://github.com/user-attachments/assets/2534b6f7-7fe5-48e0-955a-cae1d0b988d3)
