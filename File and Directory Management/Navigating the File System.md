# Navigating the Filesystem in Linux 
## The Linux Filesystem Structure

- **Root Directory `/`**
  - Top-level directory, symbolized by `/`.
  - Equivalent to "My Computer" in Windows.

- **Unified Filesystem**
  - No drive letters; all devices are accessed as directories under `/`.
  - Devices and partitions are mounted within the root hierarchy.

- **Device Accessibility**
  - Devices integrated into the directory structure, e.g., under `/mnt` or `/media`.

![[Pasted image 20240620113232.png]]
### Home Directory

- **Location**
  - **`/home` Directory**: Located under the root directory (`/`).
  - **User-Specific Subdirectories**: Each user has a subdirectory under `/home`, named after their username (e.g., `/home/sysadmin` for the user `sysadmin`).
  - ![[Pasted image 20240620115044.png]]

- **Purpose**
  - **Default Starting Directory**: Users are placed in their home directory upon opening a shell.
  - **Workspace**: Where users typically perform their work.

- **Permissions**
  - **User Control**: Users have full control to create and delete files and directories within their home directory.
  - **Access Restrictions**: Only the directory owner and system administrator can access the files, protecting user data from others.

- **Special Notation**
  - **Tilde `~`**: Represents the current user's home directory.
  - **Referencing Other Users**: `~username` can be used to refer to another user's home directory (e.g., `~bob` for `/home/bob`).

- **Example**
  - **User `sysadmin`**: Home directory is `/home/sysadmin`, which can be referenced as `~` when `sysadmin` is logged in.

This home directory structure provides a secure, personal workspace for each user on a Linux system.

## Navigating Directories: `pwd` and `cd` Commands

### `pwd` Command: Current Directory
- **Purpose**: Displays the full path of the current working directory.
- **Usage**: Run `pwd` in the terminal to see the current directory path.
- **Example**: 
  ```bash
  sysadmin@localhost:~$ pwd
  /home/sysadmin
  ```
  In this example, the user is in the `/home/sysadmin` directory.
- **Typical Use Cases**:
  - Verify your current location in the directory structure.
  - Useful for confirming paths before running commands that require directory-specific execution.

### `cd` Command: Changing Directories
- **Purpose**: Allows you to change the current working directory to another location.
- **Basic Commands**:
  - **Move to a Specific Directory**:
    ```bash
    cd <directory_path>
    ```
    Changes to the specified directory. If the directory path is relative, it is interpreted from the current directory.
  - **Move Up One Level**:
    ```bash
    cd ..
    ```
    Changes to the parent directory.
  - **Move to the Root Directory**:
    ```bash
    cd /
    ```
    Changes to the root directory.
  - **Move to the Home Directory**:
    ```bash
    cd ~
    # or 
    cd
    ```
    Changes to the user's home directory.
- **Examples**:
  ```bash
  sysadmin@localhost:~$ cd /etc
  sysadmin@localhost:/etc$ cd ..
  sysadmin@localhost:/$ cd ~
  sysadmin@localhost:~$ cd Documents
  sysadmin@localhost:~/Documents$
  ```


## Paths

- **Paths** are used in the `cd` command to navigate directories in the Linux filesystem.
- **Structure**: A path is a sequence of directories separated by the `/` character.
- **Purpose**: Paths act as addresses in the filesystem, providing step-by-step directions to locate files or directories.
- **Example**: `/home/sysadmin` navigates from the root `/` to `home` and then to `sysadmin`.

**Types of Paths**:
- **Absolute Paths**
- **Relative Paths**

### Absolute Paths

- **Definition**: Absolute paths specify the full location of a directory starting from the root (`/`). They always begin with the `/` character.
- **Usage**: 
  - Example: `/home/sysadmin` starts at the root `/`, moves to `home`, and then to `sysadmin`.
  - In the command `cd /home/sysadmin`, it navigates directly to the sysadmin user's home directory.

```bash
sysadmin@localhost:~/Documents$ cd /home/sysadmin
```

- **Verification**: 
  - To confirm the change, use `pwd` to display the current directory.
  - Output shows the absolute path.

```bash
sysadmin@localhost:~$ pwd
/home/sysadmin
```

### Relative Paths

- **Definition**: Relative paths specify a location in relation to the current directory. They do not start with the root (`/`), and instead, begin from the current working directory.

- **Special Symbols**:
  - `.` (dot): Represents the current directory.
  - `..` (double dot): Represents the parent directory.

- **Usage**:
  - To navigate to a subdirectory: use just the subdirectory name.
  - To move up one directory: use `..`.
  - Example: From `/home/sysadmin`, to navigate to a subdirectory `Documents`:
  
  ```bash
  sysadmin@localhost:~/Documents$ cd Documents
  ```

- **Examples**:
  - To move up one directory from `/home/sysadmin`:
  
  ```bash
  sysadmin@localhost:~/Documents$ cd ..
  ```
  - To move to a sibling directory `Downloads` from `Documents`:

  ```bash
  sysadmin@localhost:~/Documents$ cd ../Downloads
  ```

- **Verification**:
  - Use `pwd` to check the current directory after navigating with relative paths.

```bash
sysadmin@localhost:~/Documents$ pwd
/home/sysadmin/Documents

sysadmin@localhost:~/Documents$ cd ..
sysadmin@localhost:~$ pwd
/home/sysadmin
```

- **Combination**:
  - Relative paths can combine `.` and `..` for more complex navigation.
  - Example: Move from `/home/sysadmin/Documents` to `/home/sysadmin/Downloads`:

  ```bash
  sysadmin@localhost:~/Documents$ cd ../Downloads
  ```

