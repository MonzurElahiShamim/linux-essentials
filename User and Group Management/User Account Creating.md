# Creating a User Account

>[!caution] Before
>Before Creating User Account check the [[User Configuration Files]] for default values.

#### User Identifier (UID):

- **Default Behavior**: UIDs increment automatically.
- **Range**: 0 to over 4 billion; recommended max for compatibility is 60,000.
- **Specify UID**: Use the `-u` option.

```bash
root@localhost:~# useradd -u 1000 jane
```

#### Supplementary Groups:

- **Specify**: Use the `-G` option for additional groups.

```bash
root@localhost:~# useradd -G sales,research jane
```

#### Skeleton Directory:

- **Default**: `/etc/skel` is copied to the new home directory.
- **Specify**: Use `-k` with `-m`.

```bash
root@localhost:~# useradd -mk /home/sysadmin jane
```

#### User with no interactive shell

```bash
sudo useradd -s /sbin/nologin rose
```

#### Comment:

- **Use**: Typically holds the user's full name.
- **Specify**: Use the `-c` option.

```bash
root@localhost:~# useradd -c 'Jane Doe' jane
```