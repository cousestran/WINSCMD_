## Changing Computer Name in Linux

### Understanding Linux Hostnames

In Linux, the hostname is a crucial system identifier used for network communication and system management. A Linux system typically has three types of hostnames:

1. **Static Hostname**: Set by the system administrator and stored in `/etc/hostname`
2. **Transient Hostname**: Maintained by the kernel, can be changed at runtime
3. **Pretty Hostname**: A free-form UTF8 hostname for presentation

### Prerequisites

- Root or sudo privileges
- Access to a terminal
- Basic knowledge of Linux command line
- Backup of important configuration files
- Understanding of your distribution's init system (systemd, SysVinit, etc.)

### Method 1: Using hostnamectl (systemd-based systems)

`hostnamectl` is the modern, recommended tool for managing hostnames on systemd-based Linux distributions (Ubuntu 16.04+, Debian 8+, RHEL/CentOS 7+, Fedora 15+, and others).

#### When to Use This Method
- Modern Linux distributions with systemd
- When you need to manage all hostname types (static, transient, pretty)
- For scripting and automation purposes
- When you need persistent changes that survive reboots

#### Step-by-Step Guide

1. **Check Current Hostname Configuration**
   ```bash
   # Show complete hostname information
   hostnamectl
   
   # View specific hostname types individually
   hostname                    # Current hostname (transient if set, otherwise static)
   hostname -f                 # Fully qualified domain name (FQDN)
   hostname -s                 # Short hostname (first component of FQDN)
   hostname -d                 # Domain name (everything after the first dot)
   hostname -i                 # IP addresses for the hostname
   
   # View the static hostname file
   cat /etc/hostname
   
   # Check which process is managing the hostname
   systemctl status systemd-hostnamed
   ```

2. **Change the Hostname**
   
   **Basic Usage:**
   ```bash
   # Set the static hostname (persistent across reboots)
   sudo hostnamectl set-hostname new-hostname
   
   # Set a pretty hostname (for display purposes only, can include spaces and special chars)
   sudo hostnamectl set-hostname --pretty "New Pretty Hostname"
   
   # Set the transient hostname (temporary, lost on reboot)
   sudo hostnamectl --transient set-hostname temp-hostname
   
   # Set all three hostname types at once
   sudo hostnamectl set-hostname new-hostname \
       --static \
       --transient \
       --pretty "New Pretty Hostname"
   ```
   
   **Advanced Usage:**
   ```bash
   # Set hostname with a specific location/chassis type
   sudo hostnamectl set-hostname "web-01" --static \
       --pretty "Web Server 01 (Production)" \
       --icon-name "computer-server" \
       --chassis "server"
   
   # Set hostname from a variable
   NEW_NAME="app-server-01"
   sudo hostnamectl set-hostname "$NEW_NAME"
   
   # Set hostname from command output (e.g., AWS instance ID)
   INSTANCE_ID=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)
   sudo hostnamectl set-hostname "app-${INSTANCE_ID}"
   ```

3. **Verify the Changes**
   ```bash
   # Check all hostname types and system information
   hostnamectl
   
   # Verify the static hostname file
   cat /etc/hostname
   
   # Check all hostname types individually
   hostnamectl --static
   hostnamectl --transient
   hostnamectl --pretty
   
   # Check if the hostname is valid
   hostname -f >/dev/null 2>&1 && echo "Hostname is valid" || echo "Invalid hostname"
   ```

4. **Update System Configuration**
   ```bash
   # Update the mailname (used by mail services like postfix)
   echo "new-hostname" | sudo tee /etc/mailname
   
   # Update the login banner
   sudo sed -i "s/$(hostname -s)/new-hostname/g" /etc/issue
   sudo sed -i "s/$(hostname -s)/new-hostname/g" /etc/issue.net
   
   # Update common configuration files
   for file in /etc/*.conf; do
       [ -f "$file" ] && sudo sed -i "s/$(hostname -s)/new-hostname/g" "$file"
   done
   
   # Update application configurations (examples)
   if [ -f /etc/nginx/nginx.conf ]; then
       sudo sed -i "s/$(hostname -s)/new-hostname/g" /etc/nginx/nginx.conf
       sudo systemctl restart nginx
   fi
   
   # Restart system services to apply changes
   sudo systemctl restart systemd-hostnamed
   sudo systemctl restart systemd-journald
   ```

