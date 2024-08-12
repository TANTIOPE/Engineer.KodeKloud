# Task

The Nautilus DevOps team aims to containerize various applications following a recent meeting with the application development team. They intend to conduct testing with the following steps:

- Install `docker-ce` and `docker-compose` packages on App Server 2.
- Initiate the Docker service.

# Steps and Solution

1. **SSH into App Server 2:**

    Start by logging into App Server 2 using the provided credentials.

    ```bash
    ssh steve@172.16.238.11
    ```

2. **Install Prerequisite Packages:**

    First, install the prerequisite packages required for Docker.

    ```bash
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    ```

    - These packages provide the necessary tools and dependencies for managing the Docker repository and storage.

3. **Set Up the Docker Repository:**

    Add the Docker CE repository to your system to install Docker.

    ```bash
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    ```

    - This command configures the YUM package manager to use the official Docker repository.

4. **Install Docker CE and Docker Compose:**

    Now install Docker CE (Community Edition) and Docker Compose.

    ```bash
    sudo yum install -y docker-ce docker-compose
    ```

    - `docker-ce`: Installs the Docker engine.
    - `docker-compose`: Installs the tool to define and run multi-container Docker applications.

5. **Start and Enable Docker Service:**

    Once Docker is installed, start the Docker service and enable it to start at boot.

    ```bash
    sudo systemctl start docker
    sudo systemctl enable docker
    ```

    - `systemctl start docker`: Starts the Docker service.
    - `systemctl enable docker`: Ensures Docker starts automatically on system boot.

6. **Verify Docker Installation:**

    Confirm that Docker is running and correctly installed.

    ```bash
    sudo systemctl status docker
    docker --version
    #[root@stapp02 steve]# docker --version
    #Docker version 27.1.1, build 6312585
    docker-compose --version
    ```

    - The `status` command should show that Docker is active and running.
    - The `--version` commands confirm the installed versions of Docker and Docker Compose.
   
    ![image](https://github.com/user-attachments/assets/14bded90-e8e7-42e9-ac39-6a4f4cfd2931)
