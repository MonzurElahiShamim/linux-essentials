# Input/Output (I/O) Redirection

>[!gemini]- Summarized
>**Input/Output (I/O) Redirection**
> 
> **Standard Streams**:
> - Essential channels for communication between programs and the operating system:
>   - **STDIN**: Standard input (user input from the keyboard)
>   - **STDOUT**: Standard output (normal output from commands)
>   - **STDERR**: Standard error (error messages from commands)
> 
> **I/O Redirection**:
> - Directing data from standard streams to or from files:
>   - **`<`**: Redirects STDIN from a file
>   - **`>`**: Redirects STDOUT to a file
>   - **`2>`**: Redirects STDERR to a file
> 
> **STDOUT Redirection**:
> - Directs output of commands to a file:
>   - **`>`**: Overwrites existing content of a file
>   - **`>>`**: Appends output to the end of a file
> 
> **STDERR Redirection**:
> - **Purpose**: Captures and stores error messages in a file
> - **Syntax**: `2>`
> - **Example**: `ls /fake 2> error.txt` (sends error message to `error.txt`)
> 
> **Redirecting Multiple Streams**:
> - Simultaneous redirection of STDOUT and STDERR:
>   - **`&>`**: Combined `1>` and `2>`
>   - Redirects both streams to the same or different files
> 
> **STDIN**:
> - Typically used for keyboard input, but can be redirected from files using `<`
> - **Purpose**: Automation, integration, and piping data between commands
> 
> **Examples**:
> - **Basic Redirection**: `tr 'a-z' 'A-Z' < example.txt` (converts lowercase to uppercase from `example.txt`)
> - **Piping with STDIN**: `cat file.txt | grep "pattern"` (searches for a pattern in `file.txt`)
> 
> **Saving Output**:
> - After redirecting STDIN: `tr 'a-z' 'A-Z' < example.txt > newexample.txt` (saves uppercase transformation to `newexample.txt`)

**Standard Streams**: Standard streams in Unix/Linux systems are predefined input and output channels used for communication between programs and the operating system. They are essential for handling user input, displaying program output, and logging errors.

> [!info] Learn more
> [[Standard Stream|More on Standard Stream]]
  
  - **STDIN**: 
    - **Definition**: Standard input.
    - **Source**: User input from the keyboard.
  - **STDOUT**: 
    - **Definition**: Standard output.
    - **Source**: Normal output from commands.
    - **Stream Number**: `Channel #1`.
  - **STDERR**: 
    - **Definition**: Standard error.
    - **Source**: Error messages from commands.
    - **Stream Number**: `Channel #2`.

- **I/O Redirection**:
  - **Purpose**: Redirect data from standard streams.
  - **Redirection Symbols**:
    - **`<`**: Redirects **STDIN** from a file.
    - **`>`**: Redirects **STDOUT** to a file.
    - **`2>`**: Redirects **STDERR** to a file.
    - **`&>`**: Redirects both **STDOUT** & **STDERR** to a file.
  - ![](Input-Output%20Redirection.png)
## STDOUT Redirection

- **Definition**: Standard output (STDOUT) is the default stream for displaying command results.
- **Default Behavior**: Prints output to the terminal window.
- **Redirecting Output**:
  - **To File**: Use `>` to write output to a file (overwrites existing content).
    ```bash
    echo "text" > file.txt
    ```
  - **Append to File**: Use `>>` to add output to the end of a file (preserves existing content).
    ```bash
    echo "more text" >> file.txt
    ```

## STDERR Redirection

