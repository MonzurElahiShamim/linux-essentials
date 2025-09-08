# Updating Hostname and `/etc/hosts` File

### Command to Set a New Hostname

To set a new hostname on your system, use the following command:

```bash
sudo hostnamectl set-hostname <new-hostname>
```

- **Open a new terminal tab** to see the effect.
- **OR** use the `exec bash` command to apply the change in the current tab.

> [!note] #### Additional Note
> 
> If you have a domain name, add it after the new hostname. For example:
> ```bash
> new-hostname.mydomain.com
> ```
> Note that the terminal will display only `new-hostname`, not the full domain name.

### Steps to Update the `/etc/hosts` File

1. **Open the `/etc/hosts` File:**
   ```bash
   sudo nano /etc/hosts
   ```

2. **Edit the File:**
   Find the line that maps the current hostname to the loopback address (127.0.0.1 or :\:1 for IPv6) and update it with the new hostname.

   Before:
   ```
   127.0.0.1   old-hostname
   ```

   After:
   ```
   127.0.0.1   new-hostname
   ```

   If you are adding a domain name, it would look like this:
   ```
   127.0.0.1   new-hostname new-hostname.mydomain.com
   ```

3. **Save and Exit:**
   - Save the changes and exit the text editor (in nano, you would press `Ctrl+X`, then `Y`, and `Enter`).


> [!question]- #### Why Update the `/etc/hosts` File?
> #### Why Update the `/etc/hosts` File?
> 
> Updating the `/etc/hosts` file is crucial for the following reasons:
> 
> 1. **Local Name Resolution:**
>    - The `/etc/hosts` file maps hostnames to IP addresses. By updating it, you ensure that your system can correctly resolve the new hostname to its corresponding IP address locally without relying on an external DNS server.
> 
> 2. **Avoiding Conflicts:**
>    - If the new hostname is not updated in the `/etc/hosts` file, there might be conflicts or issues in resolving the hostname. This can lead to problems in network communication and accessing services hosted on your machine.
> 
> 3. **Consistency:**
>    - Updating the `/etc/hosts` file ensures that all applications and services running on your system are aware of the new hostname. This is particularly important for services that rely on hostname resolution for configuration and communication.
> 
> 4. **SSH and Remote Access:**
>    - Properly mapping the hostname in `/etc/hosts` can simplify SSH and other remote access configurations, making it easier to connect to your machine using the hostname instead of the IP address.
> 