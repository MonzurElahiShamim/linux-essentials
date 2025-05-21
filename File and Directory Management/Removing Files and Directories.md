# Removing Files and Directories

To delete files and directories in Linux, use the `rm` command. Here's a concise summary:
## Deleting Files

  - Use `rm` followed by the filename(s) you want to delete.
  - **Example**: `rm sample.txt` deletes the file named `sample.txt`.
>[!caution] Files are deleted without confirmation, so be cautious when using glob patterns to delete multiple files.

- **Options**:
  - **-i**: Interactive mode prompts before deleting each file.
    - **Example**: `rm -i *.txt` prompts for confirmation before deleting each `.txt` file.
## Deleting Directories 

- By default, `rm` does not delete directories. Use the `-r` (recursive) option to delete directories and their contents.
- **Example**: `rm -r Videos` deletes the `Videos` directory and all its contents.
>[!warning] **Warning**: Recursive deletion is irreversible and does not prompt for confirmation.

- **Using `rmdir`**: Use `rmdir` to delete directories only if they are empty.
  - **Example**: `rmdir Documents` deletes the `Documents` directory only if it is empty.

## Example Commands:

```bash
# Delete a single file
rm sample.txt

# Delete multiple files with confirmation
rm -i *.txt

# Delete a directory and its contents
rm -r Videos

# Delete an empty directory using rmdir
rmdir Documents
```

>[!caution] **Caution**: There is no built-in method to recover files deleted with `rm`. Use `-i` with caution to prevent accidental deletions.

## Directories with subdirectories and files

To delete a directory and all its contents (including subdirectories and files) in Bash, you can use the `rm` command with the `-r` (recursive) and `-f` (force) options. Here’s how:

### Command

```bash
rm -rf /path/to/directory
```

### Options Explained

- `-r` or `--recursive`: Removes directories and their contents recursively.
- `-f` or `--force`: Ignores nonexistent files and arguments, never prompts.

### Example

Suppose you have a directory named `example_dir` with multiple subdirectories and files inside it. To delete `example_dir` and all its contents:

```bash
rm -rf example_dir
```

### Important Notes

- **Be Careful**: This command is very powerful and will permanently delete everything in the specified directory without asking for confirmation. Double-check the directory path before running the command to avoid accidental data loss.
- **Permissions**: Ensure you have the necessary permissions to delete the files and directories. You may need to use `sudo` if you encounter permission issues:
  ```bash
  sudo rm -rf /path/to/directory
  ```

### Safety Tip

If you want to review the files that will be deleted before actually deleting them, you can list them with the `ls` command:

```bash
ls -R /path/to/directory
```

This lists all files and directories recursively under the specified path.

### Example Scenario

#### Delete a Directory Structure:

```bash
/home/user/project
  ├── subdir1
  │   └── file1.txt
  ├── subdir2
  │   └── file2.txt
  └── file3.txt
```

To delete `project` and everything inside it:

```bash
rm -rf /home/user/project
```

This will remove `project`, `subdir1`, `subdir2`, and all the files inside these directories.

### Summary

The `rm -rf` command is the most straightforward way to delete a directory and all its contents in Bash. Always use it with caution and ensure you are deleting the correct directory to avoid unintended data loss.
