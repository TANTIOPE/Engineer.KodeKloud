# Task

In the daily standup, it was noted that the timezone settings across the Nautilus Application Servers in the Stratos Datacenter are inconsistent with the local datacenter's timezone, currently set to `Asia/Kabul`.

Synchronize the timezone settings to match the local datacenter's timezone (`Asia/Kabul`).

# Steps and Solution

1. **SSH into Each App Server**:

    ```bash
    ssh tony@172.16.238.10  # For App Server 1
    ssh steve@172.16.238.11 # For App Server 2
    ssh banner@172.16.238.12 # For App Server 3
    ```

2. **Check the Current Timezone**:

    ```bash
    timedatectl
    ```
    ![image](https://github.com/user-attachments/assets/e5a097b3-5e98-40e8-a7ed-da119dfb3448)

    This command displays the current date, time, and timezone settings of the server.

3. **Set the Timezone to Asia/Kabul**:

    ```bash
    sudo timedatectl set-timezone Asia/Kabul
    ```

    This command sets the server's timezone to `Asia/Kabul`.

4. **Verify the Timezone Change**:

    ```bash
    timedatectl
    ```
    
    ![image](https://github.com/user-attachments/assets/c3a0afd4-d218-4859-8ce3-ea77647e16df)


