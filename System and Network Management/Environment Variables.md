### Environment Variables in Shell

**Environment variables**, or global variables, are accessible across all shell sessions and are recreated automatically when a new shell is opened. Common examples include `PATH`, `HOME`, and `HISTSIZE`. For instance, `HISTSIZE` determines the number of commands stored in the command history.

To **view** an environment variable's value:

```bash
echo $HISTSIZE
# Output: 1000
```

To **modify** an environment variable:

```bash
HISTSIZE=500
echo $HISTSIZE
# Output: 500
```

**Local variables** can be made environment variables using the `export` command, enabling system-wide availability:

```bash
export variable1
```

For example, creating and exporting a variable:

```bash
export variable1='Something'
env | grep variable1
# Output: variable1=Something
```

To **create and export** a variable simultaneously:

```bash
export variable2='Else'
env | grep variable2
# Output: variable2=Else
```

**Combining** values from different variables:

```bash
variable1="$variable1 $variable2"
echo $variable1
# Output: Something Else
```

To **remove** an exported variable:

```bash
unset variable2
```

Use the `env` command to **list all environment variables**, and filter specific ones with `grep`:

```bash
env | grep variable1
```

Environment variables are crucial for system-wide settings and can affect various commands and shell behaviors.### Environment Variables in Shell

**Environment variables**, or global variables, are accessible across all shell sessions and are recreated automatically when a new shell is opened. Common examples include `PATH`, `HOME`, and `HISTSIZE`. For instance, `HISTSIZE` determines the number of commands stored in the command history.

To **view** an environment variable's value:

```bash
echo $HISTSIZE
# Output: 1000
```

To **modify** an environment variable:

```bash
HISTSIZE=500
echo $HISTSIZE
# Output: 500
```

**Local variables** can be made environment variables using the `export` command, enabling system-wide availability:

```bash
export variable1
```

For example, creating and exporting a variable:

```bash
export variable1='Something'
env | grep variable1
# Output: variable1=Something
```

To **create and export** a variable simultaneously:

```bash
export variable2='Else'
env | grep variable2
# Output: variable2=Else
```

**Combining** values from different variables:

```bash
variable1="$variable1 $variable2"
echo $variable1
# Output: Something Else
```

To **remove** an exported variable:

```bash
unset variable2
```

Use the `env` command to **list all environment variables**, and filter specific ones with `grep`:

```bash
env | grep variable1
```

Environment variables are crucial for system-wide settings and can affect various commands and shell behaviors.