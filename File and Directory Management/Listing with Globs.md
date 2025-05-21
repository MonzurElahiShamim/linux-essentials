# Listing Files using wildcards (globs)
In Linux, wildcard characters are used to match patterns in file and directory names when listing or performing operations on files. Here’s a guide to using wildcards with the `ls` command for listing files:

> [!warning]- ## Issues
> ### Listing With Globs
> 
> When listing files with glob patterns using the `ls` command, the shell expands the pattern into matching filenames before executing the command. This can lead to unexpected results if the pattern includes directories.
> 
> - **Shell Expansion**: The shell replaces the glob pattern with matching filenames or directories before running `ls`.
>   - **Example**: `ls /etc/a*` expands to:
>     ```bash
>     ls /etc/adduser.conf  /etc/alternatives  /etc/apparmor  /etc/apparmor.d  /etc/apt
>     ```
>     - Equivalent to running:
>       ```bash
>       ls /etc/adduser.conf  
>       ls /etc/alternatives  
>       ls /etc/apparmor  
>       ls /etc/apparmor.d  
>       ls /etc/apt
>       ```
> 
> - **Single File Argument**: If `ls` is given a single file as an argument, it lists just the filename.
>   - **Example**:
>     ```bash
>     ls /etc/adduser.conf
>     ```
>     - Output: `/etc/adduser.conf`
> 
> - **Directory Argument**: If `ls` is given a directory, it lists the contents of the directory, not just the directory name.
>   - **Example**:
>     ```bash
>     ls /etc/apparmor
>     ```
>     - Output: Lists files within `/etc/apparmor`, like `init`, `parser.conf`, etc.
> 
> - **Confusion with Directories**: Using globs without careful consideration can cause confusion. The `ls` command lists the contents of directories matching the pattern, which can seem incorrect if only the directory name was expected.
>   - **Example**:
>     ```bash
>     ls /etc/x*
>     ```
>     - Output: Lists contents of `/etc/xdg` directory.
> 
> ## **Solution**:
>  Use the `-d` option with `ls` to list the directory names themselves, not their contents.
>   - **Example**:
>     ```bash
>     ls -d /etc/x*
>     ```
>     - Output: `/etc/xdg`

> [!success]+ Remember
> While using **Globs** with `ls` always use `-d` option.
### Wildcards for Pattern Matching

Wildcards are symbols that represent one or more characters in file names. They are particularly useful for working with multiple files at once. Here’s a summary of the most common wildcards:

- **Asterisk (\*)**: Matches zero or more characters.
- **Question Mark (?)**: Matches exactly one character.
- **Square Brackets ([ ])**: Matches any one of the characters enclosed in the brackets.

### Using Wildcards with `ls`

#### Matching Any Number of Characters (`*`)

- **Command**: `ls *.txt`
- **Description**: Lists all files ending with `.txt`.
- **Example**:
  ```bash
  sysadmin@localhost:~/Documents$ ls *.txt
  file1.txt  file2.txt  notes.txt
  ```

#### Matching Any Single Character (`?`)

- **Command**: `ls file?.txt`
- **Description**: Lists files where `file` is followed by any single character and ends with `.txt`.
- **Example**:
  ```bash
  sysadmin@localhost:~/Documents$ ls file?.txt
  file1.txt  file2.txt
  ```

#### Matching Any One of the Enclosed Characters (`[ ]`)

- **Command**: `ls file[12].txt`
- **Description**: Lists files where `file` is followed by either `1` or `2` and ends with `.txt`.
- **Example**:
  ```bash
  sysadmin@localhost:~/Documents$ ls -d file[12].txt
  file1.txt  file2.txt
  ```

#### Matching a Range of Characters (`[a-z]`)

- **Command**: `ls -d file[a-d].txt`
- **Description**: Lists files where `file` is followed by any character from `a` to `d` and ends with `.txt`.
- **Example**:
  ```bash
  sysadmin@localhost:~/Documents$ ls -d file[a-d].txt
  filea.txt  fileb.txt  filec.txt
  ```

#### Combining Wildcards

- **Command**: `ls -d *.[ch]`
- **Description**: Lists files ending with either `.c` or `.h`.
- **Example**:
  ```bash
  sysadmin@localhost:~/Documents$ ls -d *.[ch]
  main.c  utils.h
  ```

#### Escaping Wildcards

	Command: ls \*.txt
- **Description**: Lists a file literally named `*.txt` (not matching other `.txt` files).
- **Example**:
  ```bash
  sysadmin@localhost:~/Documents$ ls \*.txt
  *.txt
  ```

### Examples of Wildcard Usage:

1. **List All `.jpg` Files**:
   ```bash
   sysadmin@localhost:~/Pictures$ ls -d *.jpg
   image1.jpg  photo2.jpg  pic3.jpg
   ```

2. **List Files with a Specific Pattern**:
   ```bash
   sysadmin@localhost:~/Downloads$ ls -d report_202?.pdf
   report_2021.pdf  report_2022.pdf
   ```

3. **List Files Starting with `doc` and Ending with a Number**:
   ```bash
   sysadmin@localhost:~/Documents$ ls -d doc[0-9]
   doc1  doc2  doc3
   ```

### Summary of Wildcard Matching:

- `*`: Matches zero or more characters. Useful for broad matches.
- `?`: Matches exactly one character. Useful for precise length matches.
- `[ ]`: Matches any one character within the brackets. Useful for specific character positions or ranges.
- `[a-z]`: Matches any character within the specified range.

Wildcards make it easier to handle multiple files in Linux, especially when performing tasks like listing files, moving, copying, or deleting. They are essential for efficient file management in the command-line environment.