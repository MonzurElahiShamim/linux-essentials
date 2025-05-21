# Targets in `iptables`

Targets specify the action to take when a packet matches a rule in a chain. The action could be to allow, block, or process the packet further. Targets determine the ultimate fate of packets that meet the match criteria in a rule.

---

### **Common Targets**

1. **`ACCEPT`**
    
    - Allows the packet to pass through.
    - Example: Allow SSH traffic.
        
        ```bash
        iptables -A INPUT -p tcp --dport 22 -j ACCEPT
        ```
        
2. **`DROP`**
    
    - Silently drops the packet (no notification sent to the sender).
    - Example: Block all incoming traffic from a specific IP.
        
        ```bash
        iptables -A INPUT -s 192.168.1.100 -j DROP
        ```
        
3. **`REJECT`**
    
    - Drops the packet but sends a notification (e.g., ICMP destination-unreachable) to the sender.
    - Example: Reject pings (ICMP echo requests).
        
        ```bash
        iptables -A INPUT -p icmp --icmp-type echo-request -j REJECT
        ```
        
4. **`RETURN`**
    
    - Stops processing in the current chain and returns to the calling chain.
    - Example: Return to the parent chain after processing a user-defined chain.
        
        ```bash
        iptables -N LOG_AND_DROP
        iptables -A LOG_AND_DROP -j LOG
        iptables -A LOG_AND_DROP -j DROP
        iptables -A INPUT -s 192.168.1.100 -j LOG_AND_DROP
        ```
        

---

### **Advanced Targets**

1. **`LOG`**
    
    - Logs packet details to `syslog` without affecting packet flow.
    - Example: Log dropped packets for auditing.
        
        ```bash
        iptables -A INPUT -p tcp --dport 22 -j LOG --log-prefix "SSH attempt: "
        ```
        
2. **`SNAT` (Source NAT)**
    
    - Modifies the source IP address of packets (used in the `nat` table).
    - Example: Change source IP to a public IP for outbound packets.
        
        ```bash
        iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 203.0.113.1
        ```
        
3. **`DNAT` (Destination NAT)**
    
    - Modifies the destination IP address of packets (used in the `nat` table).
    - Example: Forward HTTP traffic to an internal server.
        
        ```bash
        iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.10:80
        ```
        
4. **`MASQUERADE`**
    
    - A dynamic form of SNAT, often used in NAT for outbound traffic when the public IP is dynamic.
    - Example: Enable internet sharing.
        
        ```bash
        iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
        ```
        
5. **`REDIRECT`**
    
    - Redirects packets to a different port on the same host.
    - Example: Redirect incoming HTTP traffic to a local web server on port 8080.
        
        ```bash
        iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
        ```
        
6. **`MARK`**
    
    - Marks a packet with a value for further processing (used in advanced routing).
    - Example: Mark packets for a specific routing table.
        
        ```bash
        iptables -A PREROUTING -t mangle -p tcp --dport 80 -j MARK --set-mark 1
        ```
        

---

### **Example Scenarios**

1. **Allow web traffic while logging rejected packets**:
    
    ```bash
    iptables -A INPUT -p tcp --dport 80 -j ACCEPT
    iptables -A INPUT -j LOG --log-prefix "Rejected: "
    iptables -A INPUT -j DROP
    ```
    
2. **Set up a NAT rule for internal traffic**:
    
    ```bash
    iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
    ```
    
3. **Forward HTTP traffic to an internal server**:
    
    ```bash
    iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.10:80
    ```
    
