# Increase `swap` space in `Oracle Linux 7`

#### **Step 1: Check Current Swap Size**
Run the following command to verify your current swap size:
```bash
sudo swapon --show
```

#### **Step 2: Create a Swap File**
If your current swap space is insufficient, you can create a new swap file to increase the swap size:

1. **Create a new swap file of 2GB** (adjust the size if needed):
   ```bash
   sudo fallocate -l 2G /swapfile
   ```

   If `fallocate` is not available, you can use `dd` instead:
   ```bash
   sudo dd if=/dev/zero of=/swapfile bs=1M count=2048
   ```

2. **Set the correct permissions for the swap file**:
   ```bash
   sudo chmod 600 /swapfile
   ```

3. **Set up the swap file**:
   ```bash
   sudo mkswap /swapfile
   ```

4. **Enable the swap file**:
   ```bash
   sudo swapon /swapfile
   ```

5. **Verify that the swap file is active**:
   ```bash
   sudo swapon --show
   ```

#### **Step 3: Make the Swap Permanent**
To ensure the swap file persists across reboots, add it to the `/etc/fstab` file:

1. Open `/etc/fstab` with a text editor:
   ```bash
   sudo nano /etc/fstab
   ```

2. Add the following line at the end of the file:
   ```bash
   /swapfile   swap    swap    defaults    0   0
   ```

3. Save and exit.

#### **Step 4: Confirm the New Swap Size**
Check that the new swap space has been added successfully:
```bash
free -h
```

This should show the increased swap space.
