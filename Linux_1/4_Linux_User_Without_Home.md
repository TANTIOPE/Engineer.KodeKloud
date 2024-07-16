# Task 

In response to the latest tool implementation at xFusionCorp Industries, the system admins require the creation of a service user account. Here are the specifics :

Create a user named `kirsty` in `App Server 3` without a home directory.

# Solution

ssh into the App Server 3 : `ssh banner@172.16.238.12`

Run the following command to create the user "kirsty" without a home directory: `sudo useradd --no-create-home kirsty`

The `--no-create-home` option ensures that a home directory is not created during the user creation process.

To check if the user was created: `grep "^kirsty:" /etc/passwd` or simply : `getent passwd kirsty` 