#### Troubleshooting

1. **Hostname Not Updating**
   ```bash
   # Check for conflicting configurations
   grep -r "$(hostname)" /etc/
   
   # Restart the hostname service
   sudo systemctl restart systemd-hostnamed
   ```

2. **Network Issues After Renaming**
   ```bash
   # Flush DNS cache
   if command -v systemd-resolve &> /dev/null; then
       sudo systemd-resolve --flush-caches
   fi
   
   # Restart network services
   sudo systemctl restart NetworkManager
   ```

3. **Services Not Recognizing New Hostname**
   ```bash
   # Restart affected services
   sudo systemctl restart sshd
   
   # Check service logs
   journalctl -u sshd --no-pager | tail -n 50
   ```

#### Best Practices
- Always back up configuration files before making changes
- Test hostname changes in a non-production environment first
- Document all changes made to the system
- Consider updating SSL certificates if they include the hostname
- Update monitoring and logging systems with the new hostname

### Method 2: Editing Configuration Files (All Distributions)

For systems without systemd or for more control over the hostname configuration, you can manually edit the necessary configuration files.

#### When to Use This Method
- Older Linux distributions without systemd
- When you need fine-grained control over hostname configuration
- For minimal Linux installations
- When troubleshooting hostname issues

#### Step-by-Step Guide

1. **Backup Current Configuration**
   ```bash
   # Create timestamped backups of important files
   sudo cp /etc/hostname /etc/hostname.bak.$(date +%Y%m%d)
   sudo cp /etc/hosts /etc/hosts.bak.$(date +%Y%m%d)
   ```

2. **Update /etc/hostname**
   ```bash
   # Set the new hostname (replace 'new-hostname' with your desired name)
   echo "new-hostname" | sudo tee /etc/hostname
   
   # For immediate effect (without reboot)
   sudo hostname new-hostname
   ```

3. **Update /etc/hosts**
   ```bash
   # Edit the hosts file
   sudo nano /etc/hosts
   
   # Look for a line like:
   # 127.0.1.1    old-hostname
   # Change it to:
   # 127.0.1.1    new-hostname
   
   # Also update any other occurrences of the old hostname
   ```

4. **Update Network Configuration**
   
   **For systems using NetworkManager:**
   ```bash
   # List all connections
   nmcli connection show
   
   # Update the hostname for a specific connection
   nmcli connection modify "Wired connection 1" connection.id "new-hostname"
   ```
   
   **For systems using /etc/network/interfaces:**
   ```bash
   # Edit the network interfaces file
   sudo nano /etc/network/interfaces
   
   # Add or update the hostname line
   # hostname new-hostname
   ```

5. **Restart Networking Services**
   ```bash
   # For systemd-based systems
   sudo systemctl restart systemd-hostnamed
   sudo systemctl restart NetworkManager
   
   # For SysVinit systems
   sudo /etc/init.d/hostname.sh restart
   sudo /etc/init.d/networking restart
   ```

6. **Verify the Changes**
   ```bash
   # Check the current hostname
   hostname
   hostname -f
   
   # Check the static hostname
   cat /etc/hostname
   
   # Check DNS resolution
   getent hosts new-hostname
   ping -c 1 new-hostname
   ```

#### Troubleshooting

1. **Hostname Not Updating**
   - Verify file permissions on /etc/hostname and /etc/hosts
   - Check for typos in configuration files
   - Look for conflicting configurations in /etc/sysconfig/network or /etc/network/interfaces
   - Check system logs for errors: `journalctl -xe` or `dmesg | grep -i hostname`

