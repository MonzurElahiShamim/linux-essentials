---
updated_at: 2024-06-20T21:41:54.338+06:00
edited_seconds: 270
---
# Copying Files

The `cp` command copies files from a source to a destination. Here's a concise overview:

### Basic Usage
- **Syntax**:`cp source destination`
  - **Example**: `cp /etc/hosts ~` copies the `/etc/hosts` file to the home directory.
  - **Output**: No output means success.
### Verbose Mode
- Use `-v` to show details of the copy process.
- **Example**: `cp -v /etc/hosts ~` displays the action being performed.

### Renaming During Copy
- Specify a new name in the destination to rename the file.
-  **Example**: `cp /etc/hosts ~/hosts.copy`

### Prevent Overwrites
- Use `-i` for interactive prompts before overwriting or `-n` to prevent overwriting without prompts.
- **Example**:
    - Interactive: `cp -i /etc/hosts example.txt`
    - No Overwrite: `cp -n /etc/hosts example.txt`

### Copying Directories
- Use `-r` or `-R` to copy directories recursively.
-  **Example**: `cp -r /source_dir /destination_dir`
>[!caution] **Caution**: This can result in copying many files and subdirectories.

## Example Commands:

```bash
# Basic copy
cp /etc/hosts ~

# Verbose copy
cp -v /etc/hosts ~

# Copy with renaming
cp /etc/hosts ~/hosts.copy

# Interactive copy to prevent overwriting
cp -i /etc/hosts example.txt

# Prevent overwrite without prompt
cp -n /etc/hosts example.txt

# Copy a directory recursively
cp -r /etc/skel /destination_dir
```

Use `-r` or `-R` cautiously, as these options will copy entire directory structures.

