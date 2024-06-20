
# Essential Linux Commands

## File and Directory Operations

- **ls**: List directory contents.
  ```sh
  ls -l
  ```

- **cd**: Change directory.
  ```sh
  cd /path/to/directory
  ```

- **pwd**: Print working directory.
  ```sh
  pwd
  ```

- **mkdir**: Create a directory.
  ```sh
  mkdir new_directory
  ```

- **rmdir**: Remove an empty directory.
  ```sh
  rmdir directory_name
  ```

- **cp**: Copy files or directories.
  ```sh
  cp source_file destination_file
  cp -r source_directory destination_directory
  ```

- **mv**: Move or rename files or directories.
  ```sh
  mv old_name new_name
  mv file /new/path/
  ```

- **rm**: Remove files or directories.
  ```sh
  rm file_name
  rm -r directory_name
  ```

- **touch**: Create an empty file or update the timestamp.
  ```sh
  touch new_file
  ```

- **find**: Search for files in a directory hierarchy.
  ```sh
  find /path/to/search -name "file_name"
  ```

- **locate**: Find files by name.
  ```sh
  locate file_name
  ```

- **du**: Estimate file space usage.
  ```sh
  du -sh /path/to/directory
  ```

- **df**: Report file system disk space usage.
  ```sh
  df -h
  ```

## File Content Operations

- **cat**: Concatenate and display file content.
  ```sh
  cat file_name
  ```

- **more/less**: View file content one page at a time.
  ```sh
  less file_name
  more file_name
  ```

- **head**: Output the first part of files.
  ```sh
  head -n 10 file_name
  ```

- **tail**: Output the last part of files.
  ```sh
  tail -n 10 file_name
  ```

- **grep**: Search for patterns in files.
  ```sh
  grep "pattern" file_name
  ```

- **sed**: Stream editor for filtering and transforming text.
  ```sh
  sed 's/old/new/g' file_name
  ```

- **awk**: Pattern scanning and processing language.
  ```sh
  awk '{print $1}' file_name
  ```

## System Information

- **uname**: Print system information.
  ```sh
  uname -a
  ```

- **top**: Display tasks and system resource usage.
  ```sh
  top
  ```

- **htop**: Interactive process viewer.
  ```sh
  htop
  ```

- **ps**: Report a snapshot of current processes.
  ```sh
  ps aux
  ```

- **free**: Display amount of free and used memory in the system.
  ```sh
  free -h
  ```

- **uptime**: Tell how long the system has been running.
  ```sh
  uptime
  ```

- **hostname**: Show or set the system's hostname.
  ```sh
  hostname
  ```

- **dmesg**: Print or control the kernel ring buffer.
  ```sh
  dmesg
  ```

## User Management

- **whoami**: Print the current user name.
  ```sh
  whoami
  ```

- **id**: Print user and group information.
  ```sh
  id
  ```

- **useradd**: Create a new user.
  ```sh
  sudo useradd new_user
  ```

- **passwd**: Change user password.
  ```sh
  sudo passwd user_name
  ```

- **usermod**: Modify a user account.
  ```sh
  sudo usermod -aG group_name user_name
  ```

- **userdel**: Delete a user account.
  ```sh
  sudo userdel user_name
  ```

- **groupadd**: Create a new group.
  ```sh
  sudo groupadd group_name
  ```

- **groupdel**: Delete a group.
  ```sh
  sudo groupdel group_name
  ```

## Network Management

- **ifconfig**: Configure network interfaces.
  ```sh
  ifconfig
  ```

- **ip**: Show/manipulate routing, devices, policy routing, and tunnels.
  ```sh
  ip addr show
  ```

- **ping**: Send ICMP ECHO_REQUEST to network hosts.
  ```sh
  ping google.com
  ```

- **netstat**: Print network connections, routing tables, interface statistics.
  ```sh
  netstat -tuln
  ```

- **ss**: Another utility to investigate sockets.
  ```sh
  ss -tuln
  ```

- **traceroute**: Print the route packets take to a network host.
  ```sh
  traceroute google.com
  ```

- **wget**: Non-interactive network downloader.
  ```sh
  wget http://example.com/file
  ```

- **curl**: Transfer data from or to a server.
  ```sh
  curl http://example.com
  ```

## Package Management

### APT (Debian-based systems)

- **Update package lists**:
  ```sh
  sudo apt-get update
  ```

- **Upgrade packages**:
  ```sh
  sudo apt-get upgrade
  ```

- **Install a package**:
  ```sh
  sudo apt-get install package_name
  ```

- **Remove a package**:
  ```sh
  sudo apt-get remove package_name
  ```

### YUM/DNF (Red Hat-based systems)

- **Update package lists**:
  ```sh
  sudo yum update
  ```

  ```sh
  sudo dnf update
  ```

- **Install a package**:
  ```sh
  sudo yum install package_name
  ```

  ```sh
  sudo dnf install package_name
  ```

- **Remove a package**:
  ```sh
  sudo yum remove package_name
  ```

  ```sh
  sudo dnf remove package_name
  ```

## Disk Management

- **fdisk**: Partition table manipulator for Linux.
  ```sh
  sudo fdisk -l
  ```

- **mkfs**: Build a Linux file system.
  ```sh
  sudo mkfs -t ext4 /dev/sdx1
  ```

- **mount**: Mount a file system.
  ```sh
  sudo mount /dev/sdx1 /mnt
  ```

- **umount**: Unmount a file system.
  ```sh
  sudo umount /mnt
  ```

- **df**: Report file system disk space usage.
  ```sh
  df -h
  ```

- **du**: Estimate file space usage.
  ```sh
  du -sh /path/to/directory
  ```

## System Monitoring and Performance

- **top**: Display Linux tasks.
  ```sh
  top
  ```

- **htop**: Interactive process viewer.
  ```sh
  htop
  ```

- **vmstat**: Report virtual memory statistics.
  ```sh
  vmstat
  ```

- **iostat**: Report CPU and input/output statistics.
  ```sh
  iostat
  ```

- **mpstat**: Report processors related statistics.
  ```sh
  mpstat
  ```

## Security and Permissions

- **chmod**: Change file access permissions.
  ```sh
  chmod 755 file_name
  ```

- **chown**: Change file owner and group.
  ```sh
  chown user:group file_name
  ```

- **passwd**: Update user's password.
  ```sh
  sudo passwd user_name
  ```

## Automation and Scripting

- **cron**: Schedule commands to run at specified times.
  ```sh
  crontab -e
  ```

- **at**: Schedule a command to run once at a particular time.
  ```sh
  at 10:00
  ```

- **bash**: GNU Bourne-Again SHell.
  ```sh
  #!/bin/bash
  ```

## Conclusion

These commands cover a wide range of tasks that a Linux server administrator and a heavy user might need to perform. Mastering these commands will help you effectively manage and troubleshoot your Linux systems.