2. **Network Issues After Renaming**
   - Verify DNS resolution works with the new hostname
   - Check /etc/nsswitch.conf for proper host resolution order
   - Restart network services: `sudo systemctl restart NetworkManager` or `sudo service networking restart`
   - Check firewall rules if they reference the old hostname

3. **Services Not Recognizing New Hostname**
   - Restart affected services
   - Check service-specific configuration files for hardcoded hostnames
   - Look for cached hostname information in /var/run or /run
   - Check application logs for hostname-related errors

#### Best Practices
- Always back up configuration files before making changes
- Test changes in a non-production environment first
- Document all changes made to the system
- Update monitoring and logging systems with the new hostname
- Consider updating SSL certificates if they include the hostname
- Update any scripts or automation that reference the hostname
- Update any configuration management systems (Ansible, Puppet, Chef, etc.)
- Update any backup configurations that might include the hostname

### Method 3: Using nmtui (Network Manager)

The NetworkManager Text User Interface (nmtui) provides a simple, text-based interface to configure network settings, including the hostname, on Linux systems with NetworkManager.

#### When to Use This Method
- When you prefer a guided, menu-driven interface
- For systems with NetworkManager installed
- When you need to configure both hostname and network settings
- For quick, one-time changes without remembering commands

#### Step-by-Step Guide

1. **Launch nmtui**
   ```bash
   sudo nmtui
   ```

2. **Navigate to "Set system hostname"**
   - Use arrow keys to navigate
   - Press Enter to select

3. **Enter New Hostname**
   - Type the new hostname in the dialog box
   - Use Tab to switch between fields
   - Select "OK" and press Enter

4. **Restart NetworkManager**
   ```bash
   sudo systemctl restart NetworkManager
   ```

5. **Verify Changes**
   ```bash
   hostnamectl
   hostname
   ```

#### Troubleshooting
- If nmtui is not installed: `sudo apt install network-manager` (Debian/Ubuntu) or `sudo yum install NetworkManager-tui` (RHEL/CentOS)
- If changes don't persist after reboot, check for conflicting configurations in /etc/hostname
- Verify NetworkManager is managing the network: `nmcli general status`

### Method 4: Using GUI Tools

For desktop Linux users, graphical tools provide an easy way to change the hostname without using the command line.

#### 4.1 GNOME Settings (Ubuntu, Fedora Workstation, etc.)

1. Open Settings (Super key + type "Settings")
2. Go to "About" in the sidebar
3. Click the "Device Name" field
4. Enter the new hostname and click "Rename"
5. Authenticate if prompted
6. Restart the system for all services to recognize the new hostname

#### 4.2 KDE System Settings (Kubuntu, KDE Plasma)

1. Open System Settings
2. Navigate to "System Administration" > "System Information"
3. Click the "Computer Name" field
4. Enter the new hostname and click "Apply"
5. Authenticate if prompted
6. Restart the system for all services to recognize the new hostname

### Method 5: For Specific Distributions

#### 5.1 Debian/Ubuntu (SysVinit)

For older Debian/Ubuntu systems using SysVinit:

1. Edit /etc/hostname:
   ```bash
   sudo nano /etc/hostname
   # Replace with new hostname
   ```

2. Update /etc/hosts:
   ```bash
   sudo nano /etc/hosts
   # Update 127.0.1.1 line with new hostname
   ```

3. Set the hostname immediately:
   ```bash
   sudo hostname new-hostname
   ```

4. Restart networking:
   ```bash
   sudo /etc/init.d/hostname.sh
   sudo /etc/init.d/networking restart
   ```

#### 5.2 RHEL/CentOS 6 and Earlier

For older RHEL/CentOS systems:

1. Edit /etc/sysconfig/network:
   ```bash
   sudo nano /etc/sysconfig/network
   # Update HOSTNAME= line
   ```

2. Update /etc/hosts:
   ```bash
   sudo nano /etc/hosts
   # Update hostname entries
   ```

3. Set the hostname immediately:
   ```bash
   sudo hostname new-hostname
   ```

