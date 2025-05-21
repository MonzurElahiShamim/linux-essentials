## Creating Symbolic Links

A symbolic link, also called a soft link, is simply a file that points to another file. There are several symbolic links already on the system, including several in the `/etc` directory:

**sysadmin@localhost:~$** ls -l /etc/grub.conf
lrwxrwxrwx. 1 root root 22 Feb 15  2011 /etc/grub.conf -> ../boot/grub/grub.conf

In the previous example, the file `/etc/grub.conf` "points to" the `../boot/grub/grub.conf` file. So, if you were to attempt to view the contents of the `/etc/grub.conf` file, it would follow the pointer and show you the contents of the `../boot/grub/grub.conf` file.

To create a symbolic link, use the `-s` option with the `ln` command:

ln -s target link_name

**sysadmin@localhost:~$**  ln -s /etc/passwd mypasswd
**sysadmin@localhost:~$**  ls -l mypasswd
lrwxrwxrwx. 1 sysadmin sysadmin 11 Oct 31 13:17 mypasswd -> /etc/passwd

**Consider This**

Notice that the first bit of the `ls -l` output is the `l` character, indicating that the file type is a link.

-  [Previous](https://content.netdevgroup.com/contents/linux-essentials/wmSZ35UMRf/18.5.1)
- [Next](https://content.netdevgroup.com/contents/linux-essentials/wmSZ35UMRf/18.5.3)