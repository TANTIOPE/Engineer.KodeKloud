# Task
To accommodate the backup agent tool's specifications, the system admin team at xFusionCorp Industries requires the creation of a user with a non-interactive shell. Here's your task :
Create a user named mariyam with a non-interactive shell on App Server 3.

# Solution

A non-interactive shell in Linux is a shell that executes commands without requiring any user interaction.
This type of shell is typically used for running scripts or automated processes. 
Unlike an interactive shell, a non-interactive shell doesn’t prompt the user for input or display output to the user.

SSH into app server 3 : `ssh banner@172.16.238.12`

Run the following command to create the user "mariyam" with a non-interactive shell: `sudo useradd --shell /bin/false mariyam`

This command creates a user named "mariyam" and sets the shell to `/bin/false`, which is a non-interactive shell. Non-interactive shells are typically used for system accounts or accounts that do not require direct login access.

To check if a user named "mariyam" was successfully created on App Server 3, you can use the following command: `id mariyam`

Running this command will display information about the user "mariyam"

![image](https://github.com/TANTIOPE/Engineer.KodeKloud/blob/main/images/2024-07-15%2019_06_05-KodeKloud%20-%20Engineer%20_%20Task%20-%20Opera.png)
