---
updated_at: 2024-08-29T22:13:01.636+06:00
edited_seconds: 80
---

View the permissions of the `/usr/bin/passwd` file:

`ls -l /usr/bin/passwd`

The listing of this file shows:
```bash
sysadmin@localhost:~$ ls -l /usr/bin/passwd                                
-rwsr-xr-x 1 root root 59640 Mar 22  2019 /usr/bin/passwd                
sysadmin@localhost:~$
```

Notice the `s` in the user's execute permission column. This indicates that this file has the setuid permission set, so it executes as the user who owns it (`root`) instead of the user running the command.

Thus, the `passwd` command is able to update the `/etc/shadow` file, as it executes as the `root` user (recall that the `root` user can edit any file, regardless of the permissions on the file).