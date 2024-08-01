---
updated_at: 2024-07-28T18:38:57.840+06:00
edited_seconds: 1180
---
# How to Set Up a Firewall with UFW on Ubuntu

This tutorial will guide you through setting up a firewall with UFW on an Ubuntu system.

**11 min. read**

[View original](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu)

---
---

## Setting Up a Firewall with UFW on Ubuntu

**Introduction**

UFW (Uncomplicated Firewall) simplifies configuring firewalls using a user-friendly interface. This tutorial will guide you through setting up a firewall with UFW on Ubuntu v18.04 or later.

**Prerequisites**
- Ubuntu server with a non-root user with `sudo` privileges
- UFW installed by default or via `sudo apt install ufw`

## Steps

### 1. Ensure IPv6 is Enabled:
   - Check `/etc/default/ufw` to ensure `IPV6` is set to `yes`.

### 2. Set Up Default Policies:
   - Set incoming default policy to `deny`: `sudo ufw default deny incoming`
   - Set outgoing default policy to `allow`: `sudo ufw default allow outgoing`

### 3. Allow SSH Connections:
   - Allow via application profile: `sudo ufw allow OpenSSH`
   - Allow via service name: `sudo ufw allow ssh`
   - Allow via port number: `sudo ufw allow 22`

### 4. Enable UFW:
   - Enable the firewall: `sudo ufw enable`

### 5. Allow Other Connections:
   - Allow specific ports, services, or IP addresses. For example:
     - **HTTP (port 80)**: `sudo ufw allow http` or `sudo ufw allow 80`
     - **HTTPS (port 443)**: `sudo ufw allow https` or `sudo ufw allow 443`
     - **IP address**: `sudo ufw allow from 203.0.113.4`
     - **Network interface**: `sudo ufw allow in on eth0 to any port 80`

### 6. Deny Connections:
   - Deny specific connections, ports, or IP addresses. For example:
     - **Deny HTTP**: `sudo ufw deny http`
     - **Deny from IP address**: `sudo ufw deny from 203.0.113.4`

### 7. Delete Rules:
   - **Delete rule by number**: `sudo ufw delete [rule number]`
   - **Delete rule by name**: `sudo ufw delete [rule name]`

### 8. Check UFW Status and Rules:
   - **Get status**: `sudo ufw status`
   - **List rules**: `sudo ufw status numbered`

### 9. Disable or Reset Firewall:
   - Disable UFW: `sudo ufw disable`
   - Reset UFW (delete rules): `sudo ufw reset`

## Conclusion

Your firewall is now configured to allow essential connections while restricting unauthorized access. UFW offers additional features and configuration options, explore them as required. Remember to keep your firewall updated to maintain good security hygiene.
 