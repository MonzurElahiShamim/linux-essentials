## Setting a User Password

#### Methods:
1. **User-Initiated Change**: 
   - Users change their own password with the `passwd` command. 
   - Users are prompted for their current password and then the new password twice.
2. **Administrator-Initiated Change**: 
   - Administrators set or change passwords for any user using `passwd <username>`.
   - Example: `passwd jane`
   - The administrator sets the password and the `/etc/shadow` file is updated.
   - Root users only need to ensure passwords are not blank.
3. **Graphical Tools**:
   - Available on systems with desktop environments.

**Administrator Example:**
```bash
root@localhost:~# passwd jane
Enter new UNIX password:
BAD PASSWORD: it is WAY too short
BAD PASSWORD: is too simple
Retype new UNIX password:
```

#### Password Rules:
- Regular users must follow all password complexity rules.
- Root users receive warnings but are only restricted from setting blank passwords.

## Managing Password Aging

#### File:
- **/etc/shadow**: Contains encrypted passwords and password aging information.

#### `chage` Command:
- Manages password aging settings in `/etc/shadow`.

##### Options:
- **`-l, --list`**: List account aging information.
- **`-d LAST_DAY, --lastday LAST_DAY`**: Set the date of the last password change.
- **`-E EXPIRE_DATE, --expiredate EXPIRE_DATE`**: Set account expiration date.
- **`-I INACTIVE, --inactive INACTIVE`**: Set inactive days after password expires.
- **`-m MIN_DAYS, --mindays MIN_DAYS`**: Set minimum days before password can be changed.
- **`-M MAX_DAYS, --maxdays MAX_DAYS`**: Set maximum days before password must be changed.
- **`-W WARN_DAYS, --warndays WARN_DAYS`**: Set days to start displaying expiration warnings.

##### Example:
```bash
root@localhost:~# chage -M 60 jane
root@localhost:~# grep jane /etc/shadow | cut -d: -f1,5
jane:60
```
This command sets the maximum password age for user `jane` to 60 days.

