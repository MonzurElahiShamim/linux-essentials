# Managing Groups in Linux

### Creating a Group:

**Use `groupadd` to create a new group:**
  ```bash
  groupadd groupname
  ```

**Optionally, specify a GID with `-g`:**
  ```bash
  groupadd -g 1005 research
  ```
- If `-g` is not used, a GID is assigned automatically.

#### Group ID Considerations:
- Avoid using GIDs in ranges reserved for system use (under 500 or 1000) to prevent conflicts with user private groups (UPGs).
- Use `-r` to create a group with a reserved GID:
  ```bash
  groupadd -r sales
  ```

### Modifying a Group

**Change the group name with `groupmod -n`:**
  ```bash
  groupmod -n newname oldname
  ```

**Change the GID with `groupmod -g`:**
  ```bash
  groupmod -g 10003 groupname
  ```

>[!caution]
>Changing the GID makes files associated with the old GID become orphaned.

### Deleting a Group

- Use `groupdel` to delete a group:
  ```bash
  groupdel groupname
  ```

>[!caution]
>Only supplemental groups can be deleted. Ensure the group is not a primary group for any user before deletion.