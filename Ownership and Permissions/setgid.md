---
updated_at: 2024-08-29T22:20:56.046+06:00
edited_seconds: 150
---

View the permissions on the `/usr/bin/wall` command:

`ls -l /usr/bin/wall`

The output now shows the `s` in the execute column for the group:
```bash
sysadmin@localhost:~$ ls -l /usr/bin/wall                                
-rwxr-sr-x 1 root tty 30800 Sep 16  2020 /usr/bin/wall                   
sysadmin@localhost:~$
```

The `s` in the group execute column indicates that this file has the setgid permission set, so it executes as the group that owns it (`tty`) instead of the group of the user running the command. Thus, the `wall` command is able to write to all terminals (`ttys`) as it executes as the `tty` group.

> [!note] Note
> This is very similar to the setuid permission, but instead of running the command as the user owner of the program, the command runs as the group owner of the program.


> [!tip] Consider this
> So far, you've seen three types of special permissions: sticky bit on a directory, setuid on an executable file and setgid on an executable file. As you have seen, these three types exist on a typical system.
> 
> One more special permission type can be used; the setgid permission can also be applied to a directory:
> 
> `drwxrwsrwx. 2 root demo 4096 Oct 30 23:20 /tmp/data`
> 
> If you see the `s` in the execute column for the group that owns directory, then the directory has the setgid permission. When a directory has the setgid permission, then any new file or directory created in that directory will automatically be owned by the group that owns the directory, not by the group of the user who created the file.
Consider This


