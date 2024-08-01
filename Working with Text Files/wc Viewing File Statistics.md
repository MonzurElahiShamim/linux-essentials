---
updated_at: 2024-07-13T19:19:30.550+06:00
edited_seconds: 40
---
# Viewing File Statistics with `wc` Command

The `wc` command provides statistics such as the number of lines, words, and bytes in a file or set of files. Here’s how you can use it effectively:

1. **Basic Usage**:
   - By default, `wc` displays three statistics for each file: lines, words, and bytes.

   **Example - Displaying Statistics for Two Files**:
   ```bash
   sysadmin@localhost:~$ wc /etc/passwd /etc/passwd-
   35   56 1710 /etc/passwd
   34   55 1665 /etc/passwd-
   69  111 3375 total
   ```
   - In this example, `wc` shows statistics (lines, words, bytes) for `/etc/passwd` and `/etc/passwd-`, followed by the total statistics for both files.

2. **Output Format**:
   - The output includes four columns: number of lines, number of words, number of bytes, and the file name.

3. **Viewing Specific Statistics**:
   - You can specify options to view only specific statistics:
     - `-l`: Displays the number of lines.
     - `-w`: Displays the number of words.
     - `-c`: Displays the number of bytes.

   **Example - Displaying Only the Number of Lines**:
   ```bash
   sysadmin@localhost:~$ wc -l /etc/passwd
   35 /etc/passwd
   ```

4. **Using `wc` with Pipes**:
   - `wc` can be piped with other commands to count lines of output. For instance, to count the number of files in a directory using `ls` and `wc`:

   **Example - Counting Files in a Directory**:
   ```bash
   sysadmin@localhost:~$ ls /etc/ | wc -l
   142
   ```
   - This command counts and displays the number of files in the `/etc/` directory by piping the output of `ls` to `wc -l`, which counts lines.

### Summary:
The `wc` command is versatile for counting lines, words, and bytes in files, and it can be combined with options to tailor output based on specific needs. Its ability to handle input from both files and standard input makes it useful for various text processing tasks in Unix/Linux environments.

---

This explanation provides a clear overview of how to use the `wc` command to gather file statistics and count lines in conjunction with other commands, highlighting its flexibility and practical applications.