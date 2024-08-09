# Task

Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App Server 3 in the Stratos Datacenter:

- Install the required SELinux packages.
- Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
- No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
- Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

# Steps and Solution

1. **SSH into App Server 3:**

    Start by logging into App Server 3 using the provided credentials.

    ```bash
    ssh banner@172.16.238.12
    ```

2. **Install SELinux Packages:**

    Install the required SELinux packages on the server. This ensures SELinux is available for future use and configuration.

    ```bash
    sudo yum install -y selinux-policy selinux-policy-targeted
    ```

    - `yum install -y selinux-policy selinux-policy-targeted`: The `-y` option automatically confirms the installation, and the command installs the SELinux policies necessary for enforcing security policies.

3. **Permanently Disable SELinux:**

    Modify the SELinux configuration file to disable SELinux permanently. This change will take effect after the next reboot.

    ```bash
    sudo nano /etc/selinux/config
    ```

    Locate the line:

    ```bash
    SELINUX=enforcing
    ```

    Change it to:

    ```bash
    SELINUX=disabled
    ```

    - `SELINUX=disabled`: This setting in the `/etc/selinux/config` file ensures that SELinux is disabled on the next reboot.

4. **Verify the Change:**

    Confirm that the SELinux configuration has been updated correctly.

    ```bash
    cat /etc/selinux/config
    ```
![image](https://github.com/user-attachments/assets/ac619ec5-7251-4c45-9896-e23868dff65d)


### Explanation

- **SSH into App Server 3:** Securely connect to the server where the configuration needs to be applied.
- **Install SELinux Packages:** Ensure that the SELinux packages are installed, preparing the system for future SELinux enforcement.
- **Permanently Disable SELinux:** Edit the configuration file to disable SELinux permanently. The change will take effect after the next reboot.
- **Verify the Change:** Use the `cat` command to verify that the configuration file has been updated as required.
