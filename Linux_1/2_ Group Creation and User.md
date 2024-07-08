# Task
The system admin team at  `xFusionCorp Industries` has streamlined access management by implementing group-based access control. Here's what you need to do :

a. Create a group named `nautilus_developers` across all App servers within the `Stratos Datacenter`.

b. Add the user `rajesh` into the `nautilus_developers` group on all App servers. If the user doesn't exist, create it as well.

# Solution
![image](https://github.com/TANTIOPE/Engineer.KodeKloud/blob/main/images/image_2024-07-08_164607341.png?raw=true)

ssh into the App Server 1: `ssh tony@172.16.238.10`

ssh into the App Server 2: `ssh steve@172.16.238.11`

ssh into the App Server 3: `ssh banner@172.16.238.12`

To list all existing groups, you can run the command : `getent group` or use `cat`on the `/etc/group` file.

Create the group "nautilus_developers" by running the following command on each App server:  `sudo groupadd nautilus_developers`

To check if the "nautilus_developers" group was created, you can use the following command : `getent group nautilus_developers`

To list all existing users, you can run the command: `getent passwd` or use cat on the `/etc/passwd` file.

Create the user "rajesh" if they don't already exist. Run the following command on each App server: `sudo useradd rajesh`

To check if the user  "rajesh" exists, you can use the following command: `getent passwd rajesh` If the user exists, it will display information about the user, including the username, UID, home directory, and shell.

Add the user "rajesh" to the "nautilus_developers" group on each App server by running the following command: `sudo usermod -aG nautilus_developers rajesh`

- `a`: This option stands for "append" or "add". It is used to add the user to the specified group(s) without removing them from any existing groups. It ensures that the user's current group memberships are preserved while adding the new group.
- `G`: This option specifies the group(s) to which the user should be added. Multiple groups can be specified by separating them with commas. In this case, the group `nautilus_developers` is specified.

![image](https://github.com/TANTIOPE/Engineer.KodeKloud/blob/main/images/2024-07-08%2016_19_35-KodeKloud%20-%20Engineer%20_%20Task%20-%20Opera.png?raw=true)
