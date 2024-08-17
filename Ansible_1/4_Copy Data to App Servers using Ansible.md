# Task

The Nautilus DevOps team needs to copy data from the `jump host` to all `application servers` in `Stratos DC` using Ansible. Execute the task with the following details:

a. Create an inventory file `/home/thor/ansible/inventory` on the `jump host` and add all `application servers` as managed nodes.

b. Create a playbook `/home/thor/ansible/playbook.yml` on the `jump host` to copy the `/usr/src/itadmin/index.html` file to all `application servers`, placing it at `/opt/itadmin`.

**Note:** Validation will run the playbook using the command `ansible-playbook -i inventory playbook.yml`. Ensure the playbook functions properly without any extra arguments.

# Steps and Solution

1. **Create the Inventory File**:

    Create an inventory file at `/home/thor/ansible/inventory` on the `jump host` and add all `application servers` as managed nodes.

    ```ini
    [app_servers]
    stapp01 ansible_host=172.16.238.10 ansible_ssh_pass=Ir0nM@n ansible_user=tony
    stapp02 ansible_host=172.16.238.11 ansible_ssh_pass=Am3ric@ ansible_user=steve
    stapp03 ansible_host=172.16.238.12 ansible_ssh_pass=BigGr33n ansible_user=banner
    ```

2. **Create the Playbook**:

    Create the playbook at `/home/thor/ansible/playbook.yml` to copy the `/usr/src/itadmin/index.html` file from the `jump host` to all `application servers`, placing it at `/opt/itadmin`.

    ```yaml
    ---
    - name: Copy index.html to all app servers
      hosts: app_servers
      become: true
      tasks:
        - name: Copy index.html file
          copy:
            src: /usr/src/itadmin/index.html
            dest: /opt/itadmin/
    ```

    - `hosts: app_servers`: Specifies that the playbook will run on all servers listed under the `app_servers` group in the inventory.
    - `become: true`: Ensures that the task is executed with elevated privileges (sudo).
    - `copy`: This Ansible module is used to copy files from the local system (`jump host`) to the remote hosts.

3. **Run the Playbook**:

    Validate the playbook using the command:

    ```bash
    ansible-playbook -i /home/thor/ansible/inventory /home/thor/ansible/playbook.yml
    ```

    - `-i` Specifies the inventory file to use, containing the list of hosts and their connection details.

  ![image](https://github.com/user-attachments/assets/a6718ce1-d573-4aa0-b00e-b5d5939ef252)


