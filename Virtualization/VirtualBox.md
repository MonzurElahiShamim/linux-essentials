---
updated_at: 2024-06-30T21:29:07.636+06:00
edited_seconds: 810
---
# VirtualBox

## Start a Virtual Machine (VM)

A Virtual Machine can be started in three modes:
- **Normal start**: Launches the VM with a graphical interface.
- **Headless start**: Launches the VM without a graphical interface.
- **Detachable start**: Starts the VM in the background, allowing it to be detached from the current terminal.

> [!example]- Detailed Explanation
> ## Start a Virtual Machine (VM)
> 
> VirtualBox allows you to start a Virtual Machine (VM) in various modes, each serving different purposes depending on your needs and preferences:
> 
> ### 1. Normal Start
> 
> - **Description**: This mode launches the VM with a full graphical interface, similar to how you would expect an operating system to start on a physical machine.
> - **Use Case**: Ideal for situations where you need to interact directly with the VM using its graphical interface. It provides a desktop-like environment within VirtualBox.
> 
> ### 2. Headless Start
> 
> - **Description**: Headless mode starts the VM without any graphical interface. The VM runs in the background as a process, and you access it through remote desktop protocols (RDP) or command-line interfaces (CLI) such as SSH.
> - **Use Case**: Useful for server-like environments where graphical output is unnecessary or resource-intensive. Headless VMs are managed remotely, making them efficient for server applications and automated tasks.
> 
> ### 3. Detachable Start
> 
> - **Description**: Detachable mode is a hybrid between normal and headless modes. It starts the VM with a graphical interface, but you can detach it from the current VirtualBox window, allowing it to continue running in the background.
> - **Use Case**: Convenient when you need to switch between managing the VM through a graphical interface and accessing it remotely. You can detach the VM window and continue managing it via SSH or other remote access methods without interrupting its operation.
> 
> ### Choosing the Right Start Mode
> 
> - **Normal Start**: Best for desktop environments or testing graphical applications.
> - **Headless Start**: Suitable for server setups, automation, or situations where remote management is preferred.
> - **Detachable Start**: Offers flexibility for managing VMs in both graphical and remote environments, making it a versatile choice.
> 

## Remote Connection Using SSH

### Configure IP Address on Remote Server

1. **Check Current IP Address**:
   Use one of the following commands to view current network interface details:
   ```bash
   ifconfig
   ip addr show
   ip a
   ```

2. **Change or Set IP Address**:
   To set a new IP address (`192.168.1.100` in this example) for `eth0` interface:
   ```bash
   sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0
   ```
   Activate the changes:
   ```bash
   sudo ifconfig eth0 up
   ```

### Check and Start SSH Server

1. **Check SSH Server Status**:
   Verify if SSH server (`sshd`) is running:
   ```bash
   systemctl status sshd
   ```

2. **Start SSH Server** (if not running):
   ```bash
   systemctl start sshd
   ```

### Connecting to Remote Server

#### Using PuTTY (Windows)

- Open PuTTY and enter:
  - **IP address of remote server**
  - **Username**
  - **Password**

#### Using Shell (Linux or macOS)

- Open a terminal and use SSH command:
  ```bash
  ssh username@ip_address
  ```
  Replace `username` with your username on the remote server and `ip_address` with the server's IP address.
  
  Example:
  ```bash
  ssh john@192.168.1.100
  ```
  Enter your password when prompted.

---

**Related Topics:**
- [[SSH|More on SSH]]
- [[Services|More on Services]]
