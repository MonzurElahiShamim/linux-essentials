### Local Variables in Shell

Local variables in a shell are confined to the current shell session and do not influence other commands or applications. They disappear once the terminal or shell is closed. Typically used for user-specific tasks, these variables are conventionally named in lowercase.

**To set a local variable**, use:

```bash
variable=value
```

If the variable exists, its value is updated; otherwise, a new variable is created. For example:

```bash
variable1='Something'
```

**To display the value** of the variable, use the `echo` command with the `$` sign:

```bash
echo $variable1
# Output: Something
```