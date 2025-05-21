# `bat` : An upgrade to `cat`

[video tutorial-learnlinuxtv](https://youtu.be/myg9zTf5aC8?si=ysJh_epKvthnpqUt)

`batcat`, often referred to as `bat`, is an enhanced alternative to the classic `cat` command, offering several advanced features for viewing files:

### Key Features
1. **Syntax Highlighting**: Highlights syntax for numerous programming and markup languages.
2. **Git Integration**: Shows changes relative to the Git repository.
3. **Line Numbers**: Displays line numbers by default.
4. **File Pager**: Functions like `less` for scrolling through large files.
5. **Themes**: Supports customizable themes for syntax highlighting.

### Installation
- **Debian-based systems**:
  ```bash
  sudo apt install batcat
  ```

### Usage
- View a file:
  ```bash
  batcat filename
  ```
- Use as a pager:
  ```bash
  batcat filename | less
  ```

### Configuration
Customize via `~/.config/bat/config` for options like themes and line numbers.

### Conclusion
`batcat` improves file viewing with syntax highlighting, git integration, and more, making it a valuable tool for developers and sysadmins.