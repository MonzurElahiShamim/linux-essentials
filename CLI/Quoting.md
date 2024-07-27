---
updated_at: 2024-07-13T18:52:07.137+06:00
edited_seconds: 520
---
# Quoting in Bash

In Bash scripting and Linux administration, quotation marks play a crucial role in handling text and commands. They instruct the shell on how to treat the enclosed content, whether to interpret it literally or to evaluate special characters and variables. Bash recognizes three primary types of quotes: double quotes `"`, single quotes `'`, and backquotes (backticks) `` ` ``. Each type of quotation affects the shell's interpretation of the enclosed text differently.

## Double Quotes (`" "`)

Double quotes preserve the literal value of most characters within them but allow the interpretation of certain special characters, such as variables and command substitution.

**Key Characteristics:**
- Variables are evaluated.
- Command substitution is allowed.
- Prevents globbing (wildcard characters) from being interpreted by the shell.

**Example of Double Quotes:**

```bash
echo "The glob characters are *, ? and [ ]"
# Output: The glob characters are *, ? and [ ]
```

In this example, the shell does not expand `*`, `?`, and `[]` into matching filenames because they are enclosed in double quotes.

**Variable and Command Substitution:**

```bash
echo "The path is $PATH"
# Output: The path is /usr/bin:/bin:/usr/sbin:/sbin
```

Here, `$PATH` is evaluated and replaced by its value. Similarly, command substitution within double quotes allows commands to be executed and their output to be incorporated into the text.
```bash
echo "Today is `date`"
# Output: Today is Mon Nov  4 03:35:50 UTC 2018
```


## Single Quotes (`' '`)

Single quotes treat everything inside them literally, preventing any interpretation of special characters.

**Key Characteristics:**
- Variables and command substitutions are not evaluated.
- Every character is treated as plain text.

**Example of Single Quotes:**

```bash
echo 'The car costs $100'
# Output: The car costs $100
```

In this case, `$100` is displayed as is, without attempting to interpret `$` as a variable.

**Literal Text Example:**

```bash
echo 'Today is `date`'
# Output: Today is `date`
```

Here, backquotes are not treated as command substitution but as literal text.

## Backslash ('\\')

The backslash character allows you to escape individual characters, making them literal without the need for enclosing the entire string in quotes.

**Key Characteristics:**
- Escapes a single character.
- Useful for selectively preventing the interpretation of special characters.

**Example of Backslash Escaping:**

```bash
echo "The service costs \$1 and the path is $PATH"
# Output: The service costs $1 and the path is /usr/bin:/bin:/usr/sbin:/sbin
```

In this example, `\$1` prevents `$1` from being interpreted as a variable while `$PATH` is still evaluated.

## Backquotes (`` ` ` ``)

Backquotes, also known as backticks, are used for command substitution, allowing the output of one command to be embedded within another command.

**Key Characteristics:**
- Executes the enclosed command and replaces the backquoted text with the output of that command.
- Enables dynamic insertion of command results into other commands.

**Example of Backquotes:**

```bash
echo "Today is `date`"
# Output: Today is Mon Nov  4 03:35:50 UTC 2018
```

Here, the `date` command is executed, and its output replaces `` `date` `` within the `echo` command.

## Combining Quotes

Sometimes, you may need to combine quotes and escapes to achieve the desired behavior, especially when handling complex strings.

**Example of Combining Quotes and Escapes:**

```bash
echo "Today's date is `date` and the price is \$50"
# Output: 
# Today's date is Mon Nov  4 03:35:50 UTC 2018 and the price is $50
```

In this example, backquotes are used for command substitution, and the backslash is used to escape `$` so that it is displayed as a literal dollar sign.

## Practical Applications of Quoting

- **Double Quotes**: Use when you need to include variables or commands within a string while protecting other special characters.
- **Single Quotes**: Use when you want to include literal text without any substitutions.
- **Backslashes**: Use for selectively escaping individual characters within a string.
- **Backquotes**: Use for embedding command output dynamically within another command.

Understanding how to use quotes effectively allows you to control the interpretation of text and commands in Bash, leading to more robust and predictable scripts and command-line operations.

> [!note]- # Original Note
> # Quoting
> Quotation marks are used throughout Linux administration and most computer programming languages to let the system know that the information contained within the quotation marks should either be ignored or treated in a way that is very different than it would normally be treated. There are three types of quotes that have special significance to the Bash shell: double quotes ", single quotes ', and back quotes `. Each set of quotes alerts the shell not to treat the text within the quotes in the normal way.
> 
> ## Double Quotes
> Double quotes stop the shell from interpreting some metacharacters (special characters), including glob characters.
> 
> Glob characters, also called wild cards, are symbols that have special meaning to the shell; they are interpreted by the shell itself before it attempts to run any command. Glob characters include the asterisk * character, the question ? mark character, and the brackets [ ], among others.
> 
> Globbing will be covered in greater detail later in the course.
> 
> Within double quotes an asterisk is just an asterisk, a question mark is just a question mark, and so on, which is useful when you want to display something on the screen that is normally a special character to the shell. In the echo command below, the Bash shell doesn't convert the glob pattern into filenames that match the pattern:
> 
> ```bash
> sysadmin@localhost:~$ echo "The glob characters are \*, ? and [ ]"      
> The glob characters are \*, ? and [ ]
> ```
> Double quotes still allow for command substitution, variable substitution, and permit some other shell metacharacters that haven't been discussed yet. The following demonstration shows that the value of the PATH variable is still displayed:
> 
> ```bash
> sysadmin@localhost:~$ echo "The path is $PATH"                          
> The path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
> ```
> ## Single Quotes
> Single quotes prevent the shell from doing any interpreting of special characters, including globs, variables, command substitution and other metacharacters that have not been discussed yet.
> 
> For example, to make the $ character simply mean a $, rather than it acting as an indicator to the shell to look for the value of a variable, execute the second command displayed below:
> 
> ```bash
> sysadmin@localhost:~$ echo The car costs $100                           
> The car costs 00                                                        
> sysadmin@localhost:~$ echo 'The car costs $100'                        
> The car costs $100
> ```
> 
> ## Backslash Character
> There is also an alternative technique to essentially single quote a single character. Consider the following message:
> 
> The service costs $1 and the path is $PATH 
> If this sentence is placed in double quotes, $1 and $PATH are considered variables.
> 
> ```bash
> sysadmin@localhost:~$ echo "The service costs $1 and the path is $PATH"
> 
> ‌⁠​​⁠​The service costs  and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games 
> ```
> If it is placed in single quotes, $1 and $PATH are not considered variables.
> 
> ```bash 
> sysadmin@localhost:~$ echo 'The service costs $1 and the path is $PATH' 
> The service costs $1 and the path is $PATH 
> ```
> But what if you want to have $PATH treated as a variable and $1 not?
> 
> In this case, use a backslash \ character in front of the dollar sign $ character to prevent the shell from interpreting it. The command below demonstrates using the \ character:
> 
> ```bash
> sysadmin@localhost:~$ echo The service costs \$1 and the path is $PATH
> The service costs $1 and the path is /usr/bin/custom:/home/sysadmin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
> ``` 
> 
> ## Backquotes
> Backquotes, or backticks, are used to specify a command within a command, a process called command substitution. This allows for powerful and sophisticated use of commands.
> 
> While it may sound confusing, an example should make things more clear. To begin, note the output of the date command:
> 
> ```bash
> sysadmin@localhost:~$ date                                           
> Mon Nov  4 03:35:50 UTC 2018
> ```
> Now, note the output of the echo command:
> 
> ```bash
> sysadmin@localhost:~$ echo Today is date                               
> Today is date
> ```
> In the previous command, the word date is treated as regular text, and the shell passes date to the echo command. To execute the date command and have the output of that command sent to the echo command, put the date command in between two backquote characters:
> 
> ```bash
> sysadmin@localhost:~$ echo Today is `date`                         
> Today is Mon Nov 4 03:40:04 UTC 2018
> ```

 