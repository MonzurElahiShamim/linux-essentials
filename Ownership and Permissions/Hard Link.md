---
updated_at: 2024-08-29T13:34:18.940+06:00
edited_seconds: 20
---
## Creating Hard Links

To understand hard links, it is helpful to understand a little bit about how the file system keeps track of files. For every file created, there is a block of data on the file system that stores the metadata of the file. Metadata includes information about the file like the permissions, ownership, and timestamps. Metadata does not include the file name or the contents of the file, but it does include just about all other information about the file.

This metadata is called the file's inode table. The inode table also includes pointers to the other blocks on the file system called data blocks where the data is stored.

Every file on a partition has a unique identification number called an inode number. The `ls -i` command displays the inode number of a file.

**sysadmin@localhost:~$** ls -i /tmp/file.txt                                       
215220874 /tmp/file.txt   

Like users and groups, what defines a file is not its name, but rather the number it has been assigned. The inode table does not include the file name. For each file, there is also an entry that is stored in a directory's data area (data block) that includes an association between an inode number and a file name.

In the data block for the `/etc` directory, there would be a list of all of the files in this directory and their corresponding inode number. For example:

|File Name|Inode Number|
|---|---|
|`passwd`|123|
|`shadow`|175|
|`group`|144|
|`gshadow`|897|

When you attempt to access the `/etc/passwd` file, the system uses this table to translate the file name into an inode number. It then retrieves the file data by looking at the information in the inode table for the file.

Hard links are two file names that point to the same inode. For example, consider the following directory entries:

|File Name|Inode Number|
|---|---|
|`passwd`|123|
|`mypasswd`|123|
|`shadow`|175|
|`group`|144|
|`gshadow`|897|

Because both the `passwd` and `mypasswd` file have the same inode number, they essentially are the same file. You can access the file data using either file name.

When you execute the `ls -li` command, the number that appears for each file between the permissions and the user owner is the link count number:

**sysadmin@localhost:~$** echo data > file.original 
**sysadmin@localhost:~$** ls -li file.* 
278772 -rw-rw-r--. 1 sysadmin sysadmin 5 Oct 25 15:42 file.original

The link count number indicates how many hard links have been created. When the number is a value of one, then the file has only one name linked to the inode.

To create hard links, the `ln` command is used with two arguments. The first argument is an existing file name to link to, called a target, and the second argument is the new file name to link to the target.

ln target link_name

When the `ln` command is used to create a hard link, the link count number increases by one for each additional filename:

**sysadmin@localhost:~$** ln file.original file.hard.1
**sysadmin@localhost:~$** ls -li file.*
278772 -rw-rw-r--. 2 sysadmin sysadmin 5 Oct 25 15:53 file.hard.1
278772 -rw-rw-r--. 2 sysadmin sysadmin 5 Oct 25 15:53 file.original
