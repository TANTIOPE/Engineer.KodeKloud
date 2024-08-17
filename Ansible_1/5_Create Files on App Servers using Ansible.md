# Task

The Nautilus DevOps team is testing various Ansible modules on servers in `Stratos DC`. They're currently focusing on file creation on remote hosts using `Ansible`. Here are the details:

a. Create an inventory file `~/playbook/inventory` on the `jump host` and include all `app servers`.

b. Create a playbook `~/playbook/playbook.yml` to create a blank file `/usr/src/nfsdata.txt` on all `app servers`.

c. Set the permissions of the `/usr/src/nfsdata.txt` file to `0644`.

d. Ensure the user/group owner of the `/usr/src/nfsdata.txt` file is `tony` on `app server 1`, `steve` on `app server 2`, and `banner` on `app server 3`.

**Note:** Validation will execute the playbook using the command `ansible-playbook -i inventory playbook.yml`, so ensure the playbook functions correctly without any additional arguments.

# Steps and Solution

1. **Create the Inventory File**:

    Create an inventory file at `~/playbook/inventory` on the `jump host` and include all `app servers`.

    ```ini
    [app_servers]
    stapp01 ansible_host=172.16.238.10 ansible_ssh_pass=Ir0nM@n ansible_user=tony
    stapp02 ansible_host=172.16.238.11 ansible_ssh_pass=Am3ric@ ansible_user=steve
    stapp03 ansible_host=172.16.238.12 ansible_ssh_pass=BigGr33n ansible_user=banner
    ```

2. **Create the Playbook**:

    Create the playbook at `~/playbook/playbook.yml` to create a blank file `/usr/src/nfsdata.txt` on all `app servers`.

    ```yaml
    ---
    - name: Create and set permissions on /usr/src/nfsdata.txt
      hosts: app_servers
      become: true
      tasks:
        - name: Create a blank file /usr/src/nfsdata.txt
          file:
            path: /usr/src/nfsdata.txt
            state: touch
            mode: '0644'
            owner: "{{ ansible_ssh_user }}"
            group: "{{ ansible_ssh_user }}"
    ```

    - `name`: Describes the purpose of the playbook.
    - `hosts: app_servers`: Specifies that the playbook will run on all servers listed under the `app_servers` group in the inventory.
    - `become: true`: Ensures that tasks are executed with elevated privileges (sudo).
    - `tasks`: Lists the tasks to be executed.
    - `file`: Ansible module used to manage files on remote hosts.
    - `path`: Specifies the file path on the remote host.
    - `state: touch`: Creates the file if it does not exist.
    - `mode: '0644'`: Sets file permissions to `0644`.
    - `owner` and `group`: Set the file owner and group to the SSH user specified in the inventory.

3. **Run the Playbook**:

    Validate the playbook using the command:

    ```bash
    ansible-playbook -i playbook/inventory playbook/playbook.yml
    ```

    - `-i`: Specifies the inventory file to use, containing the list of hosts and their connection details.
