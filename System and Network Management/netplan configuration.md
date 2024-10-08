---
updated_at: 2024-09-26T04:48:51.567+06:00
edited_seconds: 90
---
# Configuring Network Using Netplan

Netplan is a network configuration tool introduced in Ubuntu 17.10 that simplifies the process of configuring network interfaces. It uses YAML files to describe network interfaces, and it integrates with systemd-networkd or NetworkManager to apply the configurations.

### 1. Netplan Configuration Files
   - Netplan configuration files are stored in `/etc/netplan/`.
   - These files have the `.yaml` extension.
   - Typically, the file is named something like `01-netcfg.yaml`, but the name can vary.

### 2. Basic Structure of a Netplan Configuration
   A Netplan configuration file follows a simple YAML structure:

   ```yaml
   network:
     version: 2  # Specifies the Netplan version, required field
     ethernets:
       eth0:
         dhcp4: yes  # Enable DHCP for IPv4
   ```

   - **`network:`**: The root of the configuration.
   - **`version:`**: Specifies the Netplan version being used. The current version is `2`.
   - **`ethernets:`**: Defines Ethernet interfaces.
   - **`eth0:`**: The name of the network interface. Replace `eth0` with the appropriate interface name on your system (e.g., `enp0s3`, `ens160`).

### 3. Common Configuration Options
   - **DHCP Configuration**: 
     - `dhcp4: yes` enables DHCP for IPv4, allowing the system to automatically receive an IP address.
     - `dhcp6: yes` enables DHCP for IPv6.

   - **Static IP Configuration**:
     To configure a static IP, you need to specify the `addresses`, `gateway4`, and `nameservers`:

     ```yaml
     network:
       version: 2
       ethernets:
         eth0:
           dhcp4: no  # Disable DHCP for IPv4
           addresses:
             - 192.168.1.100/24  # Static IP address with subnet mask
           gateway4: 192.168.1.1  # Default gateway for IPv4
           nameservers:
             addresses:
               - 8.8.8.8  # Primary DNS server
               - 8.8.4.4  # Secondary DNS server
     ```

   - **DNS Configuration**:
     You can configure DNS servers and search domains under the `nameservers` section:

     ```yaml
     nameservers:
       search: [example.com, localdomain]  # DNS search domains
       addresses:
         - 8.8.8.8  # Primary DNS server
         - 8.8.4.4  # Secondary DNS server
     ```

   - **Routes Configuration**:
     Static routes can be added using the `routes` section:

     ```yaml
     routes:
       - to: 192.168.2.0/24
         via: 192.168.1.1
         metric: 100
     ```

### 4. Applying Configuration
   After editing a Netplan configuration file, apply the changes using the following command:

   ```bash
   sudo netplan apply
   ```

   This command reads the configuration files, generates the necessary files for the backend (either systemd-networkd or NetworkManager), and applies the changes immediately.

### 5. Testing Configuration
   Before applying a configuration permanently, you can test it to ensure there are no syntax errors or issues:

   ```bash
   sudo netplan try
   ```

   This command will apply the configuration temporarily. If it fails, the system will revert to the previous settings after a timeout.

### 6. Advanced Configuration Options
   - **Bridges**:
     Used to create virtual network bridges, often used in virtualization.

     ```yaml
     bridges:
       br0:
         dhcp4: no
         interfaces:
           - eth0
         addresses:
           - 192.168.2.100/24
         gateway4: 192.168.2.1
     ```

   - **Bonds**:
     Network bonding combines multiple interfaces for redundancy or increased throughput.

     ```yaml
     bonds:
       bond0:
         dhcp4: no
         interfaces:
           - eth0
           - eth1
         parameters:
           mode: active-backup
     ```

   - **VLANs**:
     Virtual LANs (VLANs) separate network traffic on a physical interface.

     ```yaml
     vlans:
       vlan10:
         id: 10
         link: eth0
         addresses:
           - 192.168.10.100/24
     ```

### 7. Switching Between Backends
   Netplan supports both `systemd-networkd` and `NetworkManager` as backends. You can choose which one to use by specifying it in the YAML file:

   ```yaml
   network:
     version: 2
     renderer: networkd  # or NetworkManager
   ```

### 8. Troubleshooting
   If network issues arise after applying a Netplan configuration:
   - Verify the YAML file syntax.
   - Check the interface names.
   - Use `journalctl -u systemd-networkd` or `journalctl -u NetworkManager` to view logs related to network services.

Netplan simplifies network management on Ubuntu systems by providing a clear and consistent interface for configuring network settings. By leveraging YAML syntax, it enables both simple and complex configurations in a readable format, making network setup and troubleshooting more efficient.