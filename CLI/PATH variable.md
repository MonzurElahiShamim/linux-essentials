---
updated_at: 2024-06-18T13:59:14.260+06:00
edited_seconds: 160
---
# Path Variable

One of the most important Bash shell variables to understand is the `PATH` variable. It contains a list that defines which directories the shell looks in to find commands. If a valid command is entered and the shell returns a "command not found" error, it is because the Bash shell was unable to locate a command by that name in any of the directories included in the path. The following command displays the path of the current shell:

```bash
sysadmin@localhost:~$ echo $PATH                                        
/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
sysadmin@localhost:~$
```

Each directory in the list is separated by a colon `:` character. Based on the preceding output, the path contains the following directories. The shell will check the directories in the order they are listed:

/home/sysadmin/bin
/usr/local/sbin
/usr/local/bin
/usr/sbin
/usr/bin
/sbin
/bin
/usr/games

Each of these directories is represented by a path. A path is a list of directories separated by the / character. If you think of the filesystem as a map, paths are the directory addresses, which include step-by-step navigation directions; they can be used to indicate the location of any file within the filesystem. For example, `/home/sysadmin` is a path to the home directory:

![](https://ndg-content-dev.s3.amazonaws.com/media/images/linux-essentials-v2/home_directory.png)

Directories and paths will be covered in detail later in the course.

If the command is not found in any directory listed in the `PATH` variable, then the shell returns an error:

```bash
sysadmin@localhost:~$ zed                                              
-bash: zed: command not found                                           
sysadmin@localhost:~$
```

## Modify `PATH` Variable
‌⁠​​⁠​ If custom software is installed on the system it may be necessary to modify the `PATH` to make it easier to execute these commands. For example, the following will add and verify the `/usr/bin/custom` directory to the `PATH` variable:

```bash
sysadmin@localhost:~$ PATH=/usr/bin/custom:$PATH                        
sysadmin@localhost:~$ echo $PATH                                       
/usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games 
```                                             

When updating the `PATH` variable, always include the current path, so as not to lose access to commands located in those directories. This can be accomplished by appending `$PATH` to the value in the assignment expression. Recall that a variable name preceded by a dollar sign represents the value of the variable.