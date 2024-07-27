---
updated_at: 2024-07-17T18:38:58.445+06:00
edited_seconds: 780
---
# Understanding Permissions
The descriptions of the permission types can be handy, but just themselves, they don't provide a clear description of how permissions work. To better understand how permissions work, consider the following scenarios.

To understand these scenarios, you should first understand the following diagram:

```bash
drwxr-xr-x. 17 root root 4096 23:38 /
drwxr-xr-x. 10 root root 128  03:38 /data
-rwxr-xr--.  1 bob  bob  100  21:08 /data/abc.txt
```
‌⁠​​⁠​ 
The relevant information is highlighted. The first line represents the / directory, with a user owner of root, a group owner of root and permissions of rwxr-xr-x. The second line represents the /data directory, a directory that is under the / directory. The third line represents the abc.txt file, which is stored in the /data directory.

## Scenario #1 

**Question**: Based on the following information, what access would the user bob have on the file abc.txt?

```bash
drwxr-xr-x. 17 root root 4096 23:38 /
drwxr-xr--. 10 root root 128  03:38 /data
-rwxr-xr--.  1 bob  bob  100  21:08 /data/abc.txt
```

>***Answer***: None.

**Explanation**: 
While it appears bob has full permissions on `abc.txt`, he cannot access `/data` because he lacks execute (`x`) permission on the directory. Without this, he cannot even enter the directory to reach the file.

***Lesson Learned***: 
The permissions of all parent directories must be considered before considering the permissions on a specific file.

## Scenario #2

**Question**: Based on the following information, who can use the ls command to display the contents of the /data directory (ls /data)?

```bash
drwxr-xr-x. 17 root root 4096 23:38 /
drwxr-xr--. 10 root root 128  03:38 /data
-rwxr-xr--.  1 bob  bob  100  21:08 /data/abc.txt
```

>***Answer***: All users.

**Explanation**: 
All users can view the contents of the `/data` directory because they have `r` permission on it and `x` permission on the `/` directory. The `r` permission on `/data` allows using the `ls` command to list the contents, including hidden files `ls -a`. 
However, `ls -l` requires `x` permission on `/data`, which only the root user and members of the root group have.

***Lesson Learned***: 
The r permission allows a user to view a listing of the directory.

## Scenario #3

**Question**: Based on the following information, who can delete the /data/abc.txt file?

```bash
drwxr-xr-x. 17 root root 4096 23:38 /
drwxrw-rw-. 10 root root 128  03:38 /data
-rwxr-xr--.  1 bob  bob  100  21:08 /data/abc.txt
```

>***Answer***: Only the root user.

**Explanation**: 
To delete a file, a user needs `w` permission on the directory containing the file and `x` permission to "get into" that directory. While all users have `w` permission on the `/data` directory, only the root user has `x` permission to access it. Therefore, only the root user can delete the `/data/abc.txt` file.

***Lesson Learned***: 
The `w` permission allows a user to *delete* files from a directory, but *only if* the user also has `x` permission on the directory.

## Scenario #4

**Question**: True or False: Based on the following information the user bob can successfully execute the following command: more /data/abc.txt?

```bash
drwxr-xr-x. 17 root root 4096 23:38 /
dr-xr-x--x. 10 root root 128  03:38 /data
-rwxr-xr--.  1 bob  bob  100  21:08 /data/abc.txt
```

>***Answer***: True.

**Explanation**: 
To access a file, the user must have `x` permission on all parent directories. Bob has `x` permission on both the `/` and `/data` directories, and `r` permission on the `abc.txt` file. Therefore, Bob can successfully execute `more /data/abc.txt`.
However, Bob cannot list the content of `/data` directory.

***Lesson Learned***: 
The `x` permission is required to "get into" a directory, but the `r` permission on the directory is not necessary unless you want to list the directory's contents.

## Scenario #5

**Question**: True or False: Based on the following information the user bob can successfully execute the following command: more /data/abc.txt?

>[!note]
>Note that the /data directory has different user and group owners than previous examples

```bash
drwxr-xr-x. 17 root root    4096 23:38 /
dr-xr-x---. 10 sue  payroll 128  03:38 /data
-rwxr-xr--.  1 bob  bob     100  21:08 /data/abc.txt
```
‌⁠​​⁠​ 
>***Answer***: Not enough information to determine.

**Explanation**: 
For Bob to access the `/data/abc.txt` file, he needs `x` permission on the `/data` directory. Whether he has this permission depends on if he is a member of the payroll group. If he is, he has `r-x` permissions on `/data`, and the command will work. If he is not, he has no permissions (`---`) on `/data`, and the command will fail.

***Lesson Learned***: 
You must look at each file and directory permissions separately and be aware of which groups the user account belongs to.


## Scenario #6

**Question**: *True* or *False*: Based on the following information the user bob can successfully execute the following command: more /data/abc.txt?

>[!note]
>Note that the `/data` directory has **different** user and group owners than the previous example

```bash
drwxr-xr-x. 17 root root 4096 23:38 /
dr-xr-x---. 10 bob  bob  128  03:38 /data
----rw-rwx.  1 bob  bob  100  21:08 /data/abc.txt
```

***Answer***: False.

**Explanation**: 
If Bob is the owner of a file, only the ***user owner permissions*** are checked. In this case, Bob has no permissions (`---`) on the `/data/abc.txt` file. Therefore, despite the permissions granted to the group and others, Bob cannot access the file.

***Lesson Learned***: 
Don't provide permissions to the group owner and "others" without applying at least the same level of access to the owner of the file.


