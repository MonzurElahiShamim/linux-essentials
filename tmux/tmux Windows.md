# tmux Windows

## 1. Overview

- **Windows** in `tmux` function like virtual workspaces within a single session.
- Each **window** can hold multiple **panes** and run different commands.
- You can switch between windows without affecting the running processes in other windows.

## 2. Basic Commands

### Creating and Managing Windows

- **Create a new window**:
    
    ```sh
    Ctrl-b c
    ```
    
- **List all windows**:
    
    ```sh
    Ctrl-b w
    ```
    
- **Rename the current window**:
    
    ```sh
    Ctrl-b ,  
    ```
    
    - Enter a new name and press `Enter`.
- **Close the current window**:
    
    ```sh
    Ctrl-b &  
    ```
    

### Switching Between Windows

- **Go to the next window**:
    
    ```sh
    Ctrl-b n  
    ```
    
- **Go to the previous window**:
    
    ```sh
    Ctrl-b p  
    ```
    
- **Go to a specific window by number**:
    
    ```sh
    Ctrl-b <window-number>  
    ```
    
- **Switch between the last two active windows**:
    
    ```sh
    Ctrl-b l  
    ```
    

## 3. Advanced Usage

- **Move a window to a different index**:
    
    ```sh
    Ctrl-b .  
    ```
    
    - Enter the new index and press `Enter`.
- **Kill all windows except the current one**:
    
    ```sh
    tmux kill-window -a  
    ```
    
- **Detach from a session without closing windows**:
    
    ```sh
    Ctrl-b d  
    ```
    
    - Reattach later using `tmux attach-session`.
