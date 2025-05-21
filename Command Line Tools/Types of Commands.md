# Command Types in Shell

Understanding command types in the shell can help you use the command line interface (CLI) more effectively. The `type` command helps identify the type and source of a command.

### Internal Commands
**Internal commands**, also known as built-in commands, are integrated into the shell. For example, the `cd` (change directory) command is a built-in command in the Bash shell. It is directly interpreted by the shell without needing an external program.

To identify an internal command:

```bash
type cd
# Output: cd is a shell builtin
```

### External Commands
**External commands** are executable files stored in directories listed in the `PATH` variable. When you type a command like `ls`, the shell searches these directories to find and execute the command.

To find the location of an external command:

```bash
which ls
# Output: /bin/ls
```

You can also run an external command by specifying its full path:

```bash
/bin/ls
```

To check the type of an external command:

```bash
type cal
# Output: cal is /usr/bin/cal
```

Using the `-a` option with `type` shows all instances of a command:

```bash
type -a echo
# Output:
# echo is a shell builtin
# echo is /bin/echo
```

### Aliases
**Aliases** are shortcuts for longer commands. They simplify and speed up command execution. For instance, `ls -l` might be aliased to `ll`.

To list current aliases:

```bash
alias
# Output:
# alias egrep='egrep --color=auto'
# alias fgrep='fgrep --color=auto'
# alias grep='grep --color=auto'
# alias l='ls -CF'
# alias la='ls -A'
# alias ll='ls -alF'
# alias ls='ls --color=auto'
```

To create a new alias:

```bash
alias mycal="cal 2019"
mycal
# Output: (Displays calendar for 2019)
```

Aliases are temporary and only persist for the current shell session. Use `type` to identify an alias:

```bash
type ll
# Output: ll is aliased to `ls -alF`
```

### Functions
**Functions** are more advanced than aliases and can include multiple commands. They are often used in scripts to group commands.

To create a function:

```bash
my_report () {
    ls Documents
    date
    echo "Document directory report"
}
# Output: (Lists documents, displays date, and prints a report message)
```

To execute the function:

```bash
sysadmin@localhost:~$ my_report                                              
School            alpha-third.txt  hidden.txt    numbers.txt  spelling.txt   
Work              alpha.txt        letters.txt   os.csv       words          
adjectives.txt    animals.txt      linux.txt     people.csv                  
alpha-first.txt   food.txt         longfile.txt  profile.txt                 
alpha-second.txt  hello.sh         newhome.txt   red.txt                     
Wed Oct 13 06:54:04 UTC 2021                                                 
Document directory report                                                    
sysadmin@localhost:~$
```

Functions are defined using the following syntax:

```bash
function_name () {
   commands
}
```

This format uses the function name, parentheses `()`, and braces `{}` to encapsulate the commands. Functions offer flexibility and can streamline repetitive tasks.

## Summary
- **Internal commands** are built into the shell.
- **External commands** are executables in `PATH` directories.
- **Aliases** are shortcuts for commands, making frequent tasks quicker.
- **Functions** combine multiple commands and are useful for scripts and complex tasks.

Understanding these command types enhances your efficiency and effectiveness in using the shell.