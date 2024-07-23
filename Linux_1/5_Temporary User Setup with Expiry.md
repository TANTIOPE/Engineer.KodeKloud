# Task 

As part of the temporary assignment to the `Nautilus` project, a developer named ravi requires access for a limited duration. 
To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do :

Create a user named `ravi` on `App Server 1` in Stratos Datacenter. Set the expiry date to `2024-02-17`, ensuring the user is created in lowercase as per standard protocol.

# Solution

ssh into the App Server 1: `ssh tony@172.16.238.10`

Run the following command to create the user "ravi" with a lowercase username: `sudo useradd --expiredate 2024-02-17 ravi`

To check if the user "ravi" was created, you can use the getent command : `getent passwd ravi` 
If the user exists, the command will return the user entry; otherwise, it will return nothing

To check the expiry date of the user "ravi", you can use the `chage` command: `sudo chage -l ravi`

This command displays the current aging information for the user "ravi", including the expiry date. If the user has an expiry date set, you will see output similar to the following :

[tony@stapp01 ~]$ sudo chage -l ravi

Last password change                : Jul 23, 2024

Password expires                    : never

Password inactive                   : never

Account expires                     : Feb 17, 2024

Minimum number of days between password change          : 0

Maximum number of days between password change          : 99999

Number of days of warning before password expires        : 7
