---
updated_at: 2024-07-13T19:09:45.103+06:00
edited_seconds: 130
---
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


---
### Sorting Fields and Using Sort Options with `sort`

The `sort` command in Unix/Linux can reorder lines based on specific fields delimited by a specified character, such as spaces, tabs, commas, or colons. Here’s how you can customize sorting using fields and options:

#### 1. Sorting by a Specific Field:
   - Use the `-t` option to specify the field delimiter. For example, `-t:` specifies a colon (`:`) as the delimiter.
   - Use `-k` followed by the field number to indicate which field to sort by. Field numbering starts from 1.

   **Example - Numerical Sort by the Third Field**:
   ```bash
   sysadmin@localhost:~$ sort -t: -n -k3 mypasswd
   ```
   - This command sorts the `mypasswd` file numerically by the third field, assuming fields are separated by colons (`:`).

#### 2. Reverse Sort:
   - Add `-r` option to perform a reverse sort, which arranges lines in descending order based on the specified field.

   **Example - Reverse Numerical Sort by the Third Field**:
   ```bash
   sysadmin@localhost:~$ sort -t: -n -r -k3 mypasswd
   ```
   - This command sorts `mypasswd` in reverse numerical order by the third field.

#### 3. Complex Sorting:
   - You can sort by multiple fields, specifying primary and secondary fields using `-k` multiple times.

   **Example - Sorting by Multiple Fields**:
   ```bash
   sysadmin@localhost:~/Documents$ sort -t, -k2 -k1n -k3 os.csv
   ```
   - Here, `os.csv` is a comma-separated value file. This command sorts first by the second field, then numerically by the first field (`-k1n`), and finally by the third field.

### Summary of Options Used:

| Option | Function |
|--------|----------|
| `-t,`  | Specifies the comma character as the field delimiter in CSV files. |
| `-k2`  | Sorts by the second field. |
| `-k1n` | Numerically sorts by the first field. |
| `-k3`  | Sorts by the third field. |

--- 
