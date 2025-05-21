# Matches in `iptables`

Matches are criteria used to identify which packets a rule applies to. They allow for granular filtering based on various attributes of packets, such as protocols, source/destination IPs, ports, and even advanced properties.

---

### **Types of Matches**

1. **Generic Matches**  
    These are commonly used options for basic filtering.
    
    - **`-p` (protocol)**: Specifies the protocol (e.g., TCP, UDP, ICMP).
        
        ```bash
        iptables -A INPUT -p tcp -j ACCEPT
        ```
        
    - **`-s` (source IP)**: Matches packets from a specific source IP or subnet.
        
        ```bash
        iptables -A INPUT -s 192.168.1.100 -j ACCEPT
        ```
        
    - **`-d` (destination IP)**: Matches packets destined for a specific IP or subnet.
        
        ```bash
        iptables -A INPUT -d 192.168.1.1 -j ACCEPT
        ```
        
    - **`-i` (input interface)**: Matches packets coming through a specific network interface.
        
        ```bash
        iptables -A INPUT -i eth0 -j ACCEPT
        ```
        
    - **`-o` (output interface)**: Matches packets leaving through a specific network interface.
        
        ```bash
        iptables -A OUTPUT -o eth1 -j ACCEPT
        ```
        
2. **Implicit Matches**  
    Matches based on specific protocol attributes (requires `-p` to be specified).
    
    - **`--sport` (source port)**: Matches packets from a specific source port (TCP/UDP).
        
        ```bash
        iptables -A INPUT -p tcp --sport 443 -j ACCEPT
        ```
        
    - **`--dport` (destination port)**: Matches packets to a specific destination port (TCP/UDP).
        
        ```bash
        iptables -A INPUT -p tcp --dport 22 -j ACCEPT
        ```
        
    - **`--tcp-flags`**: Matches TCP packets with specific flag combinations.
        
        ```bash
        iptables -A INPUT -p tcp --tcp-flags SYN,ACK SYN -j ACCEPT
        ```
        
3. **Explicit Matches**  
    Advanced matches requiring the `-m` (match extension) flag. These provide more detailed control.
    
    - **State Match**: Matches packets based on their connection state (`NEW`, `ESTABLISHED`, `RELATED`, etc.).
        
        ```bash
        iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
        ```
        
    - **Multiport Match**: Matches packets on multiple ports.
        
        ```bash
        iptables -A INPUT -p tcp -m multiport --dports 80,443,8080 -j ACCEPT
        ```
        
    - **IP Range Match**: Matches packets based on a range of IPs.
        
        ```bash
        iptables -A INPUT -m iprange --src-range 192.168.1.1-192.168.1.100 -j ACCEPT
        ```
        
    - **MAC Match**: Matches packets based on the source MAC address.
        
        ```bash
        iptables -A INPUT -m mac --mac-source 00:11:22:33:44:55 -j ACCEPT
        ```
        
    - **Time Match**: Matches packets based on time constraints (e.g., only allow traffic during office hours).
        
        ```bash
        iptables -A INPUT -m time --timestart 09:00 --timestop 17:00 -j ACCEPT
        ```
        
4. **Advanced Matches**  
    More complex matches often used in specialized cases.
    
    - **String Match**: Matches packets containing specific strings in their payloads.
        
        ```bash
        iptables -A INPUT -m string --string "example" --algo bm -j DROP
        ```
        
    - **Length Match**: Matches packets of a specific size.
        
        ```bash
        iptables -A INPUT -m length --length 64:128 -j ACCEPT
        ```
        

---

### **Example Use Cases**

1. **Allow only HTTP and HTTPS traffic from a specific subnet**:
    
    ```bash
    iptables -A INPUT -p tcp -s 192.168.1.0/24 -m multiport --dports 80,443 -j ACCEPT
    ```
    
2. **Allow traffic during working hours only**:
    
    ```bash
    iptables -A INPUT -m time --timestart 09:00 --timestop 17:00 --days Mon,Tue,Wed,Thu,Fri -j ACCEPT
    ```
    
3. **Block pings (ICMP echo requests)**:
    
    ```bash
    iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
    ```
    
4. **Allow traffic for established and related connections**:
    
    ```bash
    iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
    ```
    

---

### **Understanding Matches in Context**

Matches form the conditional part of an `iptables` rule. Combined with chains and targets, they provide a powerful mechanism for defining network policies.

- Matches **filter packets** based on criteria.
- Targets **define actions** once matches are satisfied.  
    For example:

```bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

This rule:

1. Matches: **TCP packets destined to port 22**.
2. Target: **Accepts** them.

