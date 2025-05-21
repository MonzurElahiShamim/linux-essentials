# Setting Up VNC Server with GUI on `Oracle Linux 7` 

This guide will walk you through :
- Installing a graphical desktop environment on Oracle Linux 7, 
- Setting up a VNC server, 
- Securing the connection using an SSH tunnel, and 
- Connecting from a local machine using a VNC client.


## Step 1: Install the Graphical Desktop Environment ("Server with GUI")

By default, Oracle Linux 7 may not have a GUI installed. We'll install the "Server with GUI" package group.

### 1.1. Update the System

First, update the system packages:

```bash
sudo yum update -y
```

### 1.2. Install "Server with GUI"

List all available package groups
```bash
sudo yum group list
```

Install the graphical desktop environment:
```bash
sudo yum groupinstall -y "Server with GUI"
```



## Step 3: Configure VNC Server

### 3.1. Create a VNC User (`optional`)

Create a user that will run the VNC server (*or use an existing user*). For this guide, we'll create a user named `oracle`.

```bash
sudo adduser oracle
sudo passwd oracle
```

### 3.2. Set VNC Password for the User

Switch to the `oracle` account and set the VNC password:

```bash
su - oracle
vncpasswd
```

You'll be prompted to enter and confirm a password for VNC access.

### 3.3. Configure VNC Server for the User

Exit back to the `root` or `sudo` user:

```bash
exit
```

Create a copy of the default configuration file for the VNC service:

```bash
sudo cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver_oracle@:1.service
```

### 3.4. Edit the VNC Service File

Edit the service file to specify the user and display number:

```bash
sudo nano /etc/systemd/system/vncserver_oracle@:1.service
```

Find the lines:

```ini
[Service]
Type=forking
# Clean any existing files in /tmp/.X11-unix environment
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/sbin/runuser -l <USER> -c "/usr/bin/vncserver %i"
PIDFile=/home/<USER>/.vnc/%H%i.pid
ExecStop=/sbin/runuser -l <USER> -c "/usr/bin/vncserver -kill %i"
```

Replace `<USER>` with `oracle`. The file should now look like:

```ini
[Service]
Type=forking
# Clean any existing files in /tmp/.X11-unix environment
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/sbin/runuser -l oracle -c "/usr/bin/vncserver %i"
PIDFile=/home/oracle/.vnc/%H%i.pid
ExecStop=/sbin/runuser -l vncuser -c "/usr/bin/vncserver -kill %i"
```

### 3.5. Reload Systemd Daemon

Reload the systemd manager configuration:

```bash
sudo systemctl daemon-reload
```


## Step 5: Configure the Firewall

By default, the firewall may block the VNC port. Since we'll be using an SSH tunnel, we don't need to open the VNC port to the outside world. Ensure that the SSH service is allowed through the firewall.

### 5.1. Allow SSH Through the Firewall

```bash
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload
```


> [!info]- #### OR If not using SSH Tunnel
> ```bash
> firewall-cmd --list-all
> firewall-cmd --add-service=vnc-server --permanent
> firewall-cmd --list-all
> ```


## Step 7: Connect to the VNC Server Using a VNC Client

Now, you can use your VNC client to connect to the remote desktop.

### 7.1. Install a VNC Client on Your Local Machine

If you don't have one installed, install a VNC client suitable for your operating system.

- **Windows**: Use clients like **TigerVNC Viewer**, **RealVNC Viewer**, or **TightVNC Viewer**.
- **macOS**: Use **RealVNC Viewer** or **TigerVNC Viewer**.
- **Linux**: Install **TigerVNC Viewer** or **Remmina**.

### 7.2. Connect to the VNC Server

Open your VNC client and connect to:

```
localhost:5901
```

Or, if you used a different local port:

```
localhost:5902
```

Or, if you don't use SSH Tunnel
```
remote_machine_ip:5901
```

**Note**: Some VNC clients require the display number instead of the port number. Since display `:1` corresponds to port `5901`, you can also use `localhost:1` in the VNC client.

### 7.3. Enter VNC Password

When prompted, enter the VNC password you set earlier for `oracle`.

### 7.4. Access the Remote Desktop

You should now see the remote desktop environment of your Oracle Linux 7 machine and can interact with it as if you were sitting in front of it.


## **Summary of Commands**

1. **Update system and install GUI**:

   ```bash
   sudo yum update -y
   sudo yum groupinstall -y "Server with GUI"
   sudo systemctl set-default graphical.target
   sudo reboot
   ```

2. **Install VNC server**:

   ```bash
   sudo yum install -y tigervnc-server
   ```

3. **Create VNC user and set VNC password**:

   ```bash
   sudo adduser vncuser
   sudo passwd vncuser
   su - vncuser
   vncpasswd
   exit
   ```

4. **Configure VNC service**:

   ```bash
   sudo cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service
   
   sudo nano /etc/systemd/system/vncserver@:1.service
   # Edit file to replace <USER> with vncuser
   
   sudo systemctl daemon-reload
   ```


5. **Start and enable VNC server**:

   ```bash
   sudo systemctl start vncserver@:1.service
   sudo systemctl enable vncserver@:1.service
   sudo systemctl status vncserver@:1.service
   ```

6. **Configure firewall to allow SSH**:

   ```bash
   sudo firewall-cmd --permanent --add-service=ssh
   sudo firewall-cmd --reload
   ```

7. **Create SSH tunnel from local machine**:

   ```bash
   ssh -L 5901:localhost:5901 vncuser@your-remote-server-ip
   ```

8. **Connect via VNC client**:

   - **VNC Server Address**: `localhost:5901` or `localhost:1`
   - **VNC Password**: Enter the password set with `vncpasswd`

