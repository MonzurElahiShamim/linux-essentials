# `tee` Command in Linux

#### Overview: 
- `tee` reads input and writes to both the screen and files. 
- It’s used to view and save command output simultaneously.
- It handles permission issues that standard redirection methods (`>>`) cannot.

##### Basic Usage: 
  ```bash
  command | tee [options] file1 [file2 ...]
  ```
  Displays the output and saves it to specified files.

- **Appending Output**: Use `-a` to append instead of overwriting.
  ```bash
  echo "New data" | tee -a log.txt
  ```

##### Key Features:
  - **Display and Save**: Shows output while saving it.
  - **Error Handling**: Continues showing output even if file write fails.
  - **Logging and Debugging**: Useful for monitoring output in real time.

#### Examples:
  1. **Display and Save Output**:
     ```bash
     ls -l | tee output.txt
     ```
     Lists directory contents, displays them, and saves to `output.txt`.

  2. **Appending Data**:
     ```bash
     date | tee -a log.txt
     ```
     Appends the current date to `log.txt`.

#### Using `tee` with `sudo`:
  - **Why**: Direct `>>` with `sudo` doesn’t work due to shell permission handling.
  - **When**: Write to protected files needing root access, like `/etc/hosts`.
  - **Example**:
    ```bash
    echo "127.0.0.1 mysite.local" | sudo tee -a /etc/hosts
    ```
    Appends to `/etc/hosts` with elevated permissions.

#### Use Cases:
  - **Monitoring and Saving**: Great for capturing command outputs while seeing them.
  - **System Administration**: Useful for updating configuration files with root access.
  - **Quiet Output Suppression**: Use `> /dev/null` to suppress output on screen.

### Summary
`tee` is valuable when you need to display and save command output, especially when dealing with system files or debugging. It handles permission issues that standard redirection methods (`>>`) cannot, making it a crucial tool for Linux users.

