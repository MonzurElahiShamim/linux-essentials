
### Allow Traffic from a Specific IP

Permit traffic from a trusted IP (e.g., 192.168.1.100):

```bash
sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT
```

### Block Traffic from a Specific IP

Deny access from a suspicious IP (e.g., 203.0.113.5):

```bash
sudo iptables -A INPUT -s 203.0.113.5 -j DROP
```

