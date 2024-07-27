---
updated_at: 2024-07-13T19:24:19.108+06:00
edited_seconds: 770
---
# Viewing files in Terminal
## Using [[cat Command]]

**Command**
```bash
cat file.txt
```
- ! **Caution**: Not ideal for large files as it dumps all contents to the screen.

> More about [[cat Command]]
## Using a Pager

- **Pager Commands for Large Files**:
  - **`less`**: Advanced paging, default in many systems.
  - **`more`**: Simpler, always available, fewer features.
- **Navigation**: Both use similar keystrokes to move through the document.

> Use **`less`** for advanced paging; **`more`** for compatibility across all systems.
### Pager Movement Commands (`less` and `more`)

#### Using `less`

- **Open File**:
  ```bash
  less filename
  ```
  Example: 
  ```bash
  less words
  ```

- **Common Movement Commands**:

| Key        | Movement        |
| ---------- | --------------- |
| Spacebar   | Window forward  |
| `b`        | Window backward |
| Enter      | Line forward    |
| `y`, `k`   | Line Backward   |
| `q`        | Exit            |
| `h` or `H` | Help            |

- **Help**:
  - Press `h` or `H` to display the help screen.

### Pager Searching Commands (`less`)

#### Forward Search

- **Start Search**:
  - Press `/` followed by the search term, then Enter.
  ```bash
  /search_term
  ```
  Example: 
  ```bash
  /frog
  ```

- **Result**:
  - Cursor moves to the first match.
  - All matches are highlighted.

#### Backward Search

- **Start Search**:
  - Press `?` followed by the search term, then Enter.
  ```bash
  ?search_term
  ```
  Example:
  ```bash
  ?frog
  ```

- **Result**:
  - Cursor moves to the first backward match.

#### Navigating Matches

- **Next Match**:
  - Press `n` to move to the next occurrence.
- **Previous Match**:
  - Press `Shift+N` to move to the previous occurrence.

> [!note]+ NOTE
> **Pattern Matching**:
>   - Uses ***regular expressions*** for searches.
  
#### Usage Example

```bash
# Search for "frog" forward
/ frog

# Search for "frog" backward
? frog

# Move to next match
n

# Move to previous match
Shift + N
```

## Using `head` and `tail` Commands

### Head Command

- **Usage**: Display the first few lines of a file or input.
  ```bash
  head [options] [file]
  ```

- **Default Behavior**: Displays the first 10 lines of the specified file.

- **Options**:
  - `-n NUM` or `-NUM`: Display the first `NUM` lines.
    ```bash
    head -3 /etc/sysctl.conf
    # Or
    head -n 3 /etc/sysctl.conf
    ```
    Displays the first 3 lines of `/etc/sysctl.conf`.

### Tail Command

- **Usage**: Display the last few lines of a file or input.
  ```bash
  tail [options] [file]
  ```

- **Default Behavior**: Displays the last 10 lines of the specified file.

- **Options**:
  - `-n NUM`: Display the last `NUM` lines.
    ```bash
    tail -n 5 /etc/sysctl.conf
    ```
    Displays the last 5 lines of `/etc/sysctl.conf`.

  - `-n +NUM`: Display from line `NUM` to the end.
    ```bash
    tail -n +25 /etc/passwd
    ```
    Displays from line 25 to the end of `/etc/passwd`.

#### Real-time File Monitoring

- **Usage**: Monitor changes in a file in real-time.
  ```bash
  tail -f /var/log/mail.log
  ```

- **Functionality**: Continuously displays appended data as it's written to the file, useful for monitoring log files or live updates.

#### Considerations

- **Practical Use**: Helpful for monitoring log files during system troubleshooting or tracking ongoing changes in critical files.

- **Interactive Viewing**: Allows system administrators to view and respond to real-time changes without needing to reload the entire file.

Using `head` and `tail` commands efficiently manages file content viewing, aiding in tasks like log analysis and quick file inspections in Unix/Linux environments.