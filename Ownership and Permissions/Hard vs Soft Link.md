## Comparing Hard and Symbolic Links

While hard and symbolic links have the same result, the different techniques produce different advantages and disadvantages. In fact, the advantage of one technique compensates for a disadvantage of the other technique.

**Advantage: Hard links don’t have a single point of failure.**

One of the benefits of using hard links is that every file name for the file content is equivalent. If you have five files hard linked together, then deleting any four of these files would not result in deleting the actual file contents.

Recall that a file is associated with a unique inode number. As long as one of the hard linked files remains, then that inode number still exists, and the file data still exists.

Symbolic links, however, have a single point of failure: the original file. Consider the following example in which access to the data fails if the original file is deleted. The `mytest.txt` file is a symbolic link to the `text.txt` file:

**sysadmin@localhost:~$** ls -l mytest.txt
lrwxrwxrwx. 1 sysadmin sysadmin 8 Oct 31 13:29 mytest.txt -> test.txt
**sysadmin@localhost:~$** more test.txt
hi there
**sysadmin@localhost:~$** more mytest.txt
hi there

If the original file, the `test.txt` file is removed, then any files linked to it, including the `mytest.txt` file, fail:

**sysadmin@localhost:~$** rm test.txt
**sysadmin@localhost:~$** more mytest.txt
mytest.txt: No such file or directory
**sysadmin@localhost:~$** ls -l mytest.txt
lrwxrwxrwx. 1 sysadmin sysadmin 8 Oct 31 13:29 mytest.txt -> test.txt

**Advantage: Soft links are easier to see.**

Sometimes it can be difficult to know where the hard links to a file exist. If you see a regular file with a link count that is greater than one, you can use the `find` command with the `-inum` search criteria to locate the other files that have the same inode number. To find the inode number you would first use the `ls -i` command:

**sysadmin@localhost:~$** ls -i file.original 
278772 file.original
**sysadmin@localhost:~$** find / -inum 278772 2> /dev/null
/home/sysadmin/file.hard.1
/home/sysadmin/file.original

Soft links are much more visual, not requiring any extra commands beyond the `ls` command to determine the link:

**sysadmin@localhost:~$** ls -l mypasswd
lrwxrwxrwx. 1 sysadmin sysadmin 11 Oct 31 13:17 mypasswd -> /etc/passwd

**Advantage: Soft links can link to any file.**

Since each file system (partition) has a separate set of inodes, hard links cannot be created that attempt to cross file systems:

**sysadmin@localhost:~$** ln /boot/vmlinuz-2.6.32-358.6.1.el6.i686 Linux.Kernel
ln: creating hard link `Linux.Kernel' => `/boot/vmlinuz-2.6.32-358.6.1.el6.i686': Invalid cross-device link

In the previous example, a hard link was attempted to be created between a file in the `/boot` file system and the `/` file system; it failed because each of these file systems has a unique set of inode numbers that can't be used outside of the filesystem.

However, because a symbolic link points to another file using a pathname, you can create a soft link to a file in another filesystem:

**sysadmin@localhost:~$** ln -s /boot/vmlinuz-2.6.32-358.6.1.el6.i686 Linux.Kernel
**sysadmin@localhost:~$** ls -l Linux.Kernel
lrwxrwxrwx. 1 sysadmin sysadmin 11 Oct 31 13:17 Linux.Kernel -> /boot/vmlinuz-2.6.32-358.6.1.el6.i686

**Advantage: Soft links can link to a directory.**

Another limitation of hard links is that they cannot be created on directories. The reason for this limitation is that the operating system itself uses hard links to define the hierarchy of the directory structure. The following example shows the error message that is displayed if you attempt to hard link to a directory:

**sysadmin@localhost:~$** ln /bin binary
ln: `/bin': hard link not allowed for directory

Linking to directories using a symbolic link is permitted:

**sysadmin@localhost:~$** ln -s /bin binary
**sysadmin@localhost:~$** ls -l binary
lrwxrwxrwx. 1 sysadmin sysadmin 11 Oct 31 13:17 binary -> /bin

-  [Previous](https://content.netdevgroup.com/contents/linux-essentials/wmSZ35UMRf/18.5.2)
- [Next](https://content.netdevgroup.com/contents/linux-essentials/wmSZ35UMRf/)