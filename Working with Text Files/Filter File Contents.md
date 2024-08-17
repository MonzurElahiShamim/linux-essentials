---
updated_at: 2024-08-17T18:49:53.064+06:00
edited_seconds: 210
---
# Filter File Contents

The `grep` command can be used to filter lines in a file or the output of another command that matches a specified pattern. That pattern can be as simple as the exact text that you want to match or it can be much more advanced through the use of regular expressions.

For example, to find all the users who can log in to the system with the BASH shell, the `grep` command can be used to filter the lines from the `/etc/passwd` file for the lines containing the pattern `bash`:
```bash
sysadmin@localhost:~$ grep bash /etc/passwd
root:x:0:0:root:/root:/bin/bash
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```
To make it easier to see what exactly is matched, use the `--color` option. This option will highlight the matched items in red: 

```bash
sysadmin@localhost:~$ grep --color bash /etc/passwd
root:x:0:0:root:/root:/bin/bash
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

In some cases, it may not be important to find the specific lines that match the pattern, but rather how many lines match the pattern. The `-c` option provides a count of how many lines match:

```bash
sysadmin@localhost:~$ grep -c bash /etc/passwd
2
```

When viewing the output from the `grep` command, it can be hard to determine the original line numbers. This information can be useful when going back into the file (perhaps to edit the file) to quickly find one of the matched lines.

The `-n` option to the `grep` command will display original line numbers. To display all lines and their line numbers in the `/etc/passwd` file which contain the pattern `bash`:

```bash
sysadmin@localhost:~$ grep -n bash /etc/passwd                          
1:root:x:0:0:root:/root:/bin/bash                                       
27:sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

The `-v` option inverts the match, outputting all lines that do not contain the pattern. To display all lines not containing `nologin` in the `/etc/passwd` file:

```bash
sysadmin@localhost:~$ grep -v nologin /etc/passwd
root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
operator:x:1000:37::/root:/bin/sh
sysadmin:x:1001:1001:System Administrator,,,,:/home/sysadmin:/bin/bash
```

The `-i` option ignores the case (capitalization) distinctions. The following searches for the pattern `the` in `newhome.txt`, allowing each character to be uppercase or lowercase:

```bash
sysadmin@localhost:~$ cd Documents
sysadmin@localhost:~/Documents$ grep -i the newhome.txt
There are three bathrooms.
**Beware** of the ghost in the bedroom.
The kitchen is open for entertaining.
**Caution** the spirits don't like guests.
```

The `-w` option only returns lines which contain matches that form whole words. To be a word, the character string must be preceded and followed by a non-word character. Word characters include letters, digits, and the underscore character.

The following examples search for the `are` pattern in the `newhome.txt` file. The first command searches with no options, while the second command includes the `-w` option. Compare the outputs:

```bash
sysadmin@localhost:~/Documents$ grep are newhome.txt
There are three bathrooms.
**Beware** of the ghost in the bedroom.
sysadmin@localhost:~/Documents$ grep -w are newhome.txt
There are three bathrooms.
```


>[!gemini]+ Gemini
>The `grep` command filters lines from a file or command output that match a specified pattern. It supports various options:
> 
> - `--color`: Highlights matches in red.
> - `-c`: Counts the number of matching lines.
> - `-n`: Displays matching line numbers.
> - `-v`: Inverts the match, showing non-matching lines.
> - `-i`: Ignores case distinctions.
> - `-w`: Only matches complete words.
> 
> For example, using `grep bash /etc/passwd` finds users with the BASH shell, with `--color` highlighting the matches. `grep -c bash /etc/passwd` counts the users with BASH, and `grep -v nologin /etc/passwd` lists users who do not have "nologin" in their entry.
 
 