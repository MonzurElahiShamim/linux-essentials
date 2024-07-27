---
updated_at: 2024-07-13T19:31:20.645+06:00
edited_seconds: 160
---
# Standard Streams

Standard streams in Unix/Linux systems are predefined input and output channels used for communication between programs and the operating system. They are essential for handling user input, displaying program output, and logging errors.

## 1. Standard Input (STDIN)
- **Stream Number**: 0
- **Function**: Receives input data for commands and programs.
- **Default Source**: Keyboard.
- **Usage**:
  - Commands prompt for input via STDIN.
  - Can be redirected to take input from a file or another command.
  - **Example**:
    ```bash
    # Taking input from a file
    command < input.txt
    ```

## 2. Standard Output (STDOUT)
- **Stream Number**: 1
- **Function**: Outputs the results of commands and programs.
- **Default Destination**: Terminal screen.
- **Usage**:
  - Typically displays command results.
  - Can be redirected to a file or another command.
  - **Example**:
    ```bash
    # Redirecting output to a file
    command > output.txt
    ```

## 3. Standard Error (STDERR)
- **Stream Number**: 2
- **Function**: Outputs error messages.
- **Default Destination**: Terminal screen.
- **Usage**:
  - Separates error messages from regular output.
  - Can be redirected to a file to log errors.
  - **Example**:
    ```bash
    # Redirecting errors to a file
    command 2> error.txt
    ```

## Redirection and Usage

- **Redirection**:
  - **Input Redirection**: Use `<` to take input from a file.
    ```bash
    command < input.txt
    ```
  - **Output Redirection**: Use `>` to send output to a file (overwrites existing content).
    ```bash
    command > output.txt
    ```
  - **Appending Output**: Use `>>` to append output to a file.
    ```bash
    command >> output.txt
    ```
  - **Error Redirection**: Use `2>` to send errors to a file.
    ```bash
    command 2> error.txt
    ```
  - **Combined Redirection**: Use `&>` to redirect both STDOUT and STDERR to the same file.
    ```bash
    command &> output.txt
    ```

- **Pipes**: Use `|` to pass output from one command as input to another.
  ```bash
  command1 | command2
  ```

> [!info] Learn more
> More on [[Input-Output Redirection]]
## Examples and Use Cases

- **Separate Output and Error**:
  ```bash
  command > output.txt 2> error.txt
  ```

- **Combine Output and Error**:
  ```bash
  command &> combined.txt
  ```

- **Chain Commands with Pipes**:
  ```bash
  ls / | grep "file" | wc -l
  ```
