# Permissions

The output of the `ls -l` command includes *ten characters* at the beginning of each line, indicating the **type of file** and the **permissions** associated with the file. Let's break down this output:

```bash
root@localhost:~# ls -l /etc/passwd
-rw-r--r--. 1 root root 4135 May 27 21:08 /etc/passwd
```

### File Type

The first character indicates the type of file:

| Character | File Type Description                                           |
| --------- | --------------------------------------------------------------- |
| -         | ***Regular file***                                                |
| d         | ***Directory file***                                              |
| l         | ***Symbolic link***                                               |
| b         | Block file (related to block hardware devices)                  |
| c         | Character file (related to character hardware devices)          |
| p         | Pipe file (for inter-process communication)                     |
| s         | Socket file (for inter-process communication between processes) |

> Typically, you will encounter ***regular files***, ***directories***, and ***symbolic links***.

### Permission Groups

The next nine characters are grouped into three sets of three, representing the permissions for the user owner, group owner, and others.

Example breakdown of `-rw-r--r--`:

- **User Owner** (`rw-`): Characters 2-4.
- **Group Owner** (`r--`): Characters 5-7.
- **Others** (`r--`): Characters 8-10.

Permissions include read (`r`), write (`w`), and execute (`x`).

### Detailed Permissions

Each group (user, group, others) can have the following permissions:

#### Read (`r`):
  - File: Allows viewing and copying of the file contents.
  - Directory: Allows listing of file names within the directory.

#### Write (`w`):
  - File: Allows modifying the file content. Typically, write permission requires read (`r`) permission to function correctly.
  - Directory: Allows adding or removing files in the directory. Requires execute (`x`) permission on the directory to function correctly.

#### Execute (`x`):
  - File: Allows the file to be executed or run as a process.
  - Directory: Allows the user to "enter" the directory using `cd` and access files and subdirectories within it.

### Examples

1. **User Owner:**
   - Example: `-rw-r--r-- 1 root root 4135 May 27 21:08 /etc/passwd`
   - Permissions: `rw-` (read and write for the owner).

2. **Group Owner:**
   - Example: `-rw-r--r-- 1 root root 4135 May 27 21:08 /etc/passwd`
   - Permissions: `r--` (read-only for the group).

3. **Others:**
   - Example: `-rw-r--r-- 1 root root 4135 May 27 21:08 /etc/passwd`
   - Permissions: `r--` (read-only for others).

