---
updated_at: 2024-07-13T18:13:52.431+06:00
edited_seconds: 620
---
# Networking in [[VirtualBox]]

VirtualBox provides several networking modes to facilitate connectivity between Virtual Machines (VMs), the host system, and external networks. Understanding these modes is crucial for setting up your virtual environment effectively.

---

#### **Objectives**

1. **Network Types**
2. **NAT (Network Address Translation)**
3. **NAT Network**
4. **Bridged Networking**
5. **Host-Only Networking**
6. **Internal Networking**
7. **Internet Connectivity**

---

### **1. Network Types**

VirtualBox supports different network types to cater to various connectivity needs:

- **NAT (Network Address Translation)**: Allows VMs to use the host's network connection while isolating the VM from the host network.
- **NAT Network**: Similar to NAT but allows multiple VMs to communicate with each other on the same network.
- **Bridged Networking**: Connects VMs to the host's physical network as if they were additional devices on the network.
- **Host-Only Networking**: Creates a private network between the host and the VMs, without any external network access.
- **Internal Networking**: Similar to Host-Only, but no access to the host; only VMs on the same internal network can communicate.
- **Generic Driver**: Used for more advanced configurations like using a different backend driver.
---

|Feature|NAT|NAT Network|Host Network|Host Network + NAT|Bridged|
|---|---|---|---|---|---|
|**VM can reach internet/other systems in the network**|Yes|Yes|No|Yes|Yes|
|**VMs can reach each other**|No|Yes|Yes|Yes|Yes|
|**Host can reach VM (Without Port forwarding)**|No|No|Yes|Yes|Yes|
|**Other systems in network can reach VM**|No|No|No|No|Yes|

---

### **2. NAT**
![[Pasted image 20240701113335.png]]
**Overview**:  
NAT (Network Address Translation) mode enables VMs to access external networks (such as the Internet) using the host machine's IP address. The VM appears to the external network as part of the host, which translates the VM's internal IP addresses to its own address.

**Advantages**:
- Easy to set up.
- Provides basic Internet access.
- Isolates the VM from the host network.

- ! VM's cannot talk to each other.

#### Setup:
1. **Enable NAT**:
   - Go to `Settings` > `Network` for your VM.
   - Set `Attached to` to `NAT`.
2. **Port Forwarding**:
   - Configure port forwarding to allow external access to services on the VM.
   - Example: Forward port `2222` on the host to port `22` on the VM     
 
**Use Case**:
- Suitable for VMs that need Internet access but don't need to interact with other devices on the host network.

---

### **3. NAT Network**

![[Pasted image 20240701115319.png]]

**Overview**:  
NAT Network is an extension of NAT that allows multiple VMs to communicate with each other on the same virtual network while still providing NAT-based Internet access.

**Advantages**:
- Allows VMs to communicate with each other.
- Provides Internet access to VMs.
- Combines the isolation benefits of NAT with the inter-VM communication capabilities.

**Setup**:
1. **Create a NAT Network**:
   - Open VirtualBox and go to `File` > `Preferences` > `Network`.
   - Click the `+` icon to create a new NAT Network.
   - Configure the network settings as needed (e.g., `10.0.2.0/24`).
2. **Attach VMs to the NAT Network**:
   - Go to `Settings` > `Network` for each VM.
   - Set `Attached to` to `NAT Network`.
   - Select the NAT Network created from the drop-down list.

**Use Case**:
- Ideal for scenarios where VMs need to communicate with each other and also require Internet access.

---

### **4. Bridged Networking**

![[Pasted image 20240701120855.png]]
**Overview**:  
Bridged Networking allows VMs to connect to the host's physical network directly. The VM acts as if it is another physical device on the network, with its own IP address assigned by the network's DHCP server.

**Advantages**:
- Direct access to the local network.
- VMs can be accessed by other devices on the network.
- Suitable for server applications and network simulations.

**Setup**:
1. **Enable Bridged Networking**:
   - Go to `Settings` > `Network` for your VM.
   - Set `Attached to` to `Bridged Adapter`.
   - Select the host's physical network interface.

**Use Case**:
- Ideal for scenarios where the VM needs to be part of the same network as the host, or when you want the VM to be reachable by other devices on the LAN.

---

### **5. Host-Only Networking**
![[Pasted image 20240630230133.png]]
**Overview**:  
Host-Only Networking creates a network that is private to the host and the VMs. This mode does not provide access to external networks but allows communication between the host and the VMs.

**Advantages**:
- Isolated environment for testing and development.
- Allows for communication between the host and VMs without external network exposure.

**Setup**:
1. **Enable Host-Only Networking**:
   - Go to `Settings` > `Network` for your VM.
   - Set `Attached to` to `Host-Only Adapter`.
   - Ensure the VirtualBox Host-Only Ethernet Adapter is selected.

**Use Case**:
- Useful for testing network applications in a controlled environment without exposing the VM to external networks.

---

### **6. Internal Networking**

**Overview**:  
Internal Networking creates a network that is private to the VMs and isolated from the host. This mode allows VMs on the same internal network to communicate with each other but not with the host or external networks.

**Advantages**:
- Provides a secure, isolated network environment for VMs.
- Useful for testing and development scenarios where no external network access is needed.

**Setup**:
1. **Enable Internal Networking**:
   - Go to `Settings` > `Network` for your VM.
   - Set `Attached to` to `Internal Network`.
   - Specify a network name (e.g., `intnet`).

**Use Case**:
- Ideal for scenarios where VMs need to communicate exclusively with each other without any access to the host or external networks.

---

### **7. Internet Connectivity**

**Overview**:  
Internet connectivity for VMs can be achieved using various network types:

- **NAT**: VMs use the host's Internet connection. Suitable for basic browsing and updates.
- **NAT Network**: Allows multiple VMs to communicate and use the Internet.
- **Bridged**: VMs appear as separate devices on the network and use the same external gateway as the host for Internet access.

**Considerations**:
- **NAT**: Provides basic outbound connectivity but might require port forwarding for inbound connections.
- **NAT Network**: Offers inter-VM communication and Internet access.
- **Bridged**: Provides more extensive access but requires VMs to have valid IP addresses on the local network.

---

### **Summary**

- **NAT**: Simplifies Internet access but isolates VMs from the local network.
- **NAT Network**: Allows VM-to-VM communication and Internet access.
- **Bridged**: Integrates VMs into the local network, making them accessible as if they were physical devices.
- **Host-Only**: Provides a private network for communication between the host and VMs, with no external access.
- **Internal Networking**: Creates a completely isolated network for VMs.

![[Pasted image 20240701121949.png]]
