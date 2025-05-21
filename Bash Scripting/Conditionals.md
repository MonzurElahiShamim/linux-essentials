# Conditionals in Bash scripting

### **1. Basic `if` Statement**
The `if` statement in Bash allows you to execute commands based on whether a condition is true. The general syntax is:

```bash
if [ condition ]; then
    # commands if condition is true
fi
```

- `[` and `]` are part of the syntax (an alias for the `test` command).
- The condition inside the brackets must evaluate to true for the commands inside the `then` block to execute.

**Example:**
```bash
if [ -f "/path/to/file.txt" ]; then
    echo "File exists."
fi
```

### **2. `if-else` Statement**
An `if-else` statement provides an alternative set of commands if the condition is false.

```bash
if [ condition ]; then
    # commands if condition is true
else
    # commands if condition is false
fi
```

**Example:**
```bash
if [ -d "/path/to/directory" ]; then
    echo "Directory exists."
else
    echo "Directory does not exist."
fi
```

### **3. `if-elif-else` Statement**
The `elif` (else if) statement lets you test multiple conditions in sequence. Only the first true condition will have its commands executed.

```bash
if [ condition1 ]; then
    # commands if condition1 is true
elif [ condition2 ]; then
    # commands if condition2 is true
else
    # commands if none of the conditions are true
fi
```

**Example:**
```bash
if [ "$score" -ge 90 ]; then
    echo "Grade: A+"
elif [ "$score" -ge 80 ]; then
    echo "Grade: A"
elif [ "$score" -ge 70 ]; then
    echo "Grade: B"
else
    echo "Grade: F"
fi
```

### **4. Common Conditional Expressions**
Bash offers various expressions for testing conditions, which include:

#### File Conditions
- `[ -f filename ]`: True if file exists and is a regular file.
- `[ -d filename ]`: True if file exists and is a directory.
- `[ -e filename ]`: True if file exists (any type).
- `[ -s filename ]`: True if file exists and is not empty.

#### String Conditions
- `[ "$str1" = "$str2" ]`: True if `str1` is equal to `str2`.
- `[ "$str1" != "$str2" ]`: True if `str1` is not equal to `str2`.
- `[ -z "$str" ]`: True if `str` is an empty string.
- `[ -n "$str" ]`: True if `str` is not empty.

#### Numeric Conditions
- `[ "$num1" -eq "$num2" ]`: True if `num1` is equal to `num2`.
- `[ "$num1" -ne "$num2" ]`: True if `num1` is not equal to `num2`.
- `[ "$num1" -gt "$num2" ]`: True if `num1` is greater than `num2`.
- `[ "$num1" -ge "$num2" ]`: True if `num1` is greater than or equal to `num2`.
- `[ "$num1" -lt "$num2" ]`: True if `num1` is less than `num2`.
- `[ "$num1" -le "$num2" ]`: True if `num1` is less than or equal to `num2`.

#### Permission Checking Expressions

|Expression|Description|
|---|---|
|`-r filename`|True if the file is readable.|
|`-w filename`|True if the file is writable.|
|`-x filename`|True if the file is executable.|
|`-u filename`|True if the file has the SUID bit set.|
|`-g filename`|True if the file has the SGID bit set.|
|`-k filename`|True if the file has the sticky bit set.|

### **5. Logical Operators**
Logical operators allow you to combine conditions.

#### AND Operator
- `[ condition1 ] && [ condition2 ]`: True if both conditions are true.
- **Example:**
  ```bash
  if [ -f "/path/to/file" ] && [ -r "/path/to/file" ]; then
      echo "File exists and is readable."
  fi
  ```

#### OR Operator
- `[ condition1 ] || [ condition2 ]`: True if at least one condition is true.
- **Example:**
  ```bash
  if [ -f "/path/to/file" ] || [ -d "/path/to/file" ]; then
      echo "File is either a regular file or a directory."
  fi
  ```

#### NOT Operator
- `[ ! condition ]`: True if condition is false.
- **Example:**
  ```bash
  if [ ! -f "/path/to/file" ]; then
      echo "File does not exist."
  fi
  ```

### **6. Nested `if` Statements**
Bash allows nesting `if` statements inside each other. This is useful for checking multiple conditions that depend on each other.

**Example:**
```bash
if [ -d "/path/to/directory" ]; then
    if [ -w "/path/to/directory" ]; then
        echo "Directory exists and is writable."
    else
        echo "Directory exists but is not writable."
    fi
else
    echo "Directory does not exist."
fi
```

### **7. Using `case` Statement**
The `case` statement is useful for checking a variable against multiple values.

```bash
case $variable in
    pattern1)
        # commands for pattern1
        ;;
    pattern2)
        # commands for pattern2
        ;;
    *)
        # default commands
        ;;
esac
```

**Example:**
```bash
read -p "Enter a letter grade: " grade
case $grade in
    "A")
        echo "Excellent!"
        ;;
    "B")
        echo "Good job!"
        ;;
    "C")
        echo "Satisfactory."
        ;;
    *)
        echo "Grade not recognized."
        ;;
esac
```

### **8. Testing Exit Status**
In Bash, each command returns an exit status (0 for success, non-zero for failure). You can use `$?` to test this.

**Example:**
```bash
ls /some/directory
if [ $? -eq 0 ]; then
    echo "Directory listing successful."
else
    echo "Failed to list directory."
fi
```

### **9. Best Practices**
   - **Quoting Variables**: Always enclose variables in double quotes (`"$var"`) to avoid issues with spaces or empty values.
   - **Indentation**: Indent commands inside `if` blocks for readability.
   - **Error Handling**: Consider using `exit` with a non-zero status for error handling in complex scripts.
