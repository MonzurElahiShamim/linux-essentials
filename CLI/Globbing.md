---
updated_at: 2024-06-20T20:17:59.426+06:00
edited_seconds: 90
---
# Globbing

- **Definition**: Globbing refers to the use of special symbol characters, known as wildcards, which have special meanings to the shell.
- **Purpose**: Allows specifying patterns to match filenames in a directory, enabling manipulation of multiple files simultaneously.
- **Use Cases**: Useful for commands affecting all files with a specific extension or particular filename length.
- **Shell Interpretation**: Globbing patterns are interpreted by the shell before running any command, making them versatile with any command.
- **Examples**: Demonstrations often use the `echo` command to show how globbing works.

### Asterisk (\*) Character

- **Purpose**: Represents zero or more of any character in a filename.
- **Flexible Placement**: Can be used anywhere in the pattern to match filenames with specific characteristics:
- **Usage Examples**:
  - **Begin with 't'**: 
    ```bash
    echo /etc/t*
    ```
    Matches files in `/etc` starting with 't':
    ```
    /etc/terminfo /etc/timezone /etc/tmpfiles.d
    ```
  - **End with '.d'**:
    ```bash
    echo /etc/*.d
    ```
    Matches files in `/etc` ending with '.d':
    ```
    /etc/apparmor.d /etc/binfmt.d /etc/cron.d /etc/depmod.d /etc/init.d ...
    ```
  - **Begin with 'r' and end with '.conf'**:
    ```bash
    echo /etc/r*.conf
    ```
    Matches files in `/etc` starting with 'r' and ending with '.conf':
    ```
    /etc/resolv.conf /etc/rsyslog.conf
    ```

### Question Mark ? Character

- **Purpose**: Represents exactly one character in filenames.
  
- **Usage Example**: To list files in `/etc` that start with "t" and have exactly 7 characters following:
  ```bash
  echo /etc/t???????
  ```
  - **Output**: Matches files like `/etc/terminfo`, `/etc/timezone`.

- **Combining Globs**: Use multiple glob characters to create more complex patterns:
  ```bash
  echo /etc/*????????????????????
  ```
  - **Output**: Matches files in `/etc` with filenames 20 or more characters long, such as `/etc/bindresvport.blacklist`, `/etc/ca-certificates.conf`.

- **Mixed Patterns**: Combine `*` and `?` to match files with specific characteristics, such as files with three-letter extensions:
  ```bash
  echo /etc/*.???
  ```
  - **Output**: Matches files like `/etc/issue.net`, `/etc/locale.gen`.

### Bracket `[ ]` Characters

- **Purpose**: Match a single character from a specified set or range of characters within a filename.

- **Set Matching**: Matches filenames starting with any character inside the brackets.
  - **Example 1**: List files in `/etc` beginning with "g" or "u" and containing zero or more additional characters:
    ```bash
    echo /etc/[gu]*
    ```
    - **Output**: Matches files like `/etc/gai.conf`, `/etc/group`, `/etc/ucf.conf`.

- **Range Matching**: Matches filenames starting with any character within the specified range.
  - **Example 2**: List files in `/etc` beginning with any letter between "a" and "d":
    ```bash
    echo /etc/[a-d]*
    ```
    - **Output**: Matches files like `/etc/adduser.conf`, `/etc/bash.bashrc`, `/etc/cron.d`.

  - **Example 3**: List files in `/etc` containing at least one digit (0-9):
    ```bash
    echo /etc/*[0-9]*
    ```
    - **Output**: Matches files like `/etc/X11`, `/etc/rc0.d`, `/etc/python3`.

- **Invalid Range**: An invalid range results in no matches.
  - **Example 4**: Attempting to match a reversed or invalid numeric range:
    ```bash
    echo /etc/*[9-0]*
    ```
    - **Output**: No files are matched because the range is invalid. 

- **Notes**:
  - The ASCII text table determines the order of characters. The `ascii` command can be used to view this table.