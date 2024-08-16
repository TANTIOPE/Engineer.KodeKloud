# Task

An Ansible playbook needs completion on the jump host, where a team member left off. Below are the details:

- The inventory file `/home/thor/ansible/inventory` requires adjustments. The playbook must run on App Server 2 in Stratos DC. Update the inventory accordingly.
- Create a playbook `/home/thor/ansible/playbook.yml`. Include a task to create an empty file `/tmp/file.txt` on App Server 2.
- Note: Validation will run the playbook using the command `ansible-playbook -i inventory playbook.yml`. Ensure the playbook works without any additional arguments.

# Steps and Solution

1. **Update the Inventory File**:

    Modify the inventory file located at `/home/thor/ansible/inventory` to include App Server 2 with the following content:

    ```ini
    stapp02 ansible_host=172.16.238.11 ansible_ssh_pass=Am3ric@ ansible_user=steve
    ```

2. **Create the Playbook**:

    Create a new Ansible playbook file at `/home/thor/ansible/playbook.yml` with the following content:

    ```yaml
    ---
    - name: Create empty file on App Server 2
      hosts: stapp02
      become: true
      tasks:
        - name: Create empty file
          file:
            path: /tmp/file.txt
            state: touch
    ```

3. **Run the Playbook**:

    Validate the playbook using the command:

    ```bash
    ansible-playbook -i /home/thor/ansible/inventory /home/thor/ansible/playbook.yml
    ```

  ![image](https://github.com/user-attachments/assets/7dae30ae-7b19-41e5-b40b-a6b5fd68dbce)

