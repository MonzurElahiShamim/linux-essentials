# Roadmap to Learn iptables


#### **1. Understand the Basics**

1. **What is iptables?**
    
    - Definition: `iptables` is a Linux utility for configuring the kernel's packet filtering ruleset.
    - Use cases: Firewall, NAT, packet filtering, and traffic shaping.
2. **Core Concepts:**
    
    - **[Chains](Chains.md)**: INPUT, OUTPUT, FORWARD, PREROUTING, POSTROUTING.
    - **[Tables](Tables.md)**: FILTER, NAT, MANGLE, RAW, SECURITY.
    - **[Rules](Rules.md)**: Conditions and actions applied to packets.
    - **[Policies](Policies.md)**: Default actions for chains (ACCEPT, DROP).
3. **Setup:**
    
    - Ensure `iptables` is installed: `sudo apt install iptables` (Debian/Ubuntu) or `sudo yum install iptables` (RHEL/CentOS).
    - Check the current rules: `sudo iptables -L`.

---

#### **2. Basic Usage**

1. **View Rules:**
    
    - List rules: `sudo iptables -L`.
    - Show line numbers: `sudo iptables -L --line-numbers`.
    - Verbose output: `sudo iptables -L -v`.
2. **Add/Remove Rules:**
    
    - Append a rule: `sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT`.
    - Insert a rule: `sudo iptables -I INPUT 1 -p tcp --dport 22 -j ACCEPT`.
    - Delete a rule: `sudo iptables -D INPUT 1`.
3. **Set Policies:**
    
    - Default drop policy: `sudo iptables -P INPUT DROP`.
4. **Flush Rules:**
    
    - Clear all rules: `sudo iptables -F`.

---

#### **3. Practical Use Cases**

1. **Common Firewall Rules:**
    
    - Allow SSH: `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`.
    - Allow HTTP/HTTPS: `sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT` and `443`.
    - Block all traffic by default: `sudo iptables -P INPUT DROP`.
2. **ICMP (Ping):**
    
    - Allow ping: `sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT`.
    - Block ping: `sudo iptables -A INPUT -p icmp --icmp-type echo-request -j DROP`.
3. **Rate Limiting:**
    
    - Limit SSH attempts: `sudo iptables -A INPUT -p tcp --dport 22 -m limit --limit 3/min -j ACCEPT`.
4. **NAT Rules:**
    
    - Enable NAT: `sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE`.

---

#### **4. Advanced Features**

1. **Stateful Packet Inspection:**
    
    - Allow established connections: `sudo iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT`.
2. **Logging:**
    
    - Log dropped packets: `sudo iptables -A INPUT -j LOG --log-prefix "Dropped: "`.
3. **Custom Chains:**
    
    - Create a custom chain: `sudo iptables -N MYCHAIN`.
    - Redirect packets: `sudo iptables -A INPUT -p tcp --dport 8080 -j MYCHAIN`.
4. **Save and Restore Rules:**
    
    - Save: `sudo iptables-save > /etc/iptables/rules.v4`.
    - Restore: `sudo iptables-restore < /etc/iptables/rules.v4`.

---
