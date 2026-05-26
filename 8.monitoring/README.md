# Linux System Monitoring

## Introduction to System Monitoring
Monitoring system resources is essential to ensure optimal performance, detect issues, and troubleshoot problems in Linux. Various tools allow us to monitor CPU, memory, disk usage, network activity, and running processes.

## Index of Commands Covered

### CPU and Memory Monitoring
- `top` – Real-time system monitoring
- `htop` – Interactive process viewer (requires installation)
- `vmstat` – Report system performance statistics
- `free -m` – Show memory usage

### Disk Monitoring
- `df -h` – Check disk space usage
- `du -sh /path` – Show disk usage of a specific directory
- `iostat` – Display CPU and disk I/O statistics

### Network Monitoring
- `ifconfig` – Show network interfaces (deprecated, use `ip a`)
- `ip a` – Show network interface details
- `netstat -tulnp` – Show active connections and listening ports
- `ss -tulnp` – Alternative to `netstat` for socket statistics
- `ping hostname` – Test network connectivity
- `traceroute hostname` – Show network path to a host
- `nslookup domain` – Get DNS resolution details

### Log Monitoring
- `tail -f /var/log/syslog` – Live monitoring of system logs
- `journalctl -f` – Live system logs for systemd-based distros
- `dmesg | tail` – View kernel logs

## CPU and Memory Monitoring
### Using `top`
To view real-time CPU and memory usage:
```bash
top
```
Press `q` to quit.

### Using `htop`
A user-friendly alternative:
```bash
htop
```
Use arrow keys to navigate and `F9` to kill processes.

### Using `vmstat`
To check CPU, memory, and I/O stats:
```bash
vmstat 1 5  # Update every 1 sec, show 5 updates
```

### Checking Memory Usage
```bash
free -m
```
Shows free and used memory in megabytes.

## Disk Monitoring
### Using `df`
Check available disk space:
```bash
df -h
```
### Using `du`
Find the size of a directory:
```bash
du -sh /var/log
```
### Using `iostat`
Check disk and CPU usage:
```bash
iostat
```

## Network Monitoring
### Checking Network Interfaces
```bash
ip a  # Show IP addresses and interfaces
```
### Viewing Open Ports and Connections
```bash
netstat -tulnp  # Show listening ports
ss -tulnp  # Alternative to netstat
```
### Testing Connectivity
```bash
ping google.com  # Test internet connection
traceroute google.com  # Trace the path to Google
```
### Checking DNS Resolution
```bash
nslookup example.com
```

## Log Monitoring
### Live Monitoring of System Logs
```bash
tail -f /var/log/syslog  # Follow logs in real-time
journalctl -f  # Systemd logs
```
### Checking Kernel Logs
```bash
dmesg | tail
```

# Disk Management in Linux

Disk management is used to check disk space, create partitions, format disks, mount disks, and manage storage.

---

## 1. Basic Disk Checking Commands

### Check disk space usage

```bash
df -h
```

Shows mounted disk usage in human-readable format.

