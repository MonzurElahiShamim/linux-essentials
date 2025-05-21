# Changing User Ownership

#### Purpose:
- Use the `chown` command to change the user ownership of files and directories.

#### Requirements:
- Root privileges are required to change the user owner of a file.

## Commands:
- **`chown user /path/to/file`**: Changes the user owner of a file.
- **`chown user:group /path/to/file`** or **`chown user.group /path/to/file`**: Changes both the user and group owners of a file.
- **`chown :group /path/to/file`** or **`chown .group /path/to/file`**: Changes only the group owner of a file.

## Usage Examples:

#### 1. Change User Ownership:
   - Root user changes the user owner of a file to `jane`.
   ```bash
   root@localhost:~# chown jane /tmp/filetest1
   root@localhost:~# ls -l /tmp/filetest1
   -rw-rw-r-- 1 jane sysadmin 0 Dec 19 18:44 /tmp/filetest1
   ```

#### 2. Change Both User and Group Ownership:
   - Root user changes both the user owner to `jane` and the group owner to `users`.
   ```bash
   root@localhost:~# chown jane:users /tmp/filetest2
   root@localhost:~# ls -l /tmp/filetest2
   -rw-r--r-- 1 jane users 0 Dec 19 18:53 /tmp/filetest2
   ```

   - Alternatively, you can use a period to separate the user and group.
   ```bash
   root@localhost:~# chown jane.users /tmp/filetest2
   root@localhost:~# ls -l /tmp/filetest2
   -rw-r--r-- 1 jane users 0 Dec 19 18:53 /tmp/filetest2
   ```

#### 3. Change Only Group Ownership:
   - Regular user changes the group owner of a file.
   ```bash
   jane@localhost:~$ chown :users /tmp/filetest1
   jane@localhost:~$ ls -l /tmp/filetest1
   -rw-rw-r-- 1 jane users 0 Dec 19 18:44 /tmp/filetest1
   ```

   - Alternatively, you can use a period to prefix the group name.
   ```bash
   jane@localhost:~$ chown .users /tmp/filetest1
   jane@localhost:~$ ls -l /tmp/filetest1
   -rw-rw-r-- 1 jane users 0 Dec 19 18:44 /tmp/filetest1
   ```

## Key Points:

- **Root Privileges Required**: Changing the user owner of a file requires root privileges.
- **Changing Group Ownership**: Both root and regular users (if they own the file) can change the group ownership using `chown` or `chgrp`.
- **Ownership Syntax**: Use a colon (`:`) or a period (`.`) to separate the user and group in the `chown` command.
- **Viewing Changes**: Use the `ls -l` command to verify ownership changes.
