---
updated_at: 2024-07-16T19:55:39.521+06:00
edited_seconds: 30
---
### User Configuration Files

The `useradd` command with the `-D` option shows or changes default values for new user accounts. These values can also be found and edited in `/etc/default/useradd`.

**Viewing Defaults:**
```bash
root@localhost:~# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

#### Default Values:

- **GROUP=100**: Default primary group ID (usually the "users" group).
  - Change with: `-g` option
- **HOME=/home**: Base directory for new user home directories.
  - Change with: `-b` option
- **INACTIVE=-1**: Number of days after password expiration that the account is disabled (-1 means disabled).
  - Change with: `-f` option
- **EXPIRE=**: Account expiration date (empty means no expiration by default).
  - Change with: `-e` option
- **SHELL=/bin/bash**: Default login shell.
  - Change with: `-s` option
- **SKEL=/etc/skel**: Skeleton directory for initializing home directories.
  - Change with: `-k` option
- **CREATE_MAIL_SPOOL=yes**: Whether to create a mail spool file for the user.
  - Change in `/etc/default/useradd` or with `useradd -D`

#### Example:
To set the INACTIVE value to 30 days:
```bash
root@localhost:~# useradd -D -f 30
root@localhost:~# useradd -D
GROUP=100
HOME=/home
INACTIVE=30
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```
