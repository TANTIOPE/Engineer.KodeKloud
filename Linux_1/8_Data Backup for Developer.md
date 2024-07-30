# Task

Within the Stratos DC, the Nautilus storage server hosts a directory named `/data`, serving as a repository for various developers non-confidential data. Developer kareem has requested a copy of their data stored in `/data/kareem`. 
The System Admin team has provided the following steps to fulfill this request :

a. Create a compressed archive named `kareem.tar.gz` of the `/data/kareem` directory.

b. Transfer the archive to the `/home` directory on the Storage Server.

# Solution

### 1. SSH into the Storage Server

```bash
ssh natasha@172.16.238.15
```

### 2. Create the compressed archive

Check the files: `cd /data/kareem` => `ls`

```bash
sudo tar -czvf /data/kareem.tar.gz /data/kareem
```
    -c: Create a new archive.
    -z: Compress the archive using gzip.
    -v: Verbose mode, display the progress and details of the archiving process.
    -f: Specify the name of the archive file.

### 3. Transfer the archive to the /home directory

 ```bash
sudo mv /data/kareem.tar.gz /home/
```
