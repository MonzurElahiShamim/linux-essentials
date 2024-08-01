---
updated_at: 2024-07-16T17:39:25.786+06:00
edited_seconds: 10
---
### Viewing User Information with the `id` Command

**Basic Usage:**

- **Current User:**
  ```bash
  id
  ```
  - Shows UID, GID, and group memberships for the current user.

- **Specific User:**
  ```bash
  id username
  ```
  - Displays UID, GID, and group memberships for the specified user.

**Options:**

- **Primary Group ID:**
  ```bash
  id -g
  ```
  - Prints only the primary group ID.

- **All Group IDs:**
  ```bash
  id -G
  ```
  - Lists all group IDs the user belongs to.

**Example:**

To view the `sysadmin` user details:

```bash
id sysadmin
```

To check group memberships:

```bash
cat /etc/group | grep sysadmin
```