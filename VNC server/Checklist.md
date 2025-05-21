# Checklist for Setting Up `VNC Server` on *Oracle Linux 7* and Connecting via *SSH Tunnel*

#### Pre-requisites
- [ ] Oracle Linux 7 installed.
- [ ] Root or sudo access to the remote server.
- [ ] SSH access to the remote server.
- [ ] VNC client installed on the local machine.


### Step 2: Install VNC Server

- [ ] Install TigerVNC server:
  ```bash
  sudo yum install -y tigervnc-server
  ```


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


### Step 6: Secure VNC Connection with SSH Tunnel

- [ ] Create an SSH tunnel on your local machine:
  ```bash
  ssh -L 5901:localhost:5901 vncuser@your-remote-server-ip
  ```


### **Security Considerations**
- [ ] Ensure the VNC port is **NOT** publicly accessible (only access via SSH tunnel).
- [ ] Use SSH keys for authentication if possible.
- [ ] Regularly update system and software packages.

