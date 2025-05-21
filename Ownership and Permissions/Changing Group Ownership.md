# Changing Group Ownership

>[!info] `chgrp`  (To change the group ownership of existing file)

**Purpose:**
- Change the group owner of an *existing file* using the `chgrp` command.

**Commands:**
- **`chgrp group_name file`**: Changes the group owner of a file.

**Usage:**

1. **Create a Sample File:**
   ```bash
   sysadmin@localhost:~$ touch sample
   sysadmin@localhost:~$ ls -l sample
   -rw-rw-r-- 1 sysadmin sysadmin 0 Oct 23 22:12 sample
   ```

2. **Change Group Ownership to 'research':**
   ```bash
   sysadmin@localhost:~$ chgrp research sample
   sysadmin@localhost:~$ ls -l sample
   -rw-rw-r--. 1 sysadmin research 0 Oct 23 22:12 sample
   ```

3. **Error on Unauthorized Change:**
   - Attempt to change group ownership of a system file without proper permissions results in an error.
   ```bash
   sysadmin@localhost:~$ chgrp development /etc/passwd
   chgrp: changing group of '/etc/passwd': Operation not permitted
   ```

4. **Change Group Ownership Recursively:**
   - Use the `-R` option to change the group ownership of a directory and all its contents.
   ```bash
   sysadmin@localhost:~$ chgrp -R development test_dir
   ```

**Considerations:**

- **Viewing Ownership and Permissions:**
  - The `ls -l` command provides basic information about file ownership.
  - For more detailed information, including group ownership by both name and GID number, use the `stat` command.
  
  ```bash
  sysadmin@localhost:~$ stat /tmp/filetest1
    File: `/tmp/filetest1'
    Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
  Device: fd00h/64768d	Inode: 31477       Links: 1
  Access: (0664/-rw-rw-r--)  Uid: ( 1001/sysadmin)   Gid: ( 1001/sysadmin) 
  Access: 2013-10-21 10:18:02.809118163 -0700
  Modify: 2013-10-21 10:18:02.809118163 -0700
  Change: 2013-10-21 10:18:02.809118163 -0700
  ```

Using these commands and understanding their output allows for effective management of file group ownership in a Linux environment, ensuring proper access and security controls.