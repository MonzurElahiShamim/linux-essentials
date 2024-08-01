---
updated_at: 2024-07-07T14:41:38.395+06:00
edited_seconds: 140
aliases:
  - cut command
  - Filter File Sections
tags:
  - Linux
---
# Filter File Sections

The `cut` command can extract columns of text from a file or standard input. It’s primarily used for working with delimited database files. Again, delimited files are files that contain columns separated by a delimiter. These files are very common on Linux systems.

By default, the `cut` command expects its input to be separated by the tab character, but the `-d` option can specify alternative delimiters such as the colon or comma.

The `-f` option can specify which fields to display, either as a hyphenated range or a comma-separated list.

```bash
sysadmin@localhost:~$ cat mypasswd                                           
root:x:0:0:root:/root:/bin/bash                                              
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin                              
bin:x:2:2:bin:/bin:/usr/sbin/nologin                                         sys:x:3:3:sys:/dev:/usr/sbin/nologin                                         sync:x:4:65534:sync:/bin:/bin/sync
```
In the following example, the first, fifth, sixth and seventh fields from the `mypasswd` database file are displayed:

```bash
sysadmin@localhost:~$ cut -d: -f1,5-7 mypasswd
root:root:/root:/bin/bash
daemon:daemon:/usr/sbin:/usr/sbin/nologin
bin:bin:/bin:/usr/sbin/nologin
sys:sys:/dev:/usr/sbin/nologin
sync:sync:/bin:/bin/sync
```

The `cut` command is also able to extract columns of text based upon character position with the `-c` option—useful when working with fixed-width database files or command outputs.

For example, the fields of the `ls -l` command are always in the same character positions. The following will display just the file type (character 1), permissions (characters 2-10), a space (character 11), and filename (characters 50+):

```bash
sysadmin@localhost:~$ ls -l | cut -c1-11,50-
total 44
drwxr-xr-x Desktop
drwxr-xr-x Documents
drwxr-xr-x Downloads
drwxr-xr-x Music
drwxr-xr-x Pictures
drwxr-xr-x Public
drwxr-xr-x Templates
drwxr-xr-x Videos
-rw-rw-r-- all.txt
-rw-rw-r-- example.txt
-rw-rw-r-- mypasswd
-rw-rw-r-- new.txt
```

