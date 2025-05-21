### User Accounts in Linux

**Location of User Account Data:**
- User and group account data is stored in text files within the `/etc` directory.
- The `/etc/passwd` file defines user account information.

**Example of `/etc/passwd`:**
```bash
sysadmin@localhost:~$ tail -5 /etc/passwd
syslog:x:101:103::/home/syslog:/bin/false
bind:x:102:105::/var/cache/bind:/bin/false
sshd:x:103:65534::/var/run/sshd:/usr/sbin/nologin
operator:x:1000:37::/root:/bin/sh
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

**Fields in `/etc/passwd`:**
1. **Username**: `sysadmin`
2. **Password Placeholder**: `x` (indicates password is stored in `/etc/shadow`)
3. **User ID (UID)**: `1001`
4. **Primary Group ID**: `1001`
5. **Comment**: `System Administrator,,,`
6. **Home Directory**: `/home/sysadmin`
7. **Shell**: `/bin/bash`

**Searching for a User Account:**
- Use `grep` to find specific user information:
```bash
sysadmin@localhost:~$ grep sysadmin /etc/passwd
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

**Password Information:**
- Stored in `/etc/shadow`.
- Regular users can't view this file for security reasons.

**Example of `/etc/shadow`:**
```bash
root@localhost:~# tail -5 /etc/shadow
syslog:*:16874:0:99999:7:::
bind:*:16874:0:99999:7:::
sshd:*:16874:0:99999:7:::
operator:!:16874:0:99999:7:::
sysadmin:$6$c75ekQWF$.GpiZpFnIXLzkALjDpZXmjxZcIll14OvL2mFSIfnc1aU2cQ/221QL5AX5RjKXpXPJRQ0uVN35TY3/..c7v0.n0:16874:5:30:7:60:15050:
```

**Fields in `/etc/shadow`:**
1. **Username**: `sysadmin`
2. **Password**: Encrypted password.
3. **Last Change**: Number of days since January 1, 1970, when the password was last changed.
4. **Minimum**: Minimum days between password changes.
5. **Maximum**: Maximum days the password is valid.
6. **Warn**: Days before password expiry to warn the user.
7. **Inactive**: Grace period for password change after expiry.
8. **Expire**: Account expiration date.
9. **Reserved**: Reserved for future use.

**Retrieving User Information:**
- Use `getent` to retrieve account information:
```bash
sysadmin@localhost:~$ getent passwd sysadmin
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

