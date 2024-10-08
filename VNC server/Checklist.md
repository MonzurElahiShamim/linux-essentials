---
updated_at: 2024-10-08T22:08:04.656+06:00
edited_seconds: 310
---
# Checklist for Setting Up `VNC Server` on *Oracle Linux 7* and Connecting via *SSH Tunnel*

#### Pre-requisites
- [ ] Oracle Linux 7 installed.
- [ ] Root or sudo access to the remote server.
- [ ] SSH access to the remote server.
- [ ] VNC client installed on the local machine.

---

### Step 1: Install GUI ("Server with GUI")

- [ ] Update the system:
  ```bash
  sudo yum update -y
  ```
- [ ] Install "Server with GUI":
  ```bash
  sudo yum groupinstall -y "Server with GUI"
  ```
- [ ] Set the default target to graphical:
  ```bash
  sudo systemctl set-default graphical.target
  ```
- [ ] Reboot the system:
  ```bash
  sudo reboot
  ```

---

### Step 2: Install VNC Server

- [ ] Install TigerVNC server:
  ```bash
  sudo yum install -y tigervnc-server
  ```

---

### Step 3: Configure VNC Server

- [ ] Create a user for VNC (`vncuser`):
  ```bash
  sudo adduser vncuser
  sudo passwd vncuser
  ```
- [ ] Set the VNC password for `vncuser`:
  ```bash
  su - vncuser
  vncpasswd
  exit
  ```
- [ ] Copy the VNC service file:
  ```bash
  sudo cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver_vncuser@:1.service
  ```
- [ ] Edit the VNC service file (`/etc/systemd/system/vncserver_user@:1.service`):
  - [ ] Replace `<USER>` with `vncuser` in the `ExecStart` and `ExecStop` lines.
- [ ] Reload the systemd daemon:
  ```bash
  sudo systemctl daemon-reload
  ```

---

### Step 4: Start and Enable the VNC Server

- [ ] Start the VNC server on display `:1`:
  ```bash
  sudo systemctl start vncserver_vncuser@:1.service
  ```
- [ ] Enable the VNC server to start at boot:
  ```bash
  sudo systemctl enable vncserver_vncuser@:1.service
  ```
- [ ] Check the status of the VNC server:
  ```bash
  sudo systemctl status vncserver_vncuser@:1.service
  ```

---

### Step 5: Configure the Firewall

- [ ] Ensure SSH is allowed through the firewall:
  ```bash
  sudo firewall-cmd --permanent --add-service=ssh
  sudo firewall-cmd --reload
  ```

> [!info]- If not using SSH Tunnel
> ```bash
> firewall-cmd --list-all
> firewall-cmd --add-service=vnc-server --permanent
> firewall-cmd --list-all
> ```


---

### Step 6: Secure VNC Connection with SSH Tunnel

- [ ] Create an SSH tunnel on your local machine:
  ```bash
  ssh -L 5901:localhost:5901 vncuser@your-remote-server-ip
  ```

---

### **Step 7: Connect Using VNC Client**

- [ ] Open the VNC client on your local machine.
- [ ] Connect to `localhost:5901` (or a different local port if configured).
- [ ] Enter the VNC password set for `vncuser`.
- [ ] Verify successful connection to the remote desktop.


---

### **Security Considerations**
- [ ] Ensure the VNC port is **NOT** publicly accessible (only access via SSH tunnel).
- [ ] Use SSH keys for authentication if possible.
- [ ] Regularly update system and software packages.

---




### 1.3. Set the Default Target to Graphical

To ensure the system boots into the graphical interface:

```bash
sudo systemctl set-default graphical.target
```

### 1.4. Reboot the System

Reboot to start the graphical environment:

```bash
sudo reboot
```
