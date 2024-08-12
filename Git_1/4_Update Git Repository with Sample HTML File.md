# Task

The Nautilus development team has initiated a new project development, establishing various Git repositories to manage each project's source code. Recently, a repository named `/opt/blog.git` was created. The team has provided a sample `index.html` file located on the jump host under the `/tmp` directory. This repository has been cloned to `/usr/src/kodekloudrepos` on the storage server in the Stratos DC.

- Copy the sample `index.html` file from the jump host to the storage server, placing it within the cloned repository at `/usr/src/kodekloudrepos/blog`.
- Add and commit the file to the repository.
- Push the changes to the master branch.

# Steps and Solution

1. **SSH into the Jump Host:**

    Start by logging into the Jump Host using the provided credentials.

    ```bash
    ssh thor@jump_host.stratos.xfusioncorp.com
    ```

2. **Copy the `index.html` file from the Jump Host to the Storage Server:**

    Use `scp` to securely transfer the `index.html` file from the jump host to the `/tmp` directory on the storage server.

    ```bash
    scp /tmp/index.html natasha@172.16.238.15:/tmp/
    ```

    - This command transfers the `index.html` file to the `/tmp` directory on the storage server.

3. **SSH into the Storage Server:**

    Log in to the Storage Server to proceed with the file operations.

    ```bash
    ssh natasha@172.16.238.15
    ```

4. **Move the `index.html` File to the Cloned Repository Directory:**

    Copy the `index.html` file from the `/tmp` directory to the cloned repository at `/usr/src/kodekloudrepos/blog`.

    ```bash
    sudo cp /tmp/index.html /usr/src/kodekloudrepos/blog/
    ```

    - This command moves the `index.html` file to the correct location within the repository directory.

5. **Navigate to the Cloned Repository Directory:**

    Change directory to the location where the repository is cloned.

    ```bash
    cd /usr/src/kodekloudrepos/blog
    ```

6. **Add the `index.html` File to the Repository:**

    Add the new `index.html` file to the Git staging area.

    ```bash
    git add index.html
    ```

7. **Commit the Changes:**

    Commit the added file with an appropriate commit message.

    ```bash
    git commit -m "Add index.html to the blog repository"
    ```

8. **Push the Changes to the Master Branch:**

    Push the committed changes to the master branch of the repository.

    ```bash
    git push origin master
    ```

9. **Verify the Push Operation:**

    Check the status to ensure all changes have been successfully pushed.

    ```bash
    git status
    ```
![image](https://github.com/user-attachments/assets/4dccd4a7-64fa-4e1e-8c78-14df7a55102d)
