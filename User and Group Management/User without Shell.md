## Creating a Linux User Without an Interactive Shell

### Steps

- **Create user with no shell access**
    
    ```bash
    sudo useradd -s /usr/sbin/nologin username
    ```
    
    Example:
    ```bash
    sudo useradd -s /usr/sbin/nologin backupuser
    ```
    
- **Verify settings**
    
    ```bash
    getent passwd backupuser
    ```

### Best Practices
- Use `/usr/sbin/nologin` instead of `/bin/false` (gives a friendly “Account not available” message).
- Ideal for service accounts or automated processes.
- Combine with expiry date for better security.
