---
updated_at: 2024-07-20T21:45:12.252+06:00
edited_seconds: 40
---
## Modifying a User

**Considerations:**
- Some changes (e.g., login name) require the user to be logged out.
- Other changes (e.g., group memberships) take effect after the user logs out and logs back in.

**Useful Commands:**
- **`who`**: Shows who is currently logged in.
- **`w`**: More verbose, shows who is logged in, system uptime, load information, and running processes.
- **`last`**: Shows current and previous login sessions with specific date and time.

#### `usermod` Command Options:

| Short Option | Long Option       | Description                                                    |
|--------------|-------------------|----------------------------------------------------------------|
| `-c`         | `COMMENT`         | Sets the GECOS/comment field.                                   |
| `-d`         | `HOME_DIR`        | Sets a new home directory.                                      |
| `-e`         | `EXPIRE_DATE`     | Sets account expiration date.                                   |
| `-f`         | `INACTIVE`        | Sets days to permit login after password expires.               |
| `-g`         | `GROUP`           | Sets the primary group.                                         |
| `-G`         | `GROUPS`          | Sets supplementary groups.                                      |
| `-a`         | `--append`        | Appends supplementary groups specified by `-G`.                 |
| `-h`         | `--help`          | Shows help for the command.                                     |
| `-l`         | `NEW_LOGIN`       | Changes the login name.                                         |
| `-L`         | `--lock`          | Locks the user account.                                         |
| `-s`         | `SHELL`           | Specifies the login shell.                                      |
| `-u`         | `NEW_UID`         | Specifies the new UID.                                          |
| `-U`         | `--unlock`        | Unlocks the user account.                                       |

**Important Considerations:**
- Changing the UID (`-u` option) can orphan user's files.
- Changing the login name (`-l` option) does not orphan files.
- Locking an account (`-L` option) prevents usage but retains file ownership.

**Managing Supplementary Groups:**
- Using `-G` without `-a` removes user from all former groups not listed.
- Using `-aG` appends new groups to the user's existing groups.
  
Example:
```bash
root@localhost:~# usermod -aG development jane
```

## Deleting a User

**`userdel` Command:**
- Deletes user account.
- Decision needed on whether to delete the user's home directory.

**Example:**
- To delete user without deleting home directory:
  ```bash
  root@localhost:~# userdel jane
  ```

- To delete user, home directory, and mail spool:
  ```bash
  root@localhost:~# userdel -r jane
  ```

**Warning:**
- `userdel -r` only deletes files in the home directory and mail spool.
- Other files owned by the user outside the home directory will become orphaned.