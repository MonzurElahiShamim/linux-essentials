# Viewing and Managing Rules

## 1. List Rules:    

```bash
sudo iptables -L --line-numbers
```

## 2. Delete a Rule

Delete a rule by its position:    
```bash
sudo iptables -D INPUT <rule_number>
```

## 3. Flush All Rules

Reset `iptables`:    
```bash
sudo iptables -F
```

>[!warning]
> Consider Safe Flush: [Safely flush](Safely%20flush.md)
 
## 4. Save Rules

Persist rules across reboots:    
```bash
sudo iptables-save | sudo tee /etc/iptables/rules.v4
```

