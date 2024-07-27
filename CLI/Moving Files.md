---
updated_at: 2024-06-20T21:49:41.079+06:00
edited_seconds: 230
---
# Moving and Renaming Files

To move or rename files in Linux, use the `mv` command. Here's a concise summary:
### Basic Usage: `mv source destination`
- **Example**: `mv /etc/hosts ~` moves the `/etc/hosts` file to the home directory (`~`).
### Moving Files: 
When you move a file, it is removed from the original location and placed in the new location.
- **Example**: `mv hosts Videos` moves the `hosts` file to the `Videos` directory.
### Renaming Files
If the destination is a filename rather than a directory, the file is renamed.
- **Example**: `mv example.txt Videos/newexample.txt` renames `example.txt` to `newexample.txt` in the `Videos` directory.

>[!warning] **Permissions**: Ensure you have appropriate permissions to remove files from a directory. Permission denied errors occur otherwise.

> [!tip] Options
> - **-i**: Interactive mode, prompts before overwriting.
> - **-n**: No clobber, prevents overwriting existing files.
> - **-v**: Verbose mode, displays the operation performed.

### Example Commands:

```bash
# Basic move
mv /etc/hosts ~

# Move to directory
mv hosts Videos

# Rename file
mv example.txt Videos/newexample.txt

# Interactive move (prompt before overwrite)
mv -i /etc/hosts .

# Prevent overwrite (no clobber)
mv -n /etc/hosts .

# Verbose move
mv -v /etc/hosts ~
```

>[!note] **Note**: Directories are moved by default with `mv` and there is no need for a `-r` option.

