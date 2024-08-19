# Task

The Nautilus team is integrating `Jenkins` into their CI/CD pipelines. After setting up a new `Jenkins` server, they're now configuring user access for the development team. Follow these steps:

1. Click on the `Jenkins` button on the top bar to access the `Jenkins UI`. Login with username `admin` and password `Adm!n321`.

2. Create a Jenkins user named `mariyam` with the password `ksH85UJjhb`. Their full name should match `Mariyam`.

3. **Install the `Project-based Matrix Authorization Strategy` Plugin**:
    - Navigate to **Manage Jenkins** > **Manage Plugins**.
    - Go to the **Available** tab and search for `Project-based Matrix Authorization Strategy`.
    - Check the box next to the plugin and click **Install without restart**.

4. Utilize the `Project-based Matrix Authorization Strategy` to assign overall read permission to the `mariyam` user.

5. Remove all permissions for `Anonymous` users (if any), ensuring that the `admin` user retains overall `Administer` permissions.

6. For the existing job, grant `mariyam` user only read permissions, disregarding other permissions such as `Agent`, `SCM`, etc.

# Steps and Solution

1. **Login to Jenkins**:

    - Access the `Jenkins UI` by clicking on the `Jenkins` button on the top bar.
    - Use the following credentials to log in:
      - Username: `admin`
      - Password: `Adm!n321`

2. **Create the `mariyam` User**:

    - Navigate to **Manage Jenkins** > **Manage Users**.
    - Click **Create User**.
    - Enter the following details:
      - Username: `mariyam`
      - Password: `ksH85UJjhb`
      - Confirm Password: `ksH85UJjhb`
      - Full Name: `Mariyam`
    - Click **Create User** to save.

3. **Install the `Project-based Matrix Authorization Strategy` Plugin**:

    - Go to **Manage Jenkins** > **Manage Plugins**.
    - Under the **Available** tab, search for `Project-based Matrix Authorization Strategy`.
    - Install the plugin by checking the box and selecting **Install without restart**.

    ![image](https://github.com/user-attachments/assets/d3e4b3cd-9219-468c-a850-c298e1a89ab7)

4. **Assign Permissions Using Project-based Matrix Authorization Strategy**:

    - Go to **Manage Jenkins** > **Security**
    - Under **Authorization**, select **Project-based Matrix Authorization Strategy**.
    - For the `mariyam` user, check the box under `Overall` for `Read` permissions.
      
    ![image](https://github.com/user-attachments/assets/35a26106-1bd3-4d8d-9cae-cd1c5af1e917)


5. **Remove Permissions for Anonymous Users**:

    - In the **Project-based Matrix Authorization Strategy** section:
      - Remove all permissions for the `Anonymous` user by unchecking all boxes.
      - Ensure the `admin` user retains `Overall Administer` permissions by checking the appropriate box.

6. **Grant Read Permission to `mariyam` for the Existing Job**:

    - Navigate to the existing Jenkins job.
    - Go to **Configure** > **Build Triggers**.
    - Under the **Project-based Matrix Authorization Strategy** for the job:
      - Add the `mariyam` user.
      - Check only the `Read` box under the `Job` section for the `mariyam` user.
      - Ensure that other permissions like `Agent`, `SCM`, etc., remain unchecked.
