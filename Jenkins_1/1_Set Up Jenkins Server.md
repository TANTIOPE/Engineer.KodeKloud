# Task

The DevOps team at xFusionCorp Industries is initiating the setup of CI/CD pipelines and has decided to utilize Jenkins as their server. Execute the task according to the provided requirements:

1. Install Jenkins on the Jenkins server using the `yum` utility only, and start its service. You might face a timeout issue while starting the Jenkins service; please refer to the provided link for help.

2. Set up the Jenkins admin user with the following details:
    - Username: `*****`
    - Password: `*****`
    - Full name: `*****`
    - Email: `******`

**Note:**

1. For this task, access the Jenkins server by SSH using the root user and password `S3curePass` from the jump host.

2. After Jenkins installation, click the Jenkins button on the top bar to access the Jenkins UI and follow the on-screen instructions to create an admin user.

# Steps and Solution

1. **SSH into the Jenkins Server:**

    Start by logging into the Jenkins server using the provided credentials.

    ```bash
    ssh root@172.16.238.19
    ```

2. **Install Jenkins:**

    Install Jenkins using the `yum` package manager.

    ```bash
    yum install -y jenkins
    ```

    - `yum install -y jenkins`: The `-y` option automatically confirms the installation, and the command installs the Jenkins package necessary for CI/CD management.

3. **Start and Enable Jenkins Service:**

    Start the Jenkins service and ensure it starts on boot.

    ```bash
    systemctl start jenkins
    systemctl enable jenkins
    ```

    - `systemctl start jenkins`: Starts the Jenkins service immediately.
    - `systemctl enable jenkins`: Enables the Jenkins service to start automatically during system boot.
    - It appeared that the service wouldn't start, so we had to use the following command to check the error :

   ```bash
    journalctl -xeu jenkins.service
    ```
   
  ![image](https://github.com/user-attachments/assets/95b73288-b6d0-4384-8893-37175ba36694)

  - So we installed java :
   ```bash
    sudo yum install java
```
  - And restarted the service with `systemctl restart jenkins`

4. **Set Up Admin User:**

    Access the Jenkins UI and set up the admin user as instructed.

    - Go to the Jenkins URL provided on the server.
    - Follow the on-screen instructions to create the admin user.

  ![image](https://github.com/user-attachments/assets/b2efad0f-fe37-42a1-8a43-d6e37db0ceaa)
  - This command displays the initial administrator password for Jenkins: `cat /var/lib/jenkins/secrets/initialAdminPassword`
    
  ![image](https://github.com/user-attachments/assets/5c16c463-fa7e-440e-9c84-6cea53ed7f68)
