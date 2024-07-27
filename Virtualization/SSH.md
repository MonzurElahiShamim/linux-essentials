---
updated_at: 2024-06-30T20:53:19.125+06:00
edited_seconds: 230
---
# Setup SSH connection

> [!note]- Connect using Password
> If you don't have SSH keys set up or prefer not to use them, you can still connect to a remote server using SSH with password authentication. Here’s how to do it:
> 
> ### Connecting to a Remote Server Using SSH with Password Authentication
> 
> 1. **Ensure SSH Client is Installed**:
>    - If not already installed, install the SSH client on your local machine (LocalMachine):
>      ```bash
>      sudo apt update
>      sudo apt install openssh-client
>      ```
> 
> 2. **Connect to the Remote Server**:
>    - Use the `ssh` command to connect to the remote server. Replace `username` with your username on the remote server and `remote_server_hostname` with the server's hostname or IP address:
>      ```bash
>      ssh username@remote_server_hostname
>      ```
>      Example:
>      ```bash
>      ssh john@example.com
>      ```
>      You will be prompted to enter your password for the remote server’s username. After entering the correct password, you will gain access to the remote server.
> 
> 3. **Authenticate**:
>    - Once you enter the password correctly, you will be logged into the remote server's command line interface.
> 
> ### Notes:
> - **Password Security**: Using password authentication is less secure than SSH key-based authentication, especially over the internet. Ensure you use a strong password and consider implementing additional security measures like IP whitelisting or two-factor authentication (if supported).
> 
> - **Using SSH Keys for Enhanced Security**: It's generally recommended to use SSH keys for authentication as they provide stronger security and convenience (once set up).
> 
## Step-by-Step Guide to Setting Up SSH

#### On Your Local Machine (Client):

1. **Install SSH Client**:
   - If not already installed, install the SSH client:
     ```bash
     sudo apt update
     sudo apt install openssh-client
     ```

2. **Generate SSH Key Pair (Optional but Recommended)**:
   - Generate SSH keys on your local machine:
     ```bash
     ssh-keygen -t rsa -b 4096
     ```
     Follow the prompts to save the keys (e.g., `id_rsa` for private key and `id_rsa.pub` for public key) in the default location (`~/.ssh/`).

3. **Copy Public Key to Remote Server**:
   - Use `ssh-copy-id` to copy your public key to the remote server:
     ```bash
     ssh-copy-id username@hostname
     ```
    Replace `username` with your username on the remote machine and `hostname` with the server's hostname or IP address. You'll be prompted to enter your password (if password authentication is enabled).

> Make sure to configure ssh server (**step 4, 5, 6**) before copying *Public Key*

#### On the Remote Server:

4. **Install SSH Server**:
   - Install the SSH server on the remote machine:
     ```bash
     sudo apt update
     sudo apt install openssh-server
     ```

5. **Configure SSH Server**:
   - Edit the SSH server configuration file to adjust settings:
     ```bash
     sudo nano /etc/ssh/sshd_config
     ```
     Adjust settings such as port number (`Port`), authentication methods (`PasswordAuthentication`, `PubkeyAuthentication`), and other security settings. Example settings:
     ```text
     Port 22
     PermitRootLogin no
     PasswordAuthentication yes
     ```

6. **Restart SSH Service**:
   - Apply the changes and restart the SSH service:
     ```bash
     sudo systemctl restart ssh
     ```

### Connecting to the Remote Server:

7. **Connect via SSH**:
   - Now, you can connect to the remote server from your local machine:
     ```bash
     ssh username@hostname
     ```
     Replace `username` with your username on the remote machine and `hostname` with the server's hostname or IP address. Enter your password if prompted (or none if using key-based authentication).

### Optional Steps for Enhanced Security:

- **Firewall Configuration**: Restrict SSH access to specific IP addresses using firewall rules (`iptables`, `ufw`).
- **Disable Root Login**: Set `PermitRootLogin no` in `sshd_config` to prevent root login over SSH.
- **SSH Protocol Version**: Ensure `Protocol 2` is set in `sshd_config` for enhanced security.

By following these clarified steps, you can securely set up SSH for remote access and management between your local machine (client) and the remote server. Adjust configurations based on your specific security requirements and operating system conventions.

