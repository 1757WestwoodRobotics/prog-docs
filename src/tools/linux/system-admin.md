# System Administration for FRC Linux Systems

System administration skills are essential for maintaining reliable FRC development environments and troubleshooting robot systems. This page covers practical Linux administration focused on FRC scenarios.

## User and Permission Management

Understanding Linux users and permissions is crucial for both development machines and RoboRIO management.

### User Management Basics

```bash path=null start=null
# View current user
whoami
id

# List all users
cat /etc/passwd | cut -d: -f1

# Add user to group (useful for development)
sudo usermod -aG dialout $USER  # For serial port access
sudo usermod -aG docker $USER   # For Docker access

# Check group membership
groups
groups username
```

### File Permissions

```bash path=null start=null
# View permissions
ls -la

# Change permissions
chmod +x script.sh          # Make executable
chmod 644 file.txt          # Read/write for owner, read for others
chmod 755 directory/        # Standard directory permissions

# Change ownership
sudo chown user:group file.txt
sudo chown -R user:group directory/

# Special permissions for team sharing
chmod g+s shared_directory  # Set group ID bit
```

### Sudo Configuration

For team development machines, configure sudo properly:

```bash path=null start=null
# Edit sudoers file (ALWAYS use visudo)
sudo visudo

# Allow users in frc group to run robot deployment without password
%frc ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart robot

# Allow specific commands without password
username ALL=(ALL) NOPASSWD: /bin/systemctl restart robot, /bin/journalctl
```

## Network Administration

Network configuration is critical for robot connectivity and development workflows.

### Network Interface Configuration

```bash path=null start=null
# View network interfaces
ip addr show
ip link show

# Bring interface up/down
sudo ip link set eth0 up
sudo ip link set eth0 down

# Configure static IP (temporary)
sudo ip addr add 10.17.57.100/24 dev eth0
sudo ip route add default via 10.17.57.1

# View routing table
ip route show
```

### NetworkManager (Modern Linux)

```bash path=null start=null
# List connections
nmcli connection show

# Connect to WiFi
nmcli device wifi connect "SSID" password "password"

# Create connection profile for robot network
nmcli connection add type ethernet con-name "robot-eth" ifname eth0 \
  ip4.addresses 10.17.57.100/24 ip4.gateway 10.17.57.1 \
  ip4.dns 8.8.8.8 ip4.method manual

# Activate connection
nmcli connection up "robot-eth"
```

### Persistent Network Configuration

#### systemd-networkd (RoboRIO-style)

```ini path=null start=null
# /etc/systemd/network/10-robot-eth.network
[Match]
Name=eth0

[Network]
Address=10.17.57.100/24
Gateway=10.17.57.1
DNS=8.8.8.8
```

#### Traditional /etc/network/interfaces (Debian/Ubuntu)

```bash path=null start=null
# /etc/network/interfaces
auto eth0
iface eth0 inet static
    address 10.17.57.100
    netmask 255.255.255.0
    gateway 10.17.57.1
    dns-nameservers 8.8.8.8
```

## Service Management with systemd

systemd is the modern init system used on most Linux distributions, including the RoboRIO.

### Basic Service Commands

```bash path=null start=null
# Service status and control
sudo systemctl status robot
sudo systemctl start robot
sudo systemctl stop robot
sudo systemctl restart robot
sudo systemctl reload robot

# Enable/disable services
sudo systemctl enable robot    # Start on boot
sudo systemctl disable robot   # Don't start on boot

# List all services
systemctl list-units --type=service
systemctl list-units --failed
```

### Creating Custom Services

Create a service file for custom robot utilities:

```ini path=null start=null
# /etc/systemd/system/robot-logger.service
[Unit]
Description=Robot Data Logger
After=network.target
Wants=network.target

[Service]
Type=simple
User=lvuser
Group=lvuser
WorkingDirectory=/home/lvuser
ExecStart=/home/lvuser/logger/robot_logger.py
Restart=always
RestartSec=5
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

Manage the custom service:

```bash path=null start=null
# Reload systemd configuration
sudo systemctl daemon-reload

