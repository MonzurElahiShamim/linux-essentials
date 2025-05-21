# Changing Groups

>[!info] `newgrp` (To create new file with different group ownership)

**Purpose:**
- Change the group ownership of a file if it should belong to a group different from your *current primary group*.

**Commands:**
- **`newgrp group_name`**: Changes your current primary group.
- **`id`**: Lists your identity information, including group memberships.
- **`groups`**: Lists all groups you belong to.

**Steps to Change Groups:**

1. **List Current Groups:**
   ```bash
   sysadmin@localhost:~$ groups
   sysadmin adm sudo research development
   ```

2. **Verify Current Primary Group:**
   ```bash
   sysadmin@localhost:~$ id
   uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),4(adm),27(sudo),1005(research),1006(development)
   ```

3. **Change Primary Group Using `newgrp`:**
   ```bash
   sysadmin@localhost:~$ newgrp research
   ```

4. **Verify New Primary Group:**
   ```bash
   sysadmin@localhost:~$ id
   uid=1001(sysadmin) gid=1005(research) groups=1005(research),4(adm),27(sudo),1001(sysadmin),1006(development)
   ```

5. **Create a File with New Group Ownership:**
   ```bash
   sysadmin@localhost:~$ touch /tmp/filetest2
   sysadmin@localhost:~$ ls -l /tmp/filetest2
   -rw-r--r--. 1 sysadmin research 0 Oct 21 10:53 /tmp/filetest2
   ```

6. **Exit the `newgrp` Shell to Return to Original Group:**
   ```bash
   sysadmin@localhost:~$ exit
   exit
   sysadmin@localhost:~$ id
   uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),4(adm),27(sudo),1005(research),1006(development)
   ```

**Considerations:**
- The `newgrp` command opens a new shell. The primary group stays changed as long as you are in this shell. Use the `exit` command to return to the original primary group.
- **Administrative Privileges:** Required to permanently change a user's primary group using:
  ```bash
  root@localhost:~# usermod -g groupname username
  ```

By following these steps, you can ensure that files are created with the appropriate group ownership, facilitating proper access and permissions management within your system.