4. Restart network services:
   ```bash
   sudo service network restart
   ```

### Advanced Configuration

#### Updating Multiple Configuration Files

Some applications store the hostname in their configuration files. Common locations to check:

```bash
# Common configuration files that might contain hostnames
/etc/mailname
/etc/postfix/main.cf
/etc/ssmtp/ssmtp.conf
/etc/monit/monitrc
/etc/munin/munin-node.conf
/etc/collectd/collectd.conf
/etc/nginx/nginx.conf
/etc/apache2/sites-available/*
```

#### Handling Services That Cache the Hostname

Some services cache the hostname on startup. After changing the hostname, you may need to restart these services:

```bash
# Common services that might need restarting
sudo systemctl restart sshd
sudo systemctl restart postfix
sudo systemctl restart rsyslog
sudo systemctl restart crond
```

#### Updating SSL Certificates

If you're using SSL certificates that include the hostname, you'll need to regenerate them:

1. Locate your SSL certificate files (common locations):
   ```bash
   /etc/ssl/certs/
   /etc/pki/tls/certs/
   /etc/letsencrypt/live/
   ```

2. Regenerate or request new certificates
3. Update any applications using these certificates
4. Restart web servers and other services using SSL

### Troubleshooting Common Issues

#### Hostname Not Persisting After Reboot

1. Check for conflicting configurations:
   ```bash
   grep -r "old-hostname" /etc/
   ```

2. Verify the hostname service is enabled:
   ```bash
   sudo systemctl enable systemd-hostnamed
   ```

3. Check for cloud-init overrides:
   ```bash
   cat /etc/cloud/cloud.cfg
   ```

#### Services Not Recognizing New Hostname

1. Check service logs:
   ```bash
   journalctl -u service-name
   ```

2. Look for hardcoded hostnames:
   ```bash
   grep -r "old-hostname" /etc/
   ```

3. Restart the service:
   ```bash
   sudo systemctl restart service-name
   ```

#### Network Issues After Renaming

1. Flush DNS caches:
   ```bash
   sudo systemd-resolve --flush-caches
   sudo systemctl restart systemd-resolved
   ```

2. Check /etc/hosts for incorrect entries
3. Verify network manager configuration:
   ```bash
   nmcli general status
   nmcli connection show
   ```

### Security Considerations

#### SSH Host Keys

When changing the hostname, consider regenerating SSH host keys to avoid potential security warnings:

```bash
# Backup existing keys
sudo cp -r /etc/ssh /etc/ssh.backup.$(date +%Y%m%d)

# Remove old keys
sudo rm /etc/ssh/ssh_host_*

# Generate new keys
sudo dpkg-reconfigure openssh-server

# Restart SSH service
sudo systemctl restart sshd
```

#### SSL/TLS Certificates

1. Update any SSL/TLS certificates that include the hostname
2. Check certificate validity:
   ```bash
   openssl x509 -in /path/to/cert.pem -text | grep -i subject
   ```
3. Update certificate revocation lists (CRLs) if needed

#### Service-Specific Configurations

Check and update configurations for:
- Web servers (Apache, Nginx)
- Database servers (MySQL, PostgreSQL)
- Mail servers (Postfix, Sendmail)
- Monitoring systems (Nagios, Zabbix)
- Backup solutions
- Configuration management tools

### Best Practices

#### Naming Conventions
- Use only lowercase letters, numbers, and hyphens
- Keep names short but descriptive (e.g., 'web01', 'db-prod-01')
- Avoid special characters and underscores
- Follow organizational naming standards if they exist
- Document the naming convention being used

#### Documentation
- Keep a record of all hostname changes
- Document the reason for the change
- Note any services or applications affected
- Update network diagrams and system documentation
- Inform relevant teams about the change

#### Testing
- Test hostname changes in a development environment first
- Verify all critical services after the change
- Check network connectivity from other systems
- Test any automation or monitoring systems
- Have a rollback plan in case of issues
- Schedule changes during maintenance windows
