# Getting Started with Linux
---

Lets get Started!!

---

### Who am I?

Find the current user:
```bash
whoami
```

---

### Who else is logged in?

List logged-in users:

```bash
who
```

```bash
w
```

---

### Where am I?

Show current directory:

```bash
pwd
```

---

### File System Hierarchy

- `/`: Root directory, the base of the file system.
- `/home`: Contains user directories (e.g., `/home/user`).
- `/etc`: Stores configuration files.
- `/bin`: Essential binaries like `ls`, `cp`, and `mv`.
- `/usr`: Contains user-installed software and libraries.

---
#### Contd...

- `/var`: Stores variable data like logs, databases, and caches.
- `/tmp`: Temporary files.
- `/opt`: Optional application software.
- `/dev`: Device files (e.g., disks, USB).
- `/mnt` and `/media`: Mount points for external drives.
- `/proc` and `/sys`: Virtual filesystems for system information.

---

### What system is this?

Display system information:

```bash
uname -a
```

```bash
cat /etc/os-release
```

```bash
hostnamectl
```

---

### Change Directory

Navigate between directories:

```bash
cd /path/to/directory    # Go to a specific directory 
```

```bash
cd ..                    # Go up one level  
```

---
### List directories and files

List contents in current directory:
```bash
ls
```

List contents in a specific directory:
```bash
ls /path/to/directory
```

---
##### Options with `ls`:
+ `l`: Long listing with details.
+ `a`: show hidden files.
+ `h`: show output in human readable form (used along with `l` option).
+ `d`: List details of a directory (used along with `l` option).

---
### Command History and utilities

```bash
history
```

```bash
cal
```

```bash
date
```

---
### Know about a Command

```bash
man command
```

```bash
command --help
```

```bash
which command
```

```bash
info command
```

```bash
type command
```

---

### Create a Directory

Make new directories:

```bash
mkdir folder1                      # Single directory  
```

```bash
mkdir dir1 dir2 dir3               # Multiple directories  
```

```bash
mkdir -p dir3/subdir1/             # Nested directories  
```

---

### Create a File

Use `touch` to create files:

```bash
touch file1.txt                    # Single file  
```

```bash
touch ./dir1/myfile.txt            # Inside a specific directory  
```

```bash
touch sample1.txt sample2.txt      # Multiple files  
```

```bash
touch newfile{1,2,3}.txt           # Using brace expansion  
```
---

### Copy

Copy a file:
```bash
cp /path/to/source /path/to/destination
```

Copy a directory:
```bash
cp -r /path/to/source /path/to/destination
```

---

### Move

```bash
mv /path/to/source /path/to/destination
```

---

### Rename

```bash
mv <old_name> <new_name>
```

---

### Delete a file

```bash
rm filename
```

```bash
rm /path/to/file
```

---

### Delete a directory

Delete an empty directory:
```bash
rmdir /path/to/directory
```

Delete a directory with files and sub-directories:
```bash
rm -r /path/to/directory
```

---
### Read contents of a file

```bash
cat /path/to/file
```

---

### Write into a file

```bash
echo "this is a sample text" > file1.txt
```

Append to a file:
```bash
echo "This is another sample" >> file1.txt
```

Write using A text editor:
```bash
nano /path/to/file
```
Other text editors: `vi`, `vim`, `neovim`, `gedit` etc.

---

### Create a User

Interactive user creation:
```bash
sudo adduser <user_name>
```

```bash
sudo useradd <user_name>
```

---

### List all users

```bash
cat /etc/passwd
```

```bash
getent passwd
```

---

### Change password of a user

Change password of current user:
```bash
passwd
```

Change password of another user:
```bash
passwd <user_name>
```

---

### List all groups of a user

##### Current user:
```bash
groups
```

```bash
id
```

##### Other user:
```bash
groups <user_name>
```

```bash
id <user_name>
```

---

### Create a Group

```bash
groupadd <group_name>
```
Or
```bash
addgroup <group_name>
```

---

### List all Groups

```bash
cat /etc/group
```

```bash
getent group
```

---

### Add a User to a Group

```bash
usermod -aG group_name user_name
```

---

### Package manager

```bash
sudo apt update
```

```bash
sudo apt upgrade
```

```bash
sudo apt install <package_name>
```

```bash
sudo apt remove <package_name>
```

---

