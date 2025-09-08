# Configuring WiFi with Netplan

Configuring WiFi using Netplan involves defining the wireless network interface and providing details such as the network SSID (name) and password. Netplan supports WiFi configuration through the `wifis` section in its YAML configuration files.

Here's a detailed guide on how to configure WiFi using Netplan:

### 1. Basic WiFi Configuration

To set up a basic WiFi connection, you need to specify the network interface, the access points (SSID), and the connection details:

```yaml
network:
  version: 2
  wifis:
    wlan0:
      dhcp4: yes  # Enable DHCP for IPv4 (automatic IP assignment)
      dhcp6: yes  # Enable DHCP for IPv6 (optional)
      access-points:
        "MyNetwork":
          password: "password123"  # WiFi network password
```

- **`wifis:`**: Defines the WiFi interfaces.
- **`wlan0:`**: Specifies the WiFi interface name. Replace `wlan0` with the actual name of your WiFi interface (e.g., `wlp2s0`).
- **`dhcp4: yes`**: Enables DHCP for IPv4, allowing the system to automatically obtain an IP address.
- **`dhcp6: yes`**: (Optional) Enables DHCP for IPv6 if required.
- **`access-points:`**: Defines the WiFi networks the interface will connect to.
- **`"MyNetwork":`**: The SSID (name) of the WiFi network you want to connect to.
- **`password:`**: The password for the WiFi network.

### 2. Static IP Configuration for WiFi

If you need to set a static IP address for the WiFi interface, modify the configuration as follows:

```yaml
network:
  version: 2
  wifis:
    wlan0:
      dhcp4: no  # Disable DHCP for IPv4
      addresses:
        - 192.168.1.100/24  # Static IP address with subnet mask
      gateway4: 192.168.1.1  # Default gateway for IPv4
      nameservers:
        addresses:
          - 8.8.8.8  # Primary DNS server
          - 8.8.4.4  # Secondary DNS server
      access-points:
        "MyNetwork":
          password: "password123"  # WiFi network password
```

- **`dhcp4: no`**: Disables DHCP for IPv4, requiring you to specify a static IP address.
- **`addresses:`**: Lists the static IP addresses assigned to the interface.
- **`gateway4:`**: Specifies the default gateway for IPv4.
- **`nameservers:`**: Defines DNS servers for name resolution.

### 3. Multiple Access Points

To configure multiple access points, you can list them under `access-points`. The interface will try to connect to the first available network:

```yaml
network:
  version: 2
  wifis:
    wlan0:
      dhcp4: yes
      access-points:
        "HomeNetwork":
          password: "homepassword"
        "OfficeNetwork":
          password: "officepassword"
```

The interface will attempt to connect to "HomeNetwork" first. If it's not available, it will try "OfficeNetwork".

### 4. Advanced Options

- **`optional: true`**: Marks the WiFi interface as optional, meaning the system won't wait for it to be up during boot.

  ```yaml
  network:
    version: 2
    wifis:
      wlan0:
        dhcp4: yes
        optional: true
        access-points:
          "MyNetwork":
            password: "password123"
  ```

- **`band:`**: Specifies the WiFi band (e.g., `a`, `b`, `g`, `n`, `ac`).

  ```yaml
  network:
    version: 2
    wifis:
      wlan0:
        dhcp4: yes
        access-points:
          "MyNetwork":
            password: "password123"
        band: "a"  # Use 5 GHz band
  ```

### 5. Applying the Configuration

After modifying the Netplan configuration file, apply the changes with:

```bash
sudo netplan apply
```

### 6. Testing the Configuration

To test the configuration without applying it permanently, use:

```bash
sudo netplan try
```

This command temporarily applies the configuration and reverts if it fails, allowing you to verify the settings before making permanent changes.

### Troubleshooting WiFi Configuration

- **Verify Interface Name**: Ensure that the interface name (`wlan0`, `wlp2s0`, etc.) matches your actual WiFi interface.
- **Check Logs**: Use `journalctl -u systemd-networkd` or `journalctl -u NetworkManager` to view logs for troubleshooting connection issues.
- **Review Configuration Syntax**: Ensure that YAML syntax is correct and properly indented.

By following these guidelines, you can effectively configure WiFi connections using Netplan, whether for simple DHCP setups or more complex static IP configurations.

