# Task

Some new requirements have come up to install and configure some packages on the Nautilus infrastructure under `Stratos Datacenter`. The Nautilus DevOps team installed and configured a new `Jenkins` server, so they wanted to create a Jenkins job to automate this task. Find below more details and complete the task accordingly:

1. Access the `Jenkins UI` by clicking on the `Jenkins` button in the top bar. Log in using the credentials: username `admin` and password `Adm!n321`.

2. Create a new Jenkins job named `install-packages` and configure it with the following specifications:

   - Add a string parameter named `PACKAGE`.
   - Configure the job to install a package specified in the `$PACKAGE` parameter on the storage server within the `Stratos Datacenter`.

**Note:**

1. Ensure to install any required plugins and restart the Jenkins service if necessary. Opt for `Restart Jenkins when installation is complete and no jobs are running` on the plugin installation/update page. Refresh the UI page if needed after restarting the service.

2. Verify that the Jenkins job runs successfully on repeated executions to ensure reliability.

3. Capture screenshots of your configuration for documentation and review purposes. Alternatively, use screen recording software like loom.com for comprehensive documentation and sharing.

# Steps and Solution

1. **Install required SSH Plugins**
   
2. **Create SSH credentials for the storage server user**

![image](https://github.com/user-attachments/assets/eea9c36f-2c6e-4b57-8b4f-75102465516a)
![image](https://github.com/user-attachments/assets/37197ac3-abf0-4a5c-bd9b-efbde19879c8)

3. **Add ssh host in Configure System**
   
![image](https://github.com/user-attachments/assets/d2e20398-d3f9-424b-8c14-c06875c39291)

4. **Create the job**
   
![image](https://github.com/user-attachments/assets/37af0e88-7beb-489a-acf8-a49fe996a19a)
![image](https://github.com/user-attachments/assets/2cb7ae50-a79d-4c51-9a9b-2aa3f9c87628)

6. **Run the Job**

![image](https://github.com/user-attachments/assets/b4c9e8d5-1dea-433c-a5ee-00e492116f29)
