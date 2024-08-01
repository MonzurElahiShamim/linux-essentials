---
updated_at: 2024-07-17T21:19:45.989+06:00
edited_seconds: 140
---
# Changing Permissions

**`chmod` Command**:
- Used to change file and directory permissions.
- Requires ownership of the file or root access.
- Syntax: `chmod new_permission file_name`

**Example File**:
```bash
root@localhost:~# touch abc.txt
root@localhost:~# ls -l abc.txt                                                 
-rw-r--r-- 1 root root 0 Dec 19 18:58 abc.txt
```

## Symbolic Method:
- Modify specific permissions while leaving others unchanged.
- Specify permission group (`u` for user, `g` for group, `o` for others, `a` for all).
- Use operators (`+` to add, `-` to remove, ` = ` to set).
- Permission types: `r` for read, `w` for write, `x` for execute.

**Examples**:
- Give group owner write permission:
  ```bash
  root@localhost:~# chmod g+w abc.txt
  -rw-rw-r-- 1 root root 0 Dec 19 18:58 abc.txt
  ```
- Add execute for user and group, remove read for others:
  ```bash
  root@localhost:~# chmod ug+x,o-r abc.txt
  -rwxrwx--- 1 root root 0 Dec 19 18:58 abc.txt
  ```
- Set user owner to read and execute only:
  ```bash
  root@localhost:~# chmod u=rx abc.txt
  -r-xrwx--- 1 root root 0 Dec 19 18:58 abc.txt
  ```

## Numeric Method:
- Useful for changing multiple permissions.
- Uses octal values: `4` for read, `2` for write, `1` for execute.
- Combine values for each permission group:
  - `7` = `rwx`
  - `6` = `rw-`
  - `5` = `r-x`
  - `4` = `r--`
  - `3` = `-wx`
  - `2` = `-w-`
  - `1` = `--x`
  - `0` = `---`
- Specify permissions as three numbers, one for each group.

**Example**:
- Set permissions to `rwxr-xr--`:
  ```bash
  root@localhost:~# chmod 754 abc.txt
  -rwxr-xr-- 1 root root 0 Dec 19 18:58 abc.txt
  ```

**Consider Using the stat Command**:
- Provides detailed file information, including symbolic and numeric permissions:
```bash
sysadmin@localhost:~$ stat /tmp/filetest1
File: `/tmp/filetest1'
Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: fd00h/64768d	Inode: 31477       Links: 1
Access: (0664/-rw-rw-r--)  Uid: (  502/sysadmin)   Gid: (  503/sysadmin)
Access: 2013-10-21 10:18:02.809118163 -0700
Modify: 2013-10-21 10:18:02.809118163 -0700
Change: 2013-10-21 10:18:02.809118163 -0700
```
