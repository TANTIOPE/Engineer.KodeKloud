# Task

For security reasons the `xFusionCorp Industries` security team has decided to use custom Apache users for each web application hosted, rather than its default user. This will be the Apache user, so it shouldn't use the default home directory. Create the user as per requirements given below:

a. Create a user named `anita` on the `App server 2` in Stratos Datacenter.

b. Set its UID to `1200` and home directory to `/var/www/anita`.


# Solution

ssh into the App Server 2 (stapp02) : `ssh steve@172.16.238.11`

This command creates a new user with the username "anita", sets the UID to 1200, creates the home directory `/var/www/anita`, and the `-m` option ensures that the home directory is created: `sudo useradd -u 1582 -d /var/www/anita -m anita` 

To check if the user "anita" was created successfully, you can use the following command: `id anita`

Running this command will display information about the user "anita", including the UID, GID (group ID), and the groups the user belongs to. If the user was created successfully, you will see output similar to the following:


