# Task

The Nautilus DevOps team aims to manage all servers within the stack using Ansible, utilizing a common sudo user across all servers. They plan to use this user for various tasks on each server. While this isn't finalized, they're starting with testing. Ansible is already installed on the jump host via `yum`. Here's the requirement:

On the jump host, modify the default configuration of Ansible to enable the use of `james` as the default SSH user for all hosts. Ensure to make changes within Ansible's default configuration without creating a new one.

# Steps and Solution

1. **Locate the Default Ansible Configuration File**:

    The default Ansible configuration file is typically located at `/etc/ansible/ansible.cfg`. Open this file for editing.

    ```bash
    sudo vi /etc/ansible/ansible.cfg
    ```

2. **Modify the SSH User Setting**:

    Find the line that specifies the `remote_user` parameter under the `[defaults]` section. Uncomment this line (if it's commented) and set it to `james`.

    ```ini
    [defaults]
    # some other configurations...

    remote_user = james
    ```

    - `remote_user = james`: Sets `james` as the default SSH user for all hosts when running Ansible playbooks.

3. **Save and Exit**:

    Save the changes and exit the editor. The Ansible configuration now uses `james` as the default SSH user for all tasks.

