---
updated_at: 2024-07-06T11:22:56.127+06:00
edited_seconds: 110
---
# `cat` Command

The `cat` command, short for "*concatenate*" is a fundamental utility in Unix-like operating systems. 
It is used to 
- display, 
- create, 
- redirect, and 
- combine text files.

#### **1. Display File Contents**

Use `cat` to read and display the contents of a text file in the terminal.

**Command**:
```bash
cat file.txt
```

**Example**:
```bash
cat food.txt
```
**Output**:
```
Food is good.
```

#### **2. Create a New File**
You can create a new text file and add content to it with `cat`.
**Command**:
```bash
cat > newfile.txt
```
**Usage**:
- Enter text directly into the terminal.
- Press `Ctrl+D` to save and exit.

**Example**:
```bash
cat > notes.txt
# (Type your content and press `Ctrl+D` to finish)
```

#### **3. Redirect Output to a File**

`cat` can redirect the contents of a file to another file using the `>` character, which overwrites the target file, or `>>`, which appends to the target file.

**Commands**:
- **Overwrite**: `cat file.txt > output.txt`
- **Append**: `cat file.txt >> output.txt`

**Example**:
```bash
cat file.txt > copy.txt  # Overwrites copy.txt with the contents of file.txt
cat file.txt >> append.txt  # Appends the contents of file.txt to append.txt
```

#### **4. Combine Multiple Files**

Combine and display or save the contents of multiple files into one using `cat`.

**Command**:
```bash
cat file1.txt file2.txt > combined.txt
```

**Example**:
```bash
cat part1.txt part2.txt > whole.txt
```
This command merges `part1.txt` and `part2.txt` into `whole.txt`.

### **Summary**

The `cat` command is versatile and simple, providing essential functionality for managing text files. Here’s a quick reference:

- **Display**: `cat file.txt`
- **Create**: `cat > newfile.txt` (press `Ctrl+D` to save)
- **Redirect**: `cat file.txt > output.txt` or `cat file.txt >> output.txt`
- **Combine**: `cat file1.txt file2.txt > combined.txt`

These operations make `cat` a valuable tool for various text file manipulations in Unix-like systems.