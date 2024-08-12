# Task

A container named `kke-container` was created by one of the Nautilus project developers on App Server 1. It was solely for testing purposes and now requires deletion. Execute the following task:

- Delete the `kke-container` on App Server 1 in Stratos DC.

# Solution

1. **SSH into App Server 1:**

    Start by logging into App Server 1 (stapp01) using the provided credentials.

    ```bash
    ssh tony@172.16.238.10
    sudo su -
    ```

2. **Stop the Container:**

    Stop the `kke-container` if it is running. Containers must be stopped before they can be removed.

    ```bash
    docker stop kke-container
    ```

3. **Delete the Container:**

    Remove the stopped `kke-container` from the system.

    ```bash
    docker rm kke-container
    ```

    ![image](https://github.com/user-attachments/assets/136cdf0f-375e-4a22-926d-d7b98d16a31c)