# Enable and start service
sudo systemctl enable robot-logger
sudo systemctl start robot-logger

# Check logs
journalctl -u robot-logger -f
```

## Process and Resource Management

Monitor and manage system resources effectively.

### Process Monitoring

```bash path=null start=null
# Real-time process monitoring
top
htop    # Enhanced version

# Process tree
pstree
ps aux --forest

# Find processes by name
pgrep python
pkill -f robot.py

# Monitor specific process
top -p $(pgrep -f robot.py)
```

### Resource Monitoring

```bash path=null start=null
# System load and uptime
uptime
cat /proc/loadavg

# Memory usage
free -h
cat /proc/meminfo

# Disk usage
df -h
du -h /home/lvuser | sort -h

# I/O statistics (if iostat available)
iostat -x 1 5
```

### Setting Resource Limits

Control resource usage for critical processes:

```bash path=null start=null
# Limit CPU usage (nice values)
nice -n 10 python robot.py     # Lower priority
renice -n 5 -p <PID>          # Change priority

# Memory limits with systemd
# In service file:
[Service]
MemoryLimit=512M
CPUShares=1024
```

## Log Management

Proper log management is essential for debugging and monitoring.

### journalctl (systemd logs)

```bash path=null start=null
# View all logs
journalctl

# Follow logs in real-time
journalctl -f

# Service-specific logs
journalctl -u robot
journalctl -u robot -f --since "1 hour ago"

# Filter by priority
journalctl -p err          # Error messages only
journalctl -p warning      # Warning and above

# Boot logs
journalctl -b             # Current boot
journalctl -b -1          # Previous boot
```

### Traditional Log Files

```bash path=null start=null
# Common log locations
tail -f /var/log/messages    # System messages
tail -f /var/log/syslog      # System log (Debian/Ubuntu)
tail -f /var/log/dmesg       # Kernel messages

# Application logs
tail -f /var/log/robot.log   # Custom application logs
```

### Log Rotation and Cleanup

```bash path=null start=null
# Configure journald limits
sudo vi /etc/systemd/journald.conf

# SystemMaxUse=100M
# SystemMaxFileSize=10M
# MaxRetentionSec=7d

# Manual cleanup
sudo journalctl --vacuum-time=7d      # Keep 7 days
sudo journalctl --vacuum-size=100M    # Keep 100MB

# Traditional log rotation (logrotate)
sudo vi /etc/logrotate.d/robot

/var/log/robot.log {
    daily
    rotate 7
    compress
    delaycompress
    missingok
    create 644 lvuser lvuser
}
```

## Package Management

Keep systems updated and manage software packages.

### APT (Debian/Ubuntu)

```bash path=null start=null
# Update package lists
sudo apt update

# Upgrade packages
sudo apt upgrade
sudo apt full-upgrade

# Install packages
sudo apt install git python3-pip lazygit

# Remove packages
sudo apt remove package-name
sudo apt purge package-name    # Remove config files too

# Search packages
apt search robotpy
apt show python3-pip
```

### YUM/DNF (RHEL/Fedora)

```bash path=null start=null
# Update system
sudo dnf update

# Install packages
sudo dnf install git python3-pip

# Search and info
dnf search robotpy
dnf info python3-pip
```

### Pacman (Arch Linux)

```bash path=null start=null
# Update system
sudo pacman -Syu

# Install packages
sudo pacman -S git python-pip lazygit

# Search packages
pacman -Ss robotpy
```

## Security and Hardening

Basic security practices for FRC development systems.

### SSH Security

```bash path=null start=null
# Generate strong SSH keys
ssh-keygen -t ed25519 -C "your-email@example.com"

# Configure SSH client
vi ~/.ssh/config

Host roborio-*
    User admin
    IdentityFile ~/.ssh/id_ed25519
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null

# SSH server hardening (on development machines)
sudo vi /etc/ssh/sshd_config

# Disable password authentication
PasswordAuthentication no
PubkeyAuthentication yes

# Change default port
Port 2222
```

### Firewall Configuration

```bash path=null start=null
# UFW (Uncomplicated Firewall) - Ubuntu
sudo ufw enable
sudo ufw default deny incoming
sudo ufw allow ssh
sudo ufw allow from 10.17.57.0/24  # Allow robot network

