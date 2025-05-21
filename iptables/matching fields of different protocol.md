# `iptables` matching fields of different protocol

`iptables` is a powerful Linux firewall tool that operates primarily on the network stack. It allows packet filtering based on various fields from **Layer 3 (Network Layer)** and **Layer 4 (Transport Layer)** protocol headers. Below is a detailed guide on the common matching options available for different protocols and headers.

---

### **Layer 3 (Network Layer) - IP Header Fields**

#### 1. **Source IP Address** (`-s` or `--source`)
- Matches packets based on the source IP address or subnet.
- Example:
  ```bash
  iptables -A INPUT -s 192.168.1.1 -j ACCEPT
  ```
  (Accepts packets originating from IP 192.168.1.1.)

#### 2. **Destination IP Address** (`-d` or `--destination`)
- Matches packets based on the destination IP address or subnet.
- Example:
  ```bash
  iptables -A OUTPUT -d 10.0.0.0/24 -j DROP
  ```
  (Drops packets destined for the 10.0.0.0/24 subnet.)

#### 3. **Protocol** (`-p` or `--protocol`)
- Matches packets based on the protocol field in the IP header (e.g., `tcp`, `udp`, `icmp`).
- Example:
  ```bash
  iptables -A INPUT -p tcp -j ACCEPT
  ```
  (Accepts packets using the TCP protocol.)

#### 4. **Interface** (`-i` and `-o`)
- **`-i`**: Matches packets entering a specific network interface.
- **`-o`**: Matches packets leaving a specific network interface.
- Example:
  ```bash
  iptables -A INPUT -i eth0 -j ACCEPT
  iptables -A OUTPUT -o eth1 -j DROP
  ```

#### 5. **Fragmentation** (`-f`)
- Matches second or later fragments of a fragmented packet.
- Example:
  ```bash
  iptables -A INPUT -f -j DROP
  ```
  (Drops all fragmented packets.)

---

### **Layer 4 (Transport Layer) - TCP, UDP, ICMP Fields**

#### **TCP (Transmission Control Protocol)**

1. **Source Port** (`--sport` or `--source-port`)
- Matches packets based on the TCP source port.
- Example:
  ```bash
  iptables -A INPUT -p tcp --sport 22 -j ACCEPT
  ```
  (Accepts packets originating from TCP port 22.)

2. **Destination Port** (`--dport` or `--destination-port`)
- Matches packets based on the TCP destination port.
- Example:
  ```bash
  iptables -A INPUT -p tcp --dport 80 -j ACCEPT
  ```
  (Accepts packets destined for TCP port 80.)

3. **TCP Flags** (`--tcp-flags`)
- Matches packets based on specific TCP flags (e.g., SYN, ACK, FIN, RST).
- Syntax: `--tcp-flags [flags to check] [flags to match]`
- Example:
  ```bash
  iptables -A INPUT -p tcp --tcp-flags SYN,ACK SYN -j ACCEPT
  ```
  (Accepts packets with the SYN flag set.)

4. **TCP MSS (Maximum Segment Size)** (`-m tcpmss` or `--mss`)
- Matches packets based on the TCP MSS field.
- Example:
  ```bash
  iptables -A FORWARD -p tcp -m tcpmss --mss 1400:1500 -j ACCEPT
  ```
  (Accepts TCP packets with MSS in the range 1400–1500.)

#### **UDP (User Datagram Protocol)**

1. **Source Port** (`--sport` or `--source-port`)
- Matches packets based on the UDP source port.
- Example:
  ```bash
  iptables -A INPUT -p udp --sport 53 -j ACCEPT
  ```
  (Accepts packets originating from UDP port 53.)

2. **Destination Port** (`--dport` or `--destination-port`)
- Matches packets based on the UDP destination port.
- Example:
  ```bash
  iptables -A INPUT -p udp --dport 123 -j ACCEPT
  ```
  (Accepts packets destined for UDP port 123.)

3. **Packet Length** (`-m length`)
- Matches packets based on the total length of the UDP header and payload.
- Example:
  ```bash
  iptables -A INPUT -p udp -m length --length 128:512 -j ACCEPT
  ```
  (Accepts UDP packets with length between 128 and 512 bytes.)

#### **ICMP (Internet Control Message Protocol)**

1. **ICMP Type** (`--icmp-type`)
- Matches packets based on the ICMP type (e.g., echo-request, echo-reply).
- Example:
  ```bash
  iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
  ```
  (Allows ICMP ping requests.)

2. **ICMP Code**
- Matches packets based on the ICMP code, providing more granular control.
- Example:
  ```bash
  iptables -A INPUT -p icmp --icmp-type destination-unreachable --icmp-code 1 -j DROP
  ```
  (Drops ICMP packets indicating host unreachable.)

---

### **General Matching Options**

1. **Connection State** (`-m state` or `-m conntrack`)
- Matches packets based on the connection state.
  - `NEW`: Packet is initiating a new connection.
  - `ESTABLISHED`: Packet belongs to an existing connection.
  - `RELATED`: Packet is related to an existing connection.
- Example:
  ```bash
  iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
  ```
  (Accepts packets that are part of established or related connections.)

2. **Rate Limiting** (`-m limit`)
- Limits the rate of matching packets.
- Example:
  ```bash
  iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/sec -j ACCEPT
  ```
  (Allows a maximum of 1 ICMP echo-request per second.)

3. **Interface** (`-i` and `-o`)
- Matches packets based on the input or output interface.
- Example:
  ```bash
  iptables -A INPUT -i eth0 -j ACCEPT
  ```
  (Accepts packets arriving on the `eth0` interface.)

4. **Logging** (`-j LOG`)
- Logs packet information to the system log.
- Example:
  ```bash
  iptables -A INPUT -j LOG --log-prefix "iptables-dropped: "
  ```
  (Logs dropped packets with a specific prefix.)

---

### **Conclusion**
By matching fields from the IP, TCP, UDP, and ICMP headers, iptables provides robust capabilities for packet filtering and firewall configuration. This enables fine-grained control over network traffic, enhancing security and performance.

