---
updated_at: 2024-07-17T10:35:40.363+06:00
edited_seconds: 360
---
# Creating a User Account

>[!caution] Before
>Before Creating User Account check the [[User Configuration Files]] for default values.

---
#### Username:

- **Required**: The only mandatory argument for `useradd`.
- **Guidelines**:
  - Start with an underscore (_) or lowercase letter (a-z).
  - Up to 32 characters (16 is safer for compatibility).
  - Use alphanumeric characters, dashes (-), or underscores (_).
  - Avoid ending with a hyphen (-).

```bash
root@localhost:~# useradd jane
```

---
#### User Identifier (UID):

- **Default Behavior**: UIDs increment automatically.
- **Range**: 0 to over 4 billion; recommended max for compatibility is 60,000.
- **Specify UID**: Use the `-u` option.

```bash
root@localhost:~# useradd -u 1000 jane
```

---
#### Primary Group:

- **Default**: "users" group with GID 100 if not using User Private Groups (UPG).
- **Specify Group**: Use the `-g` option.

```bash
root@localhost:~# useradd -g users jane
```

---
#### Supplementary Groups:

- **Specify**: Use the `-G` option for additional groups.

```bash
root@localhost:~# useradd -G sales,research jane
```

---
#### Home Directory:

- **Default**: `/home/username`.
- **Options**:
  - **Do not create**: `-M` if `CREATE_HOME` is no.
  - **Create explicitly**: `-m`.
  - **Specify base**: `-b` for different base directory.
  - **Specify directory**: `-d` for a full path.

```bash
root@localhost:~# useradd -m jane
root@localhost:~# useradd -mb /test jane
root@localhost:~# useradd -md /test/jane jane
```

---
#### Skeleton Directory:

- **Default**: `/etc/skel` is copied to the new home directory.
- **Specify**: Use `-k` with `-m`.

```bash
root@localhost:~# useradd -mk /home/sysadmin jane
```

---
#### Shell:

- **Default**: Specified in `/etc/default/useradd`.
- **Override**: Use the `-s` option.

```bash
root@localhost:~# useradd -s /bin/bash jane
```

---
#### Comment:

- **Use**: Typically holds the user's full name.
- **Specify**: Use the `-c` option.

```bash
root@localhost:~# useradd -c 'Jane Doe' jane
```