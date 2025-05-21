### System Accounts in Linux

**Purpose:**
- System accounts are not designed for user logins.
- Used for services running on the system.
- Typically have UIDs from 1 to 499.

**Characteristics of System Accounts:**
- **No home directories**: System accounts usually don’t have home directories as they don't create or store files.
- **Non-login shells**: System accounts often use non-login shells to prevent login.

**Example in `/etc/passwd`:**
```bash
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin
```
- **Username**: `sshd`
- **Password Placeholder**: `x`
- **User ID (UID)**: `103`
- **Primary Group ID**: `65534`
- **Comment**: (none)
- **Home Directory**: `/var/run/sshd`
- **Shell**: `/usr/sbin/nologin`

**Example in `/etc/shadow`:**
```bash
sshd:*:16874:0:99999:7:::
```
- **Username**: `sshd`
- **Password**: `*` (non-login account)

**Caution:**
- Most system accounts are essential for system functionality.
- Deleting system accounts may cause system issues.
- Understand each system account's role before making changes.

### Group Accounts

**Group Membership:**
- Users can be members of multiple groups.
- Groups define additional levels of system access.

**Primary and Secondary Groups:**
- **Primary Group**: Defined in `/etc/passwd`.
- **Secondary Groups**: Defined in `/etc/group`.

**Example of `/etc/group`:**
```bash
mail:x:12:mail,postfix
```
- **Group Name**: `mail`
- **Password Placeholder**: `x`
- **Group ID (GID)**: `12`
- **User List**: `mail,postfix` (members of the group)

**Group Passwords:**
- Group passwords are rare.
- If set, stored in `/etc/gshadow`.

**Checking Group Information:**
- Use `grep` or `getent` to view group details.
```bash
sysadmin@localhost:~$ grep mail /etc/group
mail:x:12:mail,postfix

sysadmin@localhost:~$ getent group mail
mail:x:12:mail,postfix
```

Understanding and managing system and group accounts properly ensures the security and efficient operation of a Linux system.