# Safely flush iptables


### 1. Script with Timestamped Backup

```bash
#!/bin/bash

# Define backup directory and file
BACKUP_DIR="$HOME/iptables_rules"
mkdir -p "$BACKUP_DIR"
TIMESTAMP=$(date +"%Y%m%d_%H%M%S")
BACKUP_FILE="$BACKUP_DIR/backup_$TIMESTAMP.rules"

# Ask for confirmation to back up iptables rules
read -p "Do you want to back up the current iptables rules to $BACKUP_FILE? (y/n): " CONFIRM_BACKUP

if [[ "$CONFIRM_BACKUP" =~ ^[Yy]$ ]]; then
    # Backup current iptables rules
    echo "Backing up to $BACKUP_FILE"
    sudo iptables-save > "$BACKUP_FILE"
else
    echo "Backup skipped."
fi

# Add SSH rule to avoid lockout
echo "Allowing SSH"
sudo iptables -I INPUT 1 -p tcp --dport 22 -j ACCEPT

# Flush existing rules and reapply necessary ones
echo "Flushing and reapplying ssh and icmp rules"
sudo iptables -F
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT  # SSH
sudo iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT  # Established connections
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT  # Ping

```

---

### 2. Steps to Execute:

1. **Create and Edit Script:**
    
    ```bash
    touch Safe_iptables_flush.sh
    nano Safe_iptables_flush.sh
    ```
    
    (Paste the script above)
    
2. **Make the Script Executable:**
    
    ```bash
    chmod +x Safe_iptables_flush.sh
    ```
    
3. **Run the Script:**
    
    ```bash
    ./Safe_iptables_flush.sh
    ```
    
4. **Verify Current Rules:**
    
    ```bash
    sudo iptables -L -v
    ```

---

### 3. Restoring iptables Rules ( `if necessary` )

To restore iptables from a backup:

1. **Locate the Backup File** (`backup_YYYYMMDD_HHMMSS.rules`).
    
2. **Restore Rules:**
    
    ```bash
    sudo iptables-restore < /path/to/backup_file.rules
    ```
    
3. **Verify Restored Rules:**
    
    ```bash
    sudo iptables -L -v
    ```
    

---

### **4. Best Practices:**

- **Backup Before Changes:** Always back up iptables before flushing or modifying rules.
- **Ensure SSH Access:** Reapply SSH access rules to avoid lockout.
- **Use Timestamped Backups:** Use the timestamp in filenames to keep multiple backups.
