# Sorting Files or Input Using `sort`

The `sort` command in Linux arranges lines of text files or input either in dictionary order (default) or numeric order. Here's how you can use it:

1. **Creating a Sample File**:
   - You can create a small file using commands like `head` to extract lines from another file and redirect the output. For example:
     ```bash
     sysadmin@localhost:~$ head -5 /etc/passwd > mypasswd
     sysadmin@localhost:~$ cat mypasswd
     root:x:0:0:root:/root:/bin/bash
     daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
     bin:x:2:2:bin:/bin:/usr/sbin/nologin
     sys:x:3:3:sys:/dev:/usr/sbin/nologin
     sync:x:4:65534:sync:/bin:/bin/sync
     ```
   - In this example, `head -5 /etc/passwd` extracts the first 5 lines of `/etc/passwd` and redirects them to a file named `mypasswd`.

2. **Sorting the File**:
   - Once you have a file (`mypasswd` in this case), you can sort its contents using `sort`:
     ```bash
     sysadmin@localhost:~$ sort mypasswd
     bin:x:2:2:bin:/bin:/usr/sbin/nologin
     daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
     root:x:0:0:root:/root:/bin/bash
     sync:x:4:65534:sync:/bin:/bin/sync
     sys:x:3:3:sys:/dev:/usr/sbin/nologin
     ```
   - The `sort mypasswd` command arranges the lines alphabetically by default. Compare this output with the original order from the `cat mypasswd` command.