Example:

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       30G   12G   18G  40% /
```

---

### Check disk usage of files and folders

```bash
du -sh *
```

Shows size of each file/folder in the current directory.

---

### Check size of a specific folder

```bash
du -sh /var/log
```

---

### Show block devices/disks

```bash
lsblk
```

Shows attached disks, partitions, and mount points.

Example:

```bash
NAME     SIZE TYPE MOUNTPOINT
xvda      30G disk
└─xvda1   30G part /
xvdf      10G disk
```

Here `xvdf` is a new disk, but not yet mounted.

---

### Show disk partitions

```bash
fdisk -l
```

Shows all disk partitions.

---

### Show filesystem type

```bash
blkid
```

Example:

```bash
/dev/xvda1: UUID="xxxx" TYPE="ext4"
```

---

## 2. EC2 Volume Creation Demo

### Step 1 — Create EBS Volume from AWS Console

1. Go to **AWS Console**
2. Open **EC2**
3. Go to **Elastic Block Store**
4. Click **Volumes**
5. Click **Create volume**
6. Select:
   - Volume type: `gp3`
   - Size: `10 GiB`
   - Availability Zone: Same as your EC2 instance
7. Click **Create volume**

Important:

```text
EBS volume and EC2 instance must be in the same Availability Zone.
```

Example:

```text
EC2 Instance AZ: us-east-1a
EBS Volume AZ: us-east-1a
```

---

### Step 2 — Attach Volume to EC2

1. Select the created volume
2. Click **Actions**
3. Click **Attach volume**
4. Select your EC2 instance
5. Device name example:

```text
/dev/sdf
```

6. Click **Attach volume**

---

## 3. Configure New Disk Inside Linux EC2

### Step 1 — Check attached disk

Login to EC2 and run:

```bash
lsblk
```

Example output:

```bash
NAME     SIZE TYPE MOUNTPOINT
xvda      30G disk
└─xvda1   30G part /
xvdf      10G disk
```

Here `/dev/xvdf` is the new attached disk.

---

### Step 2 — Check if filesystem already exists

```bash
sudo file -s /dev/xvdf
```

If output shows:

```bash
/dev/xvdf: data
```

It means the disk is empty and not formatted.

---

### Step 3 — Format the disk

```bash
sudo mkfs -t ext4 /dev/xvdf
```

This creates an `ext4` filesystem on the disk.

Warning:

```text
Do not run mkfs on a disk that already has important data.
It will erase existing data.
```

---

### Step 4 — Create mount directory

```bash
sudo mkdir /data
```

---

### Step 5 — Mount the disk

```bash
sudo mount /dev/xvdf /data
```

---

### Step 6 — Verify mount

```bash
df -h
```

or

```bash
lsblk
```

Example:

```bash
/dev/xvdf   10G   24M   9.5G   1% /data
```

---

### Step 7 — Test by creating a file

```bash
cd /data
sudo touch testfile.txt
ls -l
```

---

## 4. Make Mount Permanent After Reboot

If we only use `mount`, the disk will unmount after reboot.

To mount permanently, add entry in `/etc/fstab`.

---

### Step 1 — Get UUID of disk

```bash
sudo blkid /dev/xvdf
```

Example output:

```bash
/dev/xvdf: UUID="abcd-1234-efgh-5678" TYPE="ext4"
```

Copy the UUID.

---

### Step 2 — Backup fstab file

```bash
sudo cp /etc/fstab /etc/fstab.bkp
```

---

### Step 3 — Edit fstab

```bash
sudo vi /etc/fstab
```

Add this line:

```bash
UUID=abcd-1234-efgh-5678 /data ext4 defaults,nofail 0 2
```

Save and exit:

```bash
:wq
```

---

### Step 4 — Test fstab entry

```bash
sudo mount -a
```

If no error comes, the entry is correct.

---

### Step 5 — Verify

```bash
df -h
```

---

## 5. Useful Disk Management Commands

### Check disk space

```bash
df -h
```

### Check folder size

```bash
du -sh /foldername
```

### Check all folder sizes

```bash
du -sh *
```

### List disks

```bash
lsblk
```

### Check disk details

```bash
sudo fdisk -l
```

### Check filesystem type

```bash
blkid
```

### Format disk as ext4

```bash
sudo mkfs -t ext4 /dev/xvdf
```

### Create mount point

```bash
sudo mkdir /data
```

### Mount disk

```bash
sudo mount /dev/xvdf /data
```

### Unmount disk

```bash
sudo umount /data
```

### Check open files if unmount fails

```bash
sudo lsof +f -- /data
```

### Force check mount file

```bash
sudo mount -a
```

### View fstab

```bash
cat /etc/fstab
```

### Edit fstab

```bash
sudo vi /etc/fstab
```

---

## 6. Disk Partition Demo

Sometimes we create a partition before formatting.

### Step 1 — Start partition tool

```bash
sudo fdisk /dev/xvdf
```

Inside fdisk:

```text
n  → create new partition
p  → primary partition
1  → partition number
Enter → default first sector
Enter → default last sector
w  → write changes
```

---

### Step 2 — Check partition

```bash
lsblk
```

Example:

```bash
xvdf      10G disk
└─xvdf1   10G part
```

---

### Step 3 — Format partition

```bash
sudo mkfs -t ext4 /dev/xvdf1
```

---

### Step 4 — Mount partition

```bash
sudo mkdir /data
sudo mount /dev/xvdf1 /data
```

---

### Step 5 — Verify

```bash
df -h
```

---

## 7. Expanding Existing EC2 Root Volume Demo

### Step 1 — Increase volume size from AWS Console

1. Go to **EC2**
2. Go to **Volumes**
3. Select root volume
4. Click **Modify volume**
5. Increase size, example `30 GiB` to `50 GiB`
6. Click **Modify**

---

### Step 2 — Check disk size in Linux

```bash
lsblk
```

Example:

```bash
xvda      50G disk
└─xvda1   30G part /
```

Disk is 50G, but partition is still 30G.

---

### Step 3 — Grow partition

For Ubuntu EC2:

```bash
sudo growpart /dev/xvda 1
```

For Amazon Linux also usually same:

```bash
sudo growpart /dev/xvda 1
```

---

### Step 4 — Resize filesystem

For ext4 filesystem:

```bash
sudo resize2fs /dev/xvda1
```

For XFS filesystem:

```bash
sudo xfs_growfs /
```

---

### Step 5 — Verify

```bash
df -h
```

Now root volume should show increased size.

---

## 8. Important Notes

```text
df -h      = shows mounted disk usage
du -sh     = shows folder/file size
lsblk      = shows attached disks
fdisk -l   = shows partition details
blkid      = shows filesystem UUID
mkfs       = formats disk
mount      = attaches disk to folder
umount     = removes disk from folder
fstab      = permanent mount after reboot
```

---

## 9. Simple Real-Time Demo Flow

```bash
# Check current disks
lsblk

# Check disk usage
df -h

# Check new attached disk
lsblk

# Check if disk is empty
sudo file -s /dev/xvdf

# Format disk
sudo mkfs -t ext4 /dev/xvdf

# Create mount point
sudo mkdir /data

# Mount disk
sudo mount /dev/xvdf /data

# Verify
df -h
lsblk

# Create test file
sudo touch /data/demo.txt
ls -l /data

# Get UUID
sudo blkid /dev/xvdf

# Backup fstab
sudo cp /etc/fstab /etc/fstab.bkp

# Add UUID entry in fstab
sudo vi /etc/fstab

# Test fstab
sudo mount -a

# Verify again
df -h
```
