---
updated_at: 2024-06-30T22:41:51.568+06:00
edited_seconds: 160
---

If your Virtual Machine (VM) in VirtualBox is configured with a NAT (Network Address Translation) network interface, it means the VM is using the host computer's network connection to access external networks. However, to connect to the VM directly from your host or another machine on the same network, you typically need to set up port forwarding or use additional networking configurations. Here’s how you can do it:

### Setting Up Port Forwarding in VirtualBox

1. **Open VirtualBox and Select Your VM**:
   - Go to VirtualBox and select your VM from the list.

2. **Access VM Settings**:
   - Click on `Settings` for your VM.

3. **Configure Network Settings**:
   - Go to the `Network` tab.
   - Ensure the `Attached to` option is set to `NAT`.

4. **Port Forwarding**:
   - Click on `Port Forwarding`.
   - Add a new rule by clicking the `+` icon.
     - **Name**: Any descriptive name (e.g., SSH).
     - **Protocol**: TCP or UDP, depending on your needs.
     - **Host IP**: Leave blank or specify if needed (usually not required).
     - **Host Port**: The port on your host machine that you will use to connect to the VM (e.g., 2222).
     - **Guest IP**: Leave blank or specify if needed (usually not required).
     - **Guest Port**: The port on the VM that you want to forward (e.g., 22 for SSH).

5. **Save Settings**:
   - Click `OK` to save the settings.

### Connecting to the VM Using SSH (Example)

Assuming you forwarded port 2222 on your host to port 22 on your VM:

1. **Find Host IP**:
   - Determine the IP address of your host machine.
   - & Can use `127.0.0.1` or `localhost` if connecting from same machine.

2. **SSH Connection**:
   - Use SSH to connect to your VM through the forwarded port:
     ```bash
     ssh -p 2222 username@host_ip_address
     ```
     - Replace `2222` with the host port you configured.
     - Replace `username` with your username on the VM.
     - Replace `host_ip_address` with the IP address of your host machine.

   Example:
   ```bash
   ssh -p 2222 john@192.168.1.100
   ```

### Notes:

- **Dynamic IP Assignment**: If your VM gets its IP address dynamically (via DHCP) from VirtualBox’s internal NAT network, you might need to check the IP assigned to the VM (`ifconfig` or `ip addr show` within the VM) to connect.
  
- **Security**: Ensure firewall settings on your host and VM allow connections on the specified ports.

By setting up port forwarding in VirtualBox and connecting through SSH (or other protocols as needed), you can access and manage your VM even when it's configured with a NAT network interface. Adjust port numbers and settings based on your specific VM and networking requirements.