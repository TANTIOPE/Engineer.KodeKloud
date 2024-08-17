# Task

The Nautilus DevOps team is testing Ansible playbooks on various servers within their stack. They've placed some playbooks under `/home/thor/playbook/` directory on the jump host and now intend to test them on App Server 3 in Stratos DC. However, an inventory file needs creation for Ansible to connect to the respective app. Here are the requirements:

a. Create an ini type Ansible inventory file `/home/thor/playbook/inventory` on the jump host.

b. Include App Server 3 in this inventory along with necessary variables for proper functionality.

c. Ensure the inventory hostname corresponds to the server name as per the wiki, for example `stapp01` for App Server 1 in Stratos DC.

**Note:** Validation will execute the playbook using the command `ansible-playbook -i inventory playbook.yml`. Ensure the playbook functions properly without any extra arguments.

# Steps and Solution

1. **Create the Inventory File**:

    Create an ini type Ansible inventory file at `/home/thor/playbook/inventory` on the jump host.

    ```bash
    touch /home/thor/playbook/inventory
    ```

2. **Include App Server 3 in the Inventory**:

    Edit the inventory file to include App Server 3.

    ```ini
    [app_servers]
    stapp03 ansible_host=172.16.238.12 ansible_ssh_pass=BigGr33n ansible_user=banner
    ```

3. **Run the Playbook**:

    Validate the playbook using the command:

    ```bash
    ansible-playbook -i /home/thor/playbook/inventory /home/thor/playbook/playbook.yml
    ```

    - `-i` specifies the inventory file to use, containing the list of hosts and their connection details.

   ![image](https://github.com/user-attachments/assets/e3450aa9-0864-4ebe-8130-660ebdb6e770)

