
Commands:
- `ls` 
- `ls -l`
- `ls -l /home`
- `whoami`
- `uname`
- `uname -n`
- `uname --nodename`
- `pwd`
- `echo Hi`
- `history`
- `history 5`
- `!9`
- `echo Hello Student`
- `echo $HISTSIZE`
- `echo $PATH`
- `which date`
- `type cd`
- `which ls`
- `type cp`
- `which cp`
- `type -a ls`
- `alias`
- `type vi`
- `cd /bin`
- `type vlc`
- `cd`
- ``echo Today is `date` ``
- `echo Today is $(date)`
- ``echo This is the command '`date`'
- ``echo This is the command \`date\` ``
- `echo D*`
- `echo "D*"`
- `echo Hello; echo Linux; echo Student`
- `false; echo Not; echo Conditional`
- `echo Start && echo Going && echo Gone`
- `echo Success && false && echo Bye`
- `false || echo Fail Or`
- `true || echo Nothing to see here`

> [!note]+ Descriptions
> Here’s a short description of each command entered in Bash:
> 
> ### Listing and Navigation Commands
> - **`ls`**: Lists the contents of the current directory.
>   
> - **`ls -l`**: Lists contents of the current directory in long format, displaying detailed information including permissions, ownership, size, and modification date.
> 
> - **`ls -l /home`**: Lists contents of the `/home` directory in long format.
> 
> - **`pwd`**: Displays the present working directory, showing the full path of the current directory.
> 
> - **`cd /bin`**: Changes the current directory to `/bin`.
> 
> - **`cd`**: Changes the current directory to the user's home directory.
> 
> ### User and System Information
> - **`whoami`**: Prints the current logged-in user's username.
> 
> - **`uname`**: Displays the system's kernel name.
> 
> - **`uname -n`**: Prints the network node hostname of the system.
> 
> - **`uname --nodename`**: Also prints the network node hostname of the system (same as `uname -n`).
> 
> ### Output Commands
> - **`echo Hi`**: Outputs the text `Hi`.
> 
> - **`echo Hello Student`**: Outputs the text `Hello Student`.
> 
> - **``echo Today is `date` ``**: Executes the `date` command and substitutes its output, then echoes `Today is` followed by the current date and time.
> 
> - **`echo Today is $(date)`**: Similar to the above, using `$(date)` for command substitution to echo `Today is` followed by the current date and time.
> 
> - **``echo This is the command '`date`'``**: Prints `This is the command` followed by the `date` command enclosed in single quotes. The date command is not executed; it’s displayed literally.
> 
> - **``echo This is the command \`date\` ``**: Prints `This is the command` followed by the literal text `` `date` ``, where backticks are treated as plain text due to escaping.
> 
> - **`echo D*`**: Expands and echoes all filenames in the current directory starting with `D`.
> 
> - **`echo "D*"`**: Echoes the string `D*` literally without expansion.
> 
> ### History Commands
> - **`history`**: Displays the command history list, showing previously entered commands.
> 
> - **`history 5`**: Shows the last 5 commands entered in the command history.
> 
> - **`!9`**: Re-executes the 9th command from the command history.
> 
> ### Shell Variables and Paths
> - **`echo $HISTSIZE`**: Prints the value of the `HISTSIZE` environment variable, which defines the maximum number of commands to remember in the history list.
> 
> - **`echo $PATH`**: Prints the value of the `PATH` environment variable, showing directories the shell searches for executable files.
> 
> ### Command Location and Type
> - **`which date`**: Shows the path of the executable file for the `date` command.
> 
> - **`type cd`**: Identifies `cd` as a shell built-in command.
> 
> - **`which ls`**: Shows the path of the executable file for the `ls` command.
> 
> - **`type cp`**: Displays the type of `cp` as a shell built-in or external command.
> 
> - **`which cp`**: Shows the path of the executable file for the `cp` command.
> 
> - **`type -a ls`**: Displays all locations and types for `ls`, indicating if it’s a built-in, alias, or external command.
> 
> ### Aliases and Functions
> - **`alias`**: Lists all currently defined aliases in the shell.
> 
> - **`type vi`**: Displays the type of `vi` and its location, indicating whether it is an alias, built-in, or external command.
> 
> - **`type vlc`**: Checks the type and location of `vlc`, often indicating if it's an external command or not found.
> 
> ### Command Chaining and Conditionals
> - **`echo Hello; echo Linux; echo Student`**: Executes three `echo` commands in sequence, outputting `Hello`, `Linux`, and `Student` on separate lines.
> 
> - **`false; echo Not; echo Conditional`**: Executes `false` (which does nothing successfully), followed by `echo Not` and `echo Conditional`, since commands after `;` run regardless of the success of preceding commands.
> 
> - **`echo Start && echo Going && echo Gone`**: Executes `echo Start`, and if successful, executes `echo Going`, and if that is successful, executes `echo Gone`.
> 
> - **`echo Success && false && echo Bye`**: Executes `echo Success` successfully, then `false` (which fails), and does not execute `echo Bye` because the chain is broken.
> 
> - **`false || echo Fail Or`**: Executes `false` (which fails) and then `echo Fail Or` because the `||` operator executes the following command if the preceding command fails.
> 
> - **`true || echo Nothing to see here`**: Executes `true` (which succeeds) and does not execute `echo Nothing to see here` because the `||` operator only runs the second command if the first fails.
> 
> Each of these commands demonstrates various fundamental aspects of shell interaction in Bash, including command execution, variable handling, and conditional operations.