
### 1. Allow Incoming `SSH` Traffic

Allow `SSH` (port 22) for remote server access:

```bash
sudo iptables -I INPUT 2 -p tcp --dport 22 -j ACCEPT
```

### 2. Allow `HTTP` and `HTTPS` Traffic

Enable web server traffic (ports 80 and 443):

```bash
sudo iptables -I INPUT 3 -p tcp --dport 80 -j ACCEPT
sudo iptables -I INPUT 4 -p tcp --dport 443 -j ACCEPT
```

### 3. Allow `postgres` Traffic

Allow `postgres` (port 5432) for database access:

```bash
sudo iptables -I INPUT 2 -p tcp --dport 5432 -j ACCEPT
```

