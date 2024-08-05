# Task

Within the Stratos DC, the backup server holds template XML files crucial for the Nautilus application. Before utilization, these files require valid data insertion. As part of routine maintenance, system admins at xFusionCorp Industries employ string and file manipulation commands.

Your task is to substitute all occurrences of the string `Sample` with `LUSV` within the XML file located at `/root/nautilus.xml` on the backup server.

# Solution

1. **SSH into the Backup Server**:

    ```bash
    ssh clint@172.16.238.16
    ```

2. **Verify the Content of the File**:

    Before making any changes, it's good practice to verify the content of the file to understand its structure and current data:

    ```bash
    sudo cat /root/nautilus.xml
    ```

    Output :

    ```xml
    <?xml version="1.0"?>
    <catalog>
   <book id="bk101">
    <author>Menon, Vardaan</author>
      <title>Software Development</title>
      <genre>Sample</genre>
      <type>Random</type>
      <about>About</about>
      <price>44.95</price>
      <string>String</string>
      <text>Text</text>
      <publish_date>2000-10-01</publish_date>
      <description>Unknown Description</description>
   </book>

    ```

3. **Substitute All Occurrences of `Sample` with `LUSV`**:

    To substitute all occurrences of the string `Sample` with `LUSV`, use the `sed` command:

    ```bash
    sudo sed -i 's/Sample/LUSV/g' /root/nautilus.xml
    ```

    Explanation:
    - `sed`: Stream editor for filtering and transforming text.
    - `-i`: Edit files in place (i.e., make changes directly to the file).
    - `'s/Sample/LUSV/g'`: Substitute (`s`) all occurrences (`g` for global) of the string `Sample` with `LUSV`.
    - `/root/nautilus.xml`: The target file.

4. **Verify the Changes**:

    After running the `sed` command, verify that the changes were made correctly by displaying the content of the file again:

    ```bash
    cat /root/nautilus.xml
    ```

    Output :

    ```xml
    <?xml version="1.0"?>
    <catalog>
   <book id="bk101">
    <author>Menon, Vardaan</author>
      <title>Software Development</title>
      <genre>LUSV</genre>
      <type>Random</type>
      <about>About</about>
      <price>44.95</price>
      <string>String</string>
      <text>Text</text>
      <publish_date>2000-10-01</publish_date>
      <description>Unknown Description</description>
   </book>
    ```
