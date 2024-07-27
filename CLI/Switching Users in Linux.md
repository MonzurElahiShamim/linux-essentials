---
updated_at: 2024-07-16T16:54:48.714+06:00
edited_seconds: 170
---
# Switching Users in Linux

The `su` (substitute user) command allows you to run a shell as a different user, commonly used to switch to the root user but also capable of switching to other users.

#### Usage:
```bash
su [options] [username]
```

#### Login Shell Option:
Using the login shell option ensures the new shell is fully configured with the new user's settings. It can be specified in three ways:
```bash
su -
su -l
su --login
```

#### Switching to Root:
If no username is specified, `su` defaults to root:
```bash
su - root
su -
```

#### Example:
1. Switching to root:
```bash
sysadmin@localhost:~$ su -
Password: netlab123
root@localhost:~# id
uid=0(root) gid=0(root) groups=0(root)
```

2. Returning to original user:
```bash
root@localhost:~# exit
logout
sysadmin@localhost:~$ id
uid=1001(sysadmin) gid=1001(sysadmin) groups=1001(sysadmin),4(adm),27(sudo)
    ```

**Note:** You must know the target user's password to switch to their account using `su`.

# Executing Privileged Commands with `sudo`

**Purpose of `sudo`:**
- The `sudo` command allows users to execute commands with the privileges of another user, typically the root user.

**Syntax:**
```
sudo [options] command
```

**Default Behavior:**
- Assumes the root user if no specific user is mentioned.

**Configuration:**
- In some Linux distributions where direct root login or `su` command use is disabled, a user is configured during installation to use `sudo` for administrative tasks.

**Example Without `sudo`:**
```bash
sysadmin@localhost:~$ head /etc/shadow
head: cannot open '/etc/shadow' for reading: Permission denied
```
- Attempting to read a protected file fails due to insufficient permissions.

**Example Using `sudo`:**
```bash
sysadmin@localhost:~$ sudo head /etc/shadow
[sudo] password for sysadmin: netlab123
root:$6$4Yga95H9$8HbxqsMEIBTZ0YomlMffYCV9VE1SQ4T2H3SHXw41M02SQtfAdDVE9mqGp2hr20q.ZuncJpLyWkYwQdKlSJyS8.:16464:0:99999:7:::
...
```
- Prompts for the sysadmin user’s password, not the root’s.
- Grants temporary root privileges to execute the command.

**Security Features:**
- **Password Prompt:** Asks for the user's password, enhancing security.
- **Timeout:** The user won't be asked for the password again if subsequent `sudo` commands are executed within five minutes.
- **Logging:** Commands run with `sudo` are logged with user details, command, and timestamp for accountability.

**Advantages of `sudo`:**
- Reduces the risk of accidental command execution as root.
- Ensures clear intention by requiring the `sudo` prefix for privileged commands.
- Improves security and accountability by logging each administrative action.

**Usage Notes:**
- Users need to be configured with `sudo` privileges.
- Regular commands run without `sudo` execute with the user's regular permissions, reducing the risk of unintended system changes.
