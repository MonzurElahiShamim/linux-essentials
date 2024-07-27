---
updated_at: 2024-07-13T19:42:43.659+06:00
edited_seconds: 960
---
# Vim Editor Overview

Vim (Vi IMproved) is a highly configurable text editor built to enable efficient text editing. It's widely used in Unix-like operating systems and supports various programming languages and file formats.

### Key Features:

- **Modal Editing**: Vim operates in different modes:
  - **Normal mode**: For navigation, manipulation, and commands.
  - **Insert mode**: For inserting text.
  - **Visual mode**: For selecting blocks of text.
  - **Command-line mode**: For entering commands.

- **Extensibility**: Vim supports plugins and customizations to enhance functionality.

> [!tip] `vimtutor`
`vimtutor` is a good command line tool to learn vim
## Frequently Used Key Combinations:

### Switching Modes:

  - **Normal to Insert mode**: `i` (insert before cursor), `a` (insert after cursor), `I` (insert at the beginning of the line), `A` (insert at the end of the line).
  - **Insert to Normal mode**: `Esc` key.

### Movement:

  - **Navigate**: 
    - up: `k` or :LiMoveUp: `(up arrow)`
    - down: `j` or :LiMoveDown: `(down arrow)`
    - right: `l` or :LiMoveRight: `(right arrow)`
    - left: `h` or :LiMoveLeft: `(left arrow)`
		![[Pasted image 20240630002255.png]]

  - **Word**: `w` (forward), `b` (backward).
  - **Line**: `0` (beginning), `^` (first non-blank character), `$` (end).
  - **Page**: `Ctrl + f` (forward), `Ctrl + b` (backward).

### Editing:

  - **Copy, Cut, Paste**: `yy` (copy line), `dd` (cut line), `p` (paste).
  - **Undo, Redo**: `u` (undo), `Ctrl + r` (redo).
  - **Delete**: `x` (delete character), `dw` (delete word).

### Search and Replace:

  - **Search**: `/` (forward search), `?` (backward search), `n` (next match), `N` (previous match).
  - **Replace**: `:s/old/new/g` (replace `old` with `new` globally).

### Saving and Exiting:

  - **Save**: `:w` (save), `:wq` (save and quit).
  - **Quit without saving**: `:q!` (force quit).


