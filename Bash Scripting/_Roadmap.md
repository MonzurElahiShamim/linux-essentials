# Roadmap for learning Bash scripting:

### 1. **Setup and Basics**
   - Create a `.sh` file and make it executable (`chmod +x script.sh`).
   - Practice `echo "Hello World"` to understand script execution.
   - Learn variable declaration (`my_var="value"`) and printing (`echo $my_var`).

### 2. **Control Flow**
   - **Conditionals**: Use `if [ condition ]; then ... fi` to write basic condition checks.
   - **Loops**: Try `for` and `while` loops to repeat commands. Example: `for i in {1..5}; do echo $i; done`.
   - **Functions**: Define a function (`my_func() { ... }`) and call it (`my_func`).

### 3. **Working with User Input**
   - Use `read` to accept input (e.g., `read name`), and print the input (`echo "Hello, $name"`).
   - Work with script arguments: `echo $1` for first argument, `"$@"` for all arguments.

### 4. **Text Processing and Redirection**
   - Redirect output: Use `>` for overwrite and `>>` to append.
   - Practice basic tools: `grep "pattern"`, `sed 's/foo/bar/'`, `awk '{print $1}'`, and `cut -d':' -f1`.
   - Pipe commands (e.g., `ls | grep "txt"`).

### 5. **File Management**
   - Use `ls`, `cp`, `mv`, and `rm` for file operations.
   - Try `find /path -name "*.txt"` to locate files by name.
   - Count lines, words, etc., with `wc -l`, `wc -w`, and so on.

### 6. **Automation Tasks**
   - **System Monitor**: Write a script that runs `top -bn1 | grep "Cpu"` and `free -m`.
   - **File Backup**: Use `tar -czf backup.tar.gz /path/to/dir` for backups.
   - **Log Cleanup**: Automate log deletion (`find /path/to/logs -type f -name "*.log" -delete`).

### 7. **Error Handling and Debugging**
   - **Error Codes**: Check `if [ $? -ne 0 ]; then echo "Error"; fi`.
   - **Debug Mode**: Run `bash -x script.sh` to trace script execution.

### 8. **Practice Projects**
   - Write scripts for specific tasks (file organization, system health checks).
   - Use conditional execution (`&&`, `||`) in small scripts.

Let me know if you'd like more examples for any step! 