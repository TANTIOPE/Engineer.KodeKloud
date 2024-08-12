# Task

An issue has arisen with a static website running in a container named `nautilus` on App Server 1. To resolve the issue, investigate the following details:

- Check if the container's volume `/usr/local/apache2/htdocs` is correctly mapped with the host's volume `/var/www/html`.
- Verify that the website is accessible on host port 8080 on App Server 1. Confirm that the command `curl http://localhost:8080/` works on App Server 1.

# Solution

1. **SSH into App Server 1:**

    Start by logging into App Server 1 (stapp01) using the provided credentials.

    ```bash
    ssh tony@172.16.238.10
    sudo su -
    ```

2. **Check Volume Mapping:**

    Use the `docker inspect` command to verify the volume mapping between the container and the host. This command will provide detailed information about the container's configuration, including volume mounts.

    ```bash
    docker inspect nautilus
    ```

    Look for the `Mounts` section in the output to verify that `/usr/local/apache2/htdocs` in the container is mapped to `/var/www/html` on the host.

   ![image](https://github.com/user-attachments/assets/2cd2d699-8e33-4c27-9829-984e6bddcfb6)


4. **Verify Website Accessibility:**

    Check if the website is accessible on port 8080 by using the `curl` command to make a request to the local server.

    ```bash
    curl http://localhost:8080/
    ```

  ![image](https://github.com/user-attachments/assets/bbe0b513-bcbe-4227-beb6-344ec8779af0)

5. **Try restarting the container and verify:**

  ```bash
  docker restart nautilus
  ```
Check the result: `curl http://localhost:8080/`

![image](https://github.com/user-attachments/assets/f4d7dc29-505d-4df8-a3ec-e04e707ff3b0)
