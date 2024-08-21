---
updated_at: 2024-08-20T09:47:12.093+06:00
edited_seconds: 110
---
# Network configuration using netplan
#### Sample YAML configuration file

```yaml
# This is the network config written by 'subiquity'
network:
  version: 2  # Netplan version, required field
  ethernets:
    eth0:
      dhcp4: no  # Disable DHCP for IPv4
      dhcp6: no  # Disable DHCP for IPv6
      addresses: 
        - 192.168.1.100/24  # Static IPv4 address with subnet mask (CIDR notation)
      gateway4: 192.168.1.1  # Default gateway for IPv4
      nameservers:
        search: [example.com, localdomain]  # DNS search domains
        addresses:
          - 8.8.8.8  # Primary DNS server (Google)
          - 8.8.4.4  # Secondary DNS server (Google)
      routes:
        - to: 192.168.2.0/24  # Static route to another subnet
          via: 192.168.1.1  # Gateway for the static route
          metric: 100  # Priority of the route (lower is higher priority)
        - to: 0.0.0.0/0  # Default route (any destination)
          via: 192.168.1.1  # Gateway for the default route
          on-link: true  # Indicate that the gateway is on the link (directly reachable)
      mtu: 1500  # Maximum Transmission Unit size (standard Ethernet MTU)
      optional: true  # Mark the interface as optional (system boot does not wait for it)
      wakeonlan: true  # Enable Wake-on-LAN
      match:
        macaddress: "00:1e:67:dd:08:34"  # Match interface by MAC address
        driver: e1000e  # Match interface by driver
      set-name: eth0  # Rename the interface to eth0

  bridges:
    br0:
      dhcp4: no  # Disable DHCP for IPv4 on the bridge
      addresses:
        - 192.168.2.100/24  # Static IP address for the bridge
      gateway4: 192.168.2.1  # Default gateway for the bridge
      interfaces:
        - eth0  # Interfaces to be included in the bridge
      parameters:
        stp: true  # Enable Spanning Tree Protocol
        forward-delay: 4  # Delay time for STP in seconds
      nameservers:
        addresses:
          - 8.8.8.8  # Primary DNS server for the bridge
          - 1.1.1.1  # Secondary DNS server (Cloudflare)
      routes:
        - to: 192.168.3.0/24  # Static route through the bridge
          via: 192.168.2.1  # Gateway for the route
          metric: 200  # Priority of the route

  bonds:
    bond0:
      dhcp4: no  # Disable DHCP for IPv4 on the bond
      addresses:
        - 192.168.3.100/24  # Static IP address for the bond
      gateway4: 192.168.3.1  # Default gateway for the bond
      interfaces:
        - eth1  # First interface in the bond
        - eth2  # Second interface in the bond
      parameters:
        mode: active-backup  # Bonding mode: active-backup for redundancy
        primary: eth1  # Primary interface to use in active-backup mode
        mii-monitor-interval: 100  # Link monitoring interval in milliseconds
      nameservers:
        addresses:
          - 8.8.8.8  # Primary DNS server for the bond
          - 1.1.1.1  # Secondary DNS server

  vlans:
    vlan10:
      id: 10  # VLAN ID
      link: eth0  # Physical interface that this VLAN is tied to
      dhcp4: no  # Disable DHCP for IPv4 on the VLAN
      addresses:
        - 192.168.10.100/24  # Static IP address for the VLAN
      gateway4: 192.168.10.1  # Default gateway for the VLAN
      nameservers:
        addresses:
          - 8.8.8.8  # Primary DNS server for the VLAN
          - 1.1.1.1  # Secondary DNS server

  wifis:
    wlan0:
      access-points:
        "MyNetwork":
          password: "password123"  # WiFi network password
      dhcp4: yes  # Enable DHCP for IPv4 on the WiFi interface
      dhcp6: yes  # Enable DHCP for IPv6 on the WiFi interface
      optional: true  # Mark the WiFi interface as optional
      nameservers:
        addresses:
          - 8.8.8.8  # Primary DNS server for WiFi
          - 1.1.1.1  # Secondary DNS server
      routes:
        - to: 192.168.20.0/24  # Static route through the WiFi interface
          via: 192.168.1.1  # Gateway for the route
          metric: 300  # Priority of the route

```

### Breakdown of the Template:

1. **Ethernet Interface (`ethernets`):**
    
    - `dhcp4`/`dhcp6`: Enable or disable DHCP for IPv4/IPv6.
    - `addresses`: Static IP addresses with CIDR notation.
    - `gateway4`: Default gateway for IPv4.
    - `nameservers`: DNS servers and search domains.
    - `routes`: Custom routing table entries.
    - `mtu`: Maximum Transmission Unit size.
    - `optional`: Make the interface optional.
    - `wakeonlan`: Enable Wake-on-LAN.
    - `match` and `set-name`: Used for matching interfaces by MAC address, driver, etc., and renaming them.
2. **Bridge (`bridges`):**
    
    - `interfaces`: List of interfaces to include in the bridge.
    - `parameters`: Bridge-specific parameters like STP (Spanning Tree Protocol).
3. **Bond (`bonds`):**
    
    - `interfaces`: List of interfaces to include in the bond.
    - `parameters`: Bonding mode and options like monitoring interval, primary interface, etc.
4. **VLAN (`vlans`):**
    
    - `id`: VLAN ID.
    - `link`: The physical interface that this VLAN is tied to.
5. **WiFi (`wifis`):**
    
    - `access-points`: List of WiFi networks and their credentials.
    - `dhcp4`/`dhcp6`: Enable or disable DHCP for IPv4/IPv6.
    - `optional`: Make the interface optional.

