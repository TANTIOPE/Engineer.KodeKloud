# Task

The Nautilus development team has provided requirements to the DevOps team for a new application development project, specifically requesting the establishment of a Git repository. Follow the instructions below to create the Git repository on the Storage server in the Stratos DC.

- Utilize `yum` to install the `git` package on the Storage Server.
- Create a bare repository named `/opt/news.git` (ensure exact name usage).

# Steps and Solution

1. **SSH into the Storage Server:**

    Start by logging into the Storage Server using the provided credentials.

    ```bash
    ssh natasha@172.16.238.15
    ```

2. **Install Git Package:**

    Install the required Git package on the server. This ensures that Git is available for repository management.

    ```bash
    sudo yum install -y git
    ```

    - `yum install -y git`: The `-y` option automatically confirms the installation, and the command installs the Git package necessary for repository management.

3. **Create a Bare Git Repository:**

    After installing Git, create the bare repository at the specified location.

    ```bash
    sudo git init --bare /opt/news.git
    ```

    - `git init --bare /opt/news.git`: Initializes a new bare Git repository at `/opt/news.git`. The `--bare` option specifies that this repository will not have a working directory, making it suitable for use as a central repository.

4. **Verify the Repository Creation:**

    Confirm that the repository has been created correctly by listing the contents of the `/opt/` directory.

    ```bash
    ls -ld /opt/news.git
    ```

![image](https://github.com/user-attachments/assets/7f38dca2-b3c8-41db-b8a7-43d5cd9ff92a)