# iptables (traditional)
sudo iptables -L              # List rules
sudo iptables-save            # View current rules
```

### File System Security

```bash path=null start=null
# Set secure permissions on sensitive files
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
chmod 700 ~/.ssh

# Find files with incorrect permissions
find /home/user -type f -perm /o+w    # World-writable files
find /home/user -type f -perm /g+w    # Group-writable files
```

## Backup and Recovery

Protect important data and configurations.

### Configuration Backups

```bash path=null start=null
# Backup important configuration files
sudo tar -czf /backup/system-configs-$(date +%Y%m%d).tar.gz \
    /etc/ssh/ \
    /etc/systemd/system/ \
    /etc/network/ \
    /home/lvuser/.ssh/

# Robot code backup
tar -czf robot-backup-$(date +%Y%m%d).tar.gz \
    robot.py constants.py src/ requirements.txt
```

### Git-based Configuration Management

```bash path=null start=null
# Version control system configurations
cd /etc
sudo git init
sudo git add ssh/ systemd/system/ network/
sudo git commit -m "Initial system configuration"

# Track changes
sudo git diff
sudo git add -A
sudo git commit -m "Updated SSH configuration"
```

## Automation and Scripting

Automate common administration tasks.

### System Monitoring Script

```bash path=null start=null
#!/bin/bash
# monitor-robot.sh

LOG_FILE="/var/log/robot-monitor.log"

log_message() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

# Check robot connectivity
if ping -c 1 roborio-1757-frc.local &> /dev/null; then
    log_message "Robot is reachable"
else
    log_message "WARNING: Robot is not reachable"
fi

# Check disk space
DISK_USAGE=$(df /home | tail -1 | awk '{print $5}' | sed 's/%//')
if [ "$DISK_USAGE" -gt 80 ]; then
    log_message "WARNING: Disk usage is ${DISK_USAGE}%"
fi

# Check system load
LOAD=$(uptime | awk '{print $NF}')
log_message "System load: $LOAD"
```

### Automated Deployment Script

```bash path=null start=null
#!/bin/bash
# deploy-robot.sh

set -e

ROBOT_HOST="roborio-1757-frc.local"
ROBOT_USER="admin"
ROBOT_PATH="/home/lvuser"

echo "Starting deployment to $ROBOT_HOST..."

# Pre-deployment checks
if ! ping -c 1 "$ROBOT_HOST" &> /dev/null; then
    echo "ERROR: Cannot reach $ROBOT_HOST"
    exit 1
fi

# Deploy code
echo "Copying robot code..."
scp -r src/ robot.py constants.py requirements.txt \
    "$ROBOT_USER@$ROBOT_HOST:$ROBOT_PATH/"

# Install dependencies and restart
echo "Installing dependencies and restarting robot service..."
ssh "$ROBOT_USER@$ROBOT_HOST" << 'EOF'
cd /home/lvuser
pip3 install -r requirements.txt
sudo systemctl restart robot
EOF

echo "Deployment complete!"
```

## Troubleshooting Common Issues

### Boot Issues

```bash path=null start=null
# Check boot logs
journalctl -b
dmesg | less

# Check failed services
systemctl --failed

# Rescue mode (if system won't boot properly)
# Boot with systemd.unit=rescue.target
```

### Network Issues

```bash path=null start=null
# Diagnose network connectivity
ip addr show
ip route show
ping 8.8.8.8
nslookup google.com

# Reset network configuration
sudo systemctl restart networking
sudo systemctl restart NetworkManager
```

### Performance Issues

```bash path=null start=null
# Check system resources
top
iotop    # I/O monitoring
netstat -i    # Network interface statistics

# Check for high CPU processes
ps aux | sort -nr -k 3 | head -10

# Check for high memory processes  
ps aux | sort -nr -k 4 | head -10
```

This system administration knowledge provides the foundation for maintaining reliable, secure, and efficient Linux systems in FRC environments. Regular practice with these tools and techniques will make you an effective system administrator for your team's robotics infrastructure.
