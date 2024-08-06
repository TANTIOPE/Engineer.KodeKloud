# Task

With the installation of new tools on the app servers within the Stratos Datacenter, certain functionalities now necessitate graphical user interface (GUI) access.

Adjust the default runlevel on all App servers in Stratos Datacenter to enable GUI booting by default. It's imperative not to initiate a server reboot after completing this task.

# Steps and Solution

1. **SSH into each App Server**:

    ```bash
    ssh tony@172.16.238.10  # For App Server 1
    ssh steve@172.16.238.11 # For App Server 2
    ssh banner@172.16.238.12 # For App Server 3
    ```

2. **Check the Current Runlevel**:

    ```bash
    sudo systemctl get-default
    ```

    This command checks the current default runlevel, `graphical.target` for GUI mode or `multi-user.target` for non-GUI mode
   
4. **Set the Default Runlevel to GUI**:

    ```bash
    sudo systemctl set-default graphical.target
    ```

    This command sets the default runlevel to GUI mode without rebooting the server.
    By changing the default target to `graphical.target`, the system will boot into the graphical user interface (GUI) by default when it starts up

6. **Verify the Changes**:

    ```bash
    sudo systemctl get-default
    ```

    This command verifies that the default runlevel has been changed to `graphical.target`.