- **Basic Redirection**:
  - Redirect STDERR (stream #2) to a file using `2>`.
    ```bash
    ls /fake 2> error.txt # use 2>> to append
    ```
  - **Captures error messages** and stores them in the specified file.

- **Example**:
  - Command producing error:
    ```bash
    ls /fake
    ```
  - Redirecting STDERR:
    ```bash
    ls /fake 2> error.txt
    ```
  - **Verification**:
    ```bash
    cat error.txt
    ```
  - Output:
    ```
    ls: cannot access /fake: No such file or directory
    ```

- **Identifying STDERR**:
  - ! If STDOUT is redirected but output still appears in the terminal, the visible output is likely STDERR.
    ```bash
    ls /fake > output.txt
    ```

- **Purpose**:
  - Useful for separating error messages from regular output, facilitating error logging and debugging.

## Redirecting Multiple Streams

**STDOUT and STDERR can be redirected to files simultaneously.**

#### Example Scenario:
```bash
sysadmin@localhost:~$ ls /fake /etc/ppp
```
- **Output**:
  ```plaintext
  ls: cannot access /fake: No such file or directory
  /etc/ppp:
  ip-down.d  ip-up.d
  ```

### Redirecting STDOUT Only:
```bash
sysadmin@localhost:~$ ls /fake /etc/ppp > example.txt
```
- **Result**:
  - **Screen**: `ls: cannot access /fake: No such file or directory`
  - **File**: 
    ```plaintext
    /etc/ppp:
    ip-down.d
    ip-up.d
    ```

### Redirecting STDERR Only:
```bash
sysadmin@localhost:~$ ls /fake /etc/ppp 2> error.txt
```
- **Result**:
  - **Screen**: 
    ```plaintext
    /etc/ppp:
    ip-down.d
    ip-up.d
    ```
  - **File**: 
    ```plaintext
    ls: cannot access /fake: No such file or directory
    ```

### Redirecting Both STDOUT and STDERR to the Same File:
```bash
sysadmin@localhost:~$ ls /fake /etc/ppp &> all.txt
```
- **Result**:
  - **File**: 
    ```plaintext
    ls: cannot access /fake: No such file or directory
    /etc/ppp:
    ip-down.d
    ip-up.d
    ```

### Redirecting Both STDOUT and STDERR to Different Files:
```bash
sysadmin@localhost:~$ ls /fake /etc/ppp > example.txt 2> error.txt
```
- **Result**:
  - **STDOUT File**: 
    ```plaintext
    /etc/ppp:
    ip-down.d
    ip-up.d
    ```
  - **STDERR File**: 
    ```plaintext
    ls: cannot access /fake: No such file or directory
    ```

#### Notes:
- The **&>** symbol combines both `1>` (STDOUT) and `2>` (STDERR).
- Order of specifying streams does not affect the outcome.

## STDIN
Redirecting STDIN (Standard Input) in Linux is indeed less common compared to redirecting STDOUT (Standard Output) and STDERR (Standard Error), but it can be useful in specific scenarios. Here’s a summary based on the information provided:

1. **STDIN Basics**:
   - STDIN is typically used for input from the keyboard if no file name is specified as an argument to a command.
   - For commands like `cat` or `tr`, if no file name is provided, they read from STDIN.

2. **Redirecting STDIN**:
   - **Using `<`**: The `<` character is used to redirect input from a file to STDIN of a command. For example:
     ```
     tr 'a-z' 'A-Z' < example.txt
     ```
     This command takes the contents of `example.txt` as input to `tr`.

3. **Why Redirect STDIN?**:
   - **Automation**: Redirecting STDIN allows scripts to feed data into commands without manual input.
   - **Integration**: Some commands or scripts may require data from STDIN rather than a file name as an argument.
   - **Piping**: It enables piping data between commands where the output of one command becomes the input (via STDIN) of another.

4. **Examples**:
   - **Basic Usage**: `tr 'a-z' 'A-Z' < example.txt` translates lowercase characters in `example.txt` to uppercase.
   - **Piping**: `cat file.txt | grep "pattern"` uses STDOUT of `cat` as STDIN for `grep`.

5. **Saving Output**:
   - Redirecting the output of a command that uses STDIN can be done using `>`. For example:
     ```
     tr 'a-z' 'A-Z' < example.txt > newexample.txt
     ```
     This saves the uppercase transformation of `example.txt` into `newexample.txt`.

In summary, while redirecting STDIN is less common than redirecting STDOUT and STDERR, it's essential for automation, scripting, and integrating commands that expect input from STDIN rather than file names as arguments.

 