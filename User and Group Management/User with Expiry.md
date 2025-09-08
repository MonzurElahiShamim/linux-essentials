## Creating a Linux User with an Expiry Date

### Steps

- **Create the user with expiry date in one command**
    
    ```bash
    sudo useradd -e YYYY-MM-DD username
    ```
    
    Example:
    ```bash
    sudo useradd -e 2025-12-31 john
    ```
    
- **Verify expiry date**
    
    ```bash
    sudo chage -l john
    ```
    
- **Change expiry date later**
    
    ```bash
    sudo usermod -e 2026-01-31 john
    ```
    

### Best Practices
- Always verify with `chage -l` after setting.
- Use ISO format `YYYY-MM-DD` for clarity.
- Document user creation and expiry in an admin log.
