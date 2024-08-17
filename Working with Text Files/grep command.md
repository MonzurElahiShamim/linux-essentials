---
updated_at: 2024-08-17T19:08:36.065+06:00
edited_seconds: 420
---
# `grep` Command in Linux

The `grep` command is one of the most widely used and powerful tools in Linux for searching text files. Its name stands for ***G***lobally search a ***R***egular ***E***xpression and ***P***rint.

## Basic Syntax of `grep`

```
grep [OPTIONS] PATTERN [FILE...]
```
- **`PATTERN`**: The text or regular expression that you are searching for.
- **`FILE`**: The file(s) in which you want to search.

---
## Exit Status of `grep`
`grep` provides an exit status that can be used in scripts for conditional execution:
- `0`: If a match was found.
- `1`: If no match was found.
- `2`: If an error occurred (e.g., file not found).

---

## Common Usage of `grep`

#### 1. Searching for a Word in a File
```
grep "word" file.txt
```
- This searches for the word "word" in `file.txt` and prints the lines containing it.

#### 2. Case-Insensitive Search
```
grep -i "word" file.txt
```
- The `-i` option makes the search case-insensitive, matching both "Word", "WORD", and "word".

#### 3. Search in Multiple Files
```
grep "word" file1.txt file2.txt
```
- This searches for "word" in both `file1.txt` and `file2.txt`.

#### 4. Recursive Search in Directories
```
grep -r "word" /path/to/directory
```
- The `-r` option searches recursively through all files in the specified directory and its subdirectories.

#### 5. Displaying Line Numbers
```
grep -n "word" file.txt
```
- The `-n` option prints the line number where the word appears, useful for pinpointing locations.

---

## Advanced `grep` Features

#### 1. Inverted Search (Display Non-Matching Lines)
```
grep -v "word" file.txt
```
- The `-v` option displays all lines that do **not** contain "word".

#### 2. Counting Matches
```
grep -c "word" file.txt
```
- The `-c` option counts the number of lines containing the pattern instead of printing the actual matches.

#### 3. Search for Whole Words
```
grep -w "word" file.txt
```
- The `-w` option restricts matches to whole words. Without this option, "word" would also match "sword" or "wording".

#### 4. Display Only Matching Parts of the Line
```
grep -o "word" file.txt
```
- The `-o` option only prints the matched part of the line, not the entire line.

#### 5. Search with Regular Expressions
- `grep` supports basic regular expressions (BRE). By using the `-E` option, it switches to extended regular expressions (ERE).
  
**Basic Regular Expression Example:**
```
grep "w.rd" file.txt
```
- Matches "word", "ward", "w1rd", and so on (any single character in place of `.`).

**Extended Regular Expression Example:**
```
grep -E "w(ord|ard)" file.txt
```
- Matches both "word" and "ward".

#### 6. Fixed String Search (No Regular Expression)
```
grep -F "word" file.txt
```
- The `-F` option treats the pattern as a fixed string, not a regular expression. It’s useful when you want to match special characters literally.

#### 7. Show Context Around Matches
- To display lines before and/or after the matched line, use the following options:
  
**Show 3 lines before match:**
```
grep -B 3 "word" file.txt
```
- The `-B` (before) option displays the specified number of lines before the match.

**Show 2 lines after match:**
```
grep -A 2 "word" file.txt
```
- The `-A` (after) option shows the specified number of lines after the match.

**Show 2 lines before and 2 lines after match:**
```
grep -C 2 "word" file.txt
```
- The `-C` (context) option shows both before and after lines.

---

## Other Useful `grep` Options

#### 1. Print File Names Containing the Match
```
grep -l "word" *.txt
```
- The `-l` option lists only the names of the files that contain the pattern, without displaying the matching lines.

#### 2. Suppress Output (Exit Status Only)
```
grep -q "word" file.txt
```
- The `-q` (quiet) option suppresses all output. It returns a success (exit status `0`) if the pattern is found, otherwise, it returns a failure (exit status `1`). This is useful in scripts for checking if a string exists in a file.

#### 3. Show Number of Matches per File
```
grep -H "word" *.txt
```
- The `-H` option includes the file name in the output, useful when searching through multiple files.

#### 4. Binary File Search
```
grep -a "word" binaryfile.bin
```
- The `-a` option treats binary files as if they were text, allowing `grep` to search through binary files.

---

## `grep` with Piping

The `grep` command is often used in conjunction with other Linux commands using pipes (`|`) to filter output.

#### 1. Search Within Command Output
```
ps aux | grep "root"
```
- This command displays only the lines containing "root" from the output of the `ps aux` command, which lists all running processes.

#### 2. Filtering Output from Log Files
```
dmesg | grep "error"
```
- Filters system messages to display only the ones containing "error".

#### 3. Combining Multiple Commands
```
ls -l | grep "^d"
```
- Lists only directories (as indicated by `^d` at the beginning of the line) from the `ls -l` output.

---

## Real-World Examples

#### 1. Searching Logs for Errors
```
grep -i "error" /var/log/syslog
```
- Searches the system logs for any mention of "error" (case-insensitive), useful for diagnosing issues.

#### 2. Extracting IP Addresses from a File
```
grep -Eo "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" file.txt
```
- Uses a regular expression to extract IP addresses from the file, printing only the matching parts.

---
---
