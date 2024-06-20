# 9. Security and Permissions

## 9.1 Introduction to Linux Security and Permissions

- **Security and Permissions**: Ensuring that users and processes have the correct access to system resources while preventing unauthorized access.

### Key Concepts

- **Root User**: The superuser with full administrative access.
- **Regular Users**: Users with limited permissions.
- **Groups**: Collections of users that can be granted shared permissions.

## 9.2 File Permissions

### Understanding File Permissions

- **Permission Types**: Read (`r`), Write (`w`), Execute (`x`).
- **Permission Levels**: Owner, Group, Others.

```sh
# Example of file permissions
-rwxr-xr--  1 owner group  size date time file_name
```

#### Permission Breakdown

- `-rwxr-xr--`:
  - `-`: File type (e.g., `-` for regular file, `d` for directory).
  - `rwx`: Owner permissions (read, write, execute).
  - `r-x`: Group permissions (read, execute).
  - `r--`: Others permissions (read).

### Changing File Permissions

- **chmod**: Change file mode bits.

```sh
# Give read, write, and execute permissions to the owner
chmod u+rwx file_name

# Remove write permission for the group
chmod g-w file_name

# Give execute permission to others
chmod o+x file_name

# Set permissions using numeric notation (e.g., 755)
chmod 755 file_name
```

### Changing File Ownership

- **chown**: Change file owner and group.

```sh
# Change owner
chown new_owner file_name

# Change owner and group
chown new_owner:new_group file_name
```

- **chgrp**: Change group ownership.

```sh
chgrp new_group file_name
```

## 9.3 Special Permissions

### SUID (Set User ID)

- **SUID**: Allows a user to run an executable with the file owner's privileges.

```sh
chmod u+s file_name
```

### SGID (Set Group ID)

- **SGID**: Allows a user to run an executable with the file group's privileges.

```sh
chmod g+s file_name
```

### Sticky Bit

- **Sticky Bit**: Restricts file deletion in a directory to the file owner.

```sh
chmod +t directory_name
```

## 9.4 Access Control Lists (ACLs)

### Introduction to ACLs

- **ACLs**: Provide a more flexible permission mechanism than traditional UNIX permissions.

### Managing ACLs

- **setfacl**: Set file access control lists.

```sh
# Set ACL for a user
setfacl -m u:user:rwx file_name

# Set ACL for a group
setfacl -m g:group:r-x file_name

# Remove an ACL entry
setfacl -x u:user file_name

# Set default ACLs for a directory
setfacl -d -m u:user:rwx directory_name
```

- **getfacl**: Get file access control lists.

```sh
getfacl file_name
```

## 9.5 User and Group Management

### Creating and Managing Users

- **useradd**: Add a new user.

```sh
sudo useradd new_user
```

- **passwd**: Set or change a user password.

```sh
sudo passwd new_user
```

- **usermod**: Modify a user account.

```sh
# Add user to a group
sudo usermod -aG group_name user_name

# Change user login name
sudo usermod -l new_login old_login
```

- **userdel**: Delete a user account.

```sh
sudo userdel user_name
```

### Creating and Managing Groups

- **groupadd**: Add a new group.

```sh
sudo groupadd new_group
```

- **groupdel**: Delete a group.

```sh
sudo groupdel group_name
```

## 9.6 SSH (Secure Shell)

### Introduction to SSH

- **SSH**: A protocol for securely logging into remote systems.

### Configuring SSH

- **sshd_config**: The main configuration file for the SSH daemon.

```sh
# Edit the SSH configuration file
sudo nano /etc/ssh/sshd_config
```

### Key-Based Authentication

- **Generating SSH Keys**:

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- **Copying the Public Key to the Server**:

```sh
ssh-copy-id user@remote_host
```

### SSH Commands

- **Connecting to a Remote Host**:

```sh
ssh user@remote_host
```

- **Transferring Files with SCP**:

```sh
scp file_name user@remote_host:/path/to/destination
```

- **Using SFTP**:

```sh
sftp user@remote_host
```

## 9.7 Firewall Configuration

### Introduction to Firewalls

- **Firewall**: Controls incoming and outgoing network traffic based on security rules.

### Configuring iptables

- **iptables**: The traditional Linux firewall utility.

```sh
# Allow SSH traffic
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Block a specific IP address
sudo iptables -A INPUT -s 192.168.1.100 -j DROP

# Save iptables rules
sudo iptables-save > /etc/iptables/rules.v4
```

### Configuring ufw (Uncomplicated Firewall)

- **ufw**: A user-friendly interface for managing iptables.

```sh
# Enable ufw
sudo ufw enable

# Allow SSH traffic
sudo ufw allow ssh

# Deny incoming traffic from a specific IP
sudo ufw deny from 192.168.1.100

# Check ufw status
sudo ufw status
```

## 9.8 SELinux (Security-Enhanced Linux)

### Introduction to SELinux

- **SELinux**: A security module that provides a mechanism for supporting access control security policies.

### Managing SELinux

- **Checking SELinux Status**:

```sh
sestatus
```

- **Changing SELinux Modes**:

```sh
# Set SELinux to enforcing mode
sudo setenforce 1

# Set SELinux to permissive mode
sudo setenforce 0
```

- **Configuring SELinux**:

```sh
# Edit the SELinux configuration file
sudo nano /etc/selinux/config
```

### SELinux Commands

- **semanage**: Manage SELinux policy.

```sh
# Add a port to a service
sudo semanage port -a -t http_port_t -p tcp 8080
```

- **restorecon**: Restore the default SELinux context for files.

```sh
sudo restorecon -v /path/to/file
```

## 9.9 AppArmor

### Introduction to AppArmor

- **AppArmor**: A Linux security module that restricts programs' capabilities using per-program profiles.

### Managing AppArmor

- **Checking AppArmor Status**:

```sh
sudo apparmor_status
```

- **Managing AppArmor Profiles**:

```sh
# Disable a profile
sudo aa-disable /path/to/profile

# Enable a profile
sudo aa-enforce /path/to/profile
```

### Configuring AppArmor

- **Edit AppArmor Profiles**:

```sh
sudo nano /etc/apparmor.d/usr.bin.your_application
```

## 9.10 Security Best Practices

### Regular Updates

- **Keep the system and software up to date** to patch vulnerabilities.

```sh
sudo apt-get update && sudo apt-get upgrade
```

### Strong Passwords

- **Use strong, unique passwords** for all user accounts.

### Minimal Privileges

- **Follow the principle of least privilege**: Only grant users the permissions they need.

### Regular Audits

- **Conduct regular security audits** to identify and fix security issues.

### Use of Security Tools

- **Utilize security tools** such as `fail2ban`, `rkhunter`, and `clamav` to enhance security.

```sh
# Install and configure fail2ban
sudo apt-get install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

## Conclusion

Understanding Linux security and permissions is crucial for system administrators. This knowledge helps ensure that systems are secure from unauthorized access and that users have the appropriate permissions to perform their tasks. Mastering these concepts will significantly improve your ability to manage and secure Linux systems.
