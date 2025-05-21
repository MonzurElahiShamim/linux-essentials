---
width: 1920
height: 1080
transition: slide
slide: true
---

# Intermediate Linux Commands

---
## File Viewing Commands

---

### less/more: View file content page by page.

+ `less file.txt`: Scroll with arrow keys (quitting: `q`).
+ `/search_term`: Search for a term while viewing.
+ `more file.txt`: Similar to less, but less flexible.

---

### `head/tail`: View specific lines of a file.

+ `head file.txt`: Display first 10 lines.
+ `head -n 15 file.txt`: Display first 15 lines.
+ `tail file.txt`: Display last 10 lines.
+ `tail -n 15 file.txt`: Display last 15 lines.
+ `tail -f file.txt`: Continuously display appended lines in real-time.

---

## Text Processing Commands

---

### grep: Search for patterns in a file.

+ `grep 'pattern' file.txt`:  Finds lines matching the pattern.
+ `grep -i 'pattern' file.txt`: Ignore case while searching.
+ `grep -n 'pattern' file.txt`: Show line numbers of matching lines.
+ `grep -c 'pattern' file.txt`: Count occurrences of the pattern.
+ `grep -v 'pattern' file.txt`: Invert match (show lines that don’t match).

---

### cut: Extract specific fields/columns from input.

+ `cut -f1 file.txt`: Extract the 1st column using ‘`tab`’ as a delimiter.
+ `cut -d':' -f1 file.txt`: Extract the first column using ‘:’ as a delimiter.
+ `cut -c1-5 file.txt`: Extract characters 1 to 5 from each line.

---

### sort: Sort lines in a file.

+ `sort file.txt`: Sort alphabetically.
+ `sort -n file.txt`: Sort numerically.
+ `sort -r file.txt`: Sort in reverse order.

---

### uniq: Filter out duplicate lines.

+ `uniq file.txt`: Removes consecutive duplicates.
+ `sort file.txt | uniq -c`: Count occurrences of unique lines.

---

## Shell Commands

---

### Piping (|): Chain commands by passing the output of one command as input to another.

- Example: `ls | grep '.txt'`: List `.txt` files.
- Combine multiple tools: `cat file.txt | sort | uniq`.

---

### Search in History

- `history | grep command`: Search previously run commands.
+ `Ctrl + r`: Interactive search in command history.

---

### Alias: Create shortcuts for commands.

- `alias ll='ls -la'`: Shortcut for `ls -la`.
+ `unalias ll`: Remove the alias.

---

## Networking

---

### ssh: Securely connect to remote systems.

+ `ssh user@hostname`: Connect to a remote host.
+ `ssh -p 2222 user@hostname`: Connect using a specific port.
+ `ssh -i /path/to/key.pem user@hostname`: Connect using a specific private key.

---

### Viewing Listening Ports:

- `netstat -tuln` or `ss -tuln`: Display active listening ports.

---

### firewalld/ufw: Firewall management tools.

---

#### **firewalld Commands:**

- `firewall-cmd --state`: Check the status of **firewalld**.
- `firewall-cmd --zone=public --add-port=80/tcp --permanent`: Open port 80 (HTTP) for TCP traffic.
- `firewall-cmd --reload`: Reload **firewalld** to apply changes.
- `firewall-cmd --list-all`: List all settings in the current zone.
- `firewall-cmd --zone=public --remove-port=80/tcp --permanent`: Close port 80 (HTTP) for TCP traffic.
- `firewall-cmd --list-services`: Show the allowed services in the current zone.
- `firewall-cmd --zone=public --add-service=http --permanent`: Allow HTTP service.

---

#### **ufw Commands:**

- `ufw enable`: Enable **ufw** firewall.
- `ufw disable`: Disable **ufw** firewall.
- `ufw status`: Show **ufw** status.
- `ufw allow 22/tcp`: Allow SSH (port 22) for TCP traffic.
- `ufw deny 80/tcp`: Deny HTTP (port 80) for TCP traffic.
- `ufw allow from 192.168.1.0/24`: Allow traffic from a specific IP range.
- `ufw delete allow 22/tcp`: Remove the rule allowing SSH (port 22).
- `ufw reset`: Reset **ufw** to default settings.


---

## Process Management

---

### Running Process in Background

+ `command &`: Run a command in the background.
+ `fg`: Bring background process to foreground.
+ `jobs`: List background processes.

---

### Viewing Running Processes

- `ps aux`: Display all running processes.
- `top` or `htop`: Monitor live system processes.

---

### Kill a Process

- `kill PID`: Terminate process with a given PID.
- `kill -9 PID`: Force kill a process.

---

## Disk Usage and Storage

---

### Disk Usage

- `df -h`: Show disk usage with human-readable sizes.
- `du -sh directory`: Display total size of a directory.

---

### Partition and Filesystem

- `lsblk`: Show block device details.
- `fdisk -l`: List available partitions.
- `mount /dev/sdX /mnt`: Mount a device.
- `umount /mnt`: Unmount a device.

---

## System Monitoring

---

### Basic Monitoring

- `uptime`: Show system uptime and load average.
- `free -h`: Display memory usage.
- `vmstat`: Monitor system performance.

---

## Package Management

---

### APT (Debian-based systems)

- `apt update`: Update package lists.
- `apt install package`: Install a package.
- `apt remove package`: Remove a package.

---

### YUM/DNF (RHEL-based systems)

- `yum install package` or `dnf install package`: Install a package.
- `yum update` or `dnf update`: Update all packages.

---

## Input/Output and Environment

---

### STDIN, STDOUT, and STDERR

+ Redirect output (STDOUT): `command > file.txt`.
+ Append output (STDOUT): `command >> file.txt`.
+ Redirect errors (STDERR): `command 2> error.log`.
+ Redirect both STDOUT and STDERR: `command > output.log 2>&1`.
+ Discard errors: `command 2>/dev/null`.

---

### Environment Variable

- `export VAR=value`: Set environment variable.
- `echo $VAR`: Display variable value.
- `env`: View all environment variables.

---
