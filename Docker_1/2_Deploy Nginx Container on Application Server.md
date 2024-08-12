# Task

The Nautilus DevOps team is conducting application deployment tests on selected application servers. They require a `nginx` container deployment on Application Server 3. Complete the task with the following instructions:

- On Application Server 3, create a container named `nginx_3` using the `nginx:alpine` image.
- Ensure the container is in a running state.

# Solution

1. **SSH into Application Server 3:**

    Start by logging into Application Server 3 (stapp03) using the provided credentials.

    ```bash
    ssh banner@172.16.238.12
    sudo su -
    ```

2. **Pull the Nginx Image:**

    Ensure the `nginx:alpine` image is available locally by pulling it from the Docker registry.

    ```bash
    docker pull nginx:alpine
    ```

3. **Create and Start the Nginx Container:**

    Create and start a new container named `nginx_3` using the pulled image.

    ```bash
    docker run -d --name nginx_3 nginx:alpine
    ```

4. **Verify the Container is Running:**

    Confirm that the container is up and running.

    ```bash
    docker ps
    ```
![image](https://github.com/user-attachments/assets/cb0e9c62-4157-4e15-90ff-282fafb707e8)
