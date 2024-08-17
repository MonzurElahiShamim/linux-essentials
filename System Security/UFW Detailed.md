---
updated_at: 2024-08-01T15:25:06.694+06:00
edited_seconds: 160
---
## Detailed Note on UFW (Uncomplicated Firewall) Configuration

UFW (Uncomplicated Firewall) is a user-friendly frontend for managing iptables firewall rules. It is designed to make firewall configuration easier and straightforward for beginners. This guide provides a detailed note on configuring UFW on a Linux system.

### Installation

Before configuring UFW, ensure it is installed on your system.

**Ubuntu/Debian:**
```bash
sudo apt update
sudo apt install ufw
```

**CentOS/RHEL (via EPEL repository):**
```bash
sudo yum install epel-release
sudo yum install ufw
```

**Arch Linux:**
```bash
sudo pacman -S ufw
```

### Basic UFW Commands

#### Enable and Disable UFW

- **Enable UFW:**
  ```bash
  sudo ufw enable
  ```

- **Disable UFW:**
  ```bash
  sudo ufw disable
  ```

#### Status of UFW

- **Check UFW status:**
  ```bash
  sudo ufw status
  ```

- **Check UFW status in numbered mode:**
	```bash
  sudo ufw status numbered
	```

- **Check UFW status in verbose mode:**
  ```bash
  sudo ufw status verbose
  ```

#### Default Policies

Setting default policies is crucial as they define the basic behavior of the firewall. Typically, you want to deny incoming traffic and allow outgoing traffic.

- **Set default to deny all incoming connections:**
  ```bash
  sudo ufw default deny incoming
  ```

- **Set default to allow all outgoing connections:**
  ```bash
  sudo ufw default allow outgoing
  ```

### Allowing and Denying Specific Connections

#### Allowing Connections

- **Allow a specific port (e.g., SSH on port 22):**
  ```bash
  sudo ufw allow 22
  ```

- **Allow a specific service by name (e.g., HTTP):**
  ```bash
  sudo ufw allow http
  ```

- **Allow a port range (e.g., ports 3000 to 4000):**
  ```bash
  sudo ufw allow 3000:4000/tcp
  ```

- **Allow connections from a specific IP address:**
  ```bash
  sudo ufw allow from 192.168.1.100
  ```

- **Allow connections from a specific subnet (e.g., 192.168.1.0/24):**
  ```bash
  sudo ufw allow from 192.168.1.0/24
  ```

- **Allow connections to a specific port from a specific IP using specific protocol:**
  ```bash
  sudo ufw allow from 192.168.1.100 to any port 22 proto tcp
  ```

#### Denying Connections

- **Deny a specific port:**
  ```bash
  sudo ufw deny 22
  ```

- **Deny a specific service by name:**
  ```bash
  sudo ufw deny http
  ```

- **Deny connections from a specific IP address:**
  ```bash
  sudo ufw deny from 192.168.1.100
  ```

### Advanced UFW Configuration

#### Application Profiles

UFW uses application profiles to simplify the process of allowing or denying connections for specific services.

- **List available application profiles:**
  ```bash
  sudo ufw app list
  ```

- **Get detailed information about a profile (e.g., OpenSSH):**
  ```bash
  sudo ufw app info OpenSSH
  ```

- **Allow a service using an application profile:**
  ```bash
  sudo ufw allow OpenSSH
  ```

#### Logging

Enable logging to keep track of blocked and allowed connections. Logging is essential for monitoring and troubleshooting.

- **Enable logging:**
  ```bash
  sudo ufw logging on
  ```

- **Disable logging:**
  ```bash
  sudo ufw logging off
  ```

- **Set log level (low, medium, high, full):**
  ```bash
  sudo ufw logging medium
  ```

#### Deleting Rules

- **Delete a rule by rule number:**
  ```bash
  sudo ufw status numbered
  sudo ufw delete <rule-number>
  ```

- **Delete a rule allowing a specific port:**
  ```bash
  sudo ufw delete allow 22
  ```

- **Delete a rule denying a specific IP:**
  ```bash
  sudo ufw delete deny from 192.168.1.100
  ```

### UFW and IPv6

By default, UFW is configured to support IPv6 as well as IPv4.

- **Ensure UFW is configured for IPv6:**
  Open the UFW configuration file:
  ```bash
  sudo nano /etc/default/ufw
  ```

  Set the following value:
  ```text
  IPV6=yes
  ```

### Advanced Configuration files

For more advanced configurations, you can edit the UFW configuration files located in `/etc/ufw/`.

- **Default rules**: `/etc/ufw/ufw.conf`
- **Before rules**: `/etc/ufw/before.rules`
- **After rules**: `/etc/ufw/after.rules`
- **Application profiles**: `/etc/ufw/applications.d/`

### Example Configuration

Here’s a sample configuration to secure a web server:

1. **Set default policies:**
   ```bash
   sudo ufw default deny incoming
   sudo ufw default allow outgoing
   ```

2. **Allow SSH (on port 22):**
   ```bash
   sudo ufw allow 22
   ```

3. **Allow HTTP (on port 80) and HTTPS (on port 443):**
   ```bash
   sudo ufw allow http
   sudo ufw allow https
   ```

4. **Enable UFW:**
   ```bash
   sudo ufw enable
   ```

5. **Check the status:**
   ```bash
   sudo ufw status verbose
   ```

