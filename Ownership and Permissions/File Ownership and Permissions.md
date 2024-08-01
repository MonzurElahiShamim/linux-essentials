---
updated_at: 2024-07-17T12:14:19.248+06:00
edited_seconds: 50
---
# File Ownership and Permissions

**File Ownership:**
- Each file has a user owner and a group owner.
- **User Owner:** Default owner is the user who created the file, identified by UID.
- **Group Owner:** Default group owner is the primary group of the user, identified by GID.

**Key Points:**
- Changing UID or deleting a user can orphan files (shown by numeric UID).
- Similarly, changing GID or deleting a group can orphan files (shown by numeric GID).

**Useful Command:**
- **`id`**: Displays the current user's UID, GID, and group memberships.

**Example of `id` Command Output:**
```bash
sysadmin@localhost:~$ id
uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),4(adm),27(sudo),1005(research),1006(development)
```

**Creating and Listing Files:**
- When a file is created (e.g., using `touch`), it belongs to the user and their primary group.
- **Example:**
  ```bash
  sysadmin@localhost:~$ touch /tmp/filetest1
  ```
- **Confirm Ownership:**
  ```bash
  sysadmin@localhost:~$ ls -l /tmp/filetest1
  -rw-rw-r--. 1 sysadmin sysadmin 0 Oct 21 10:18 /tmp/filetest1
  ```

**Listing Hidden Files:**
- **`ls -a`**: Lists all files including hidden ones (starting with a period `.`).
- **Example:**
  ```bash
  sysadmin@localhost:~$ ls -la
  total 60
  drwxr-xr-x 1 sysadmin sysadmin 4096 Nov  3 22:29 .
  drwxr-xr-x 1 root     root     4096 Mar 14  2016 ..
  -rw-r--r-- 1 sysadmin sysadmin  220 Apr  3  2012 .bash_logout
  -rw-r--r-- 1 sysadmin sysadmin 3768 Mar 14  2016 .bashrc
  drwx------ 2 sysadmin sysadmin 4096 Nov  3 22:29 .cache
  -rw-r--r-- 1 sysadmin sysadmin  675 Apr  3  2012 .profile
  -rw-r--r-- 1 sysadmin sysadmin   74 Mar 14  2016 .selected_editor
  drwxr-xr-x 2 sysadmin sysadmin 4096 Mar 14  2016 Desktop
  drwxr-xr-x 2 sysadmin sysadmin 4096 Mar 14  2016 Documents
  drwxr-xr-x 2 sysadmin sysadmin 4096 Mar 14  2016 Downloads
  ...
  ...
  ```

**Output of `ls -l` Command:**
- **Permissions:** `-rw-rw-r--.` indicates read and write permissions for owner and group, and read-only for others.
- **User Owner:** The user who owns the file (e.g., `sysadmin`).
- **Group Owner:** The group that owns the file (e.g., `sysadmin`).

Understanding file ownership and permissions is crucial for maintaining file security and proper access control within a system.