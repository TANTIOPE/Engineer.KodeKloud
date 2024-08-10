# Task

The DevOps team established a new Git repository last week, which remains unused at present. However, the Nautilus application development team now requires a copy of this repository on the Storage Server in the Stratos DC. Follow the provided details to clone the repository:

- The repository to be cloned is located at `/opt/games.git`.
- Clone this Git repository to the `/usr/src/kodekloudrepos` directory. Ensure no modifications are made to the repository during the cloning process.

# Steps and Solution

1. **SSH into the Storage Server:**

    Start by logging into the Storage Server using the provided credentials.

    ```bash
    ssh natasha@172.16.238.15
    ```

2. **Clone the Git Repository:**

    Use the `git clone` command to copy the repository from `/opt/games.git` to `/usr/src/kodekloudrepos`. This will create a new directory for the repository and copy all contents to it.

    ```bash
    sudo git clone /opt/games.git /usr/src/kodekloudrepos
    ```

    - `git clone /opt/games.git /usr/src/kodekloudrepos`: This command clones the repository from the specified source to the destination directory. The repository is copied exactly as it is, ensuring no modifications to its content.

![image](https://github.com/user-attachments/assets/b5b14e8c-dcdc-443d-a1b8-d02adb495dca)
