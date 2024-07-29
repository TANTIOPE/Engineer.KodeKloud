# Task : Disable Direct SSH Root Login

Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.

Disable direct SSH root login on all app servers within the Stratos Datacenter.

# Solution 

- **App Server 1**: `172.16.238.10`
- **App Server 2**: `172.16.238.11`
- **App Server 3**: `172.16.238.12`

### 1. SSH into Each App Server

#### App Server 1

```bash
ssh tony@172.16.238.10
```
### 2. Edit the SSH Configuration File

Open the SSH configuration file /etc/ssh/sshd_config in a text editor:

```bash
sudo nano /etc/ssh/sshd_config
```

Find the line : `#PermitRootLogin yes`

Modify the value to no or without-password. This disables direct root login.

### 3. Restart the SSH Service

To apply the changes, restart the SSH service :

```bash
sudo systemctl restart sshd
```

To verify that root login has been disabled, attempt to SSH into each server as the root user

If correctly configured, you should receive a permission denied error.
