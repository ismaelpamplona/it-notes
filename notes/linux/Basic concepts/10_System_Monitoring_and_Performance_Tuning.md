# 10. System Monitoring and Performance Tuning

## 10.1 Introduction to System Monitoring

- **System Monitoring**: The process of continuously checking and tracking system performance and resource usage.
- **Performance Tuning**: The process of adjusting system parameters to optimize performance.

### Key Concepts

- **Resource Utilization**: Tracking CPU, memory, disk, and network usage.
- **Bottlenecks**: Identifying points in the system that limit performance.
- **Proactive Monitoring**: Regularly monitoring to prevent issues.
- **Reactive Monitoring**: Addressing issues as they arise.

## 10.2 Monitoring Tools

### top and htop

- **top**: Displays real-time system information, including processes and resource usage.

```sh
top
```

- **htop**: An interactive version of `top` with a more user-friendly interface.

```sh
htop
```

### ps and pstree

- **ps**: Reports a snapshot of current processes.

```sh
ps aux
```

- **pstree**: Displays processes in a tree format.

```sh
pstree
```

### free

- **free**: Displays amount of free and used memory in the system.

```sh
free -h
```

### vmstat

- **vmstat**: Reports virtual memory statistics.

```sh
vmstat 5
```

### iostat

- **iostat**: Reports CPU and input/output statistics for devices and partitions.

```sh
iostat -x 5
```

### mpstat

- **mpstat**: Reports CPU usage by individual processors.

```sh
mpstat -P ALL 5
```

### netstat and ss

- **netstat**: Prints network connections, routing tables, interface statistics.

```sh
netstat -tuln
```

- **ss**: Investigates sockets.

```sh
ss -tuln
```

### iftop

- **iftop**: Displays bandwidth usage on an interface by host.

```sh
sudo iftop -i eth0
```

### nload

- **nload**: Monitors network traffic and bandwidth usage in real time.

```sh
sudo nload
```

### sar

- **sar**: Collects, reports, and saves system activity information.

```sh
sar -u 5
```

### dstat

- **dstat**: Combines information from vmstat, iostat, netstat, and ifstat.

```sh
dstat
```

### glances

- **glances**: An advanced, real-time system monitoring tool.

```sh
glances
```

## 10.3 Performance Tuning

### CPU Performance Tuning

- **CPU Affinity**: Binding processes to specific CPUs to optimize performance.

```sh
taskset -c 0,1 <command>
```

- **nice and renice**: Adjusting process priority.

```sh
nice -n 10 <command>
renice -n 10 -p <pid>
```

### Memory Performance Tuning

- **Swappiness**: Adjusting the kernel's tendency to swap.

```sh
# Check current swappiness value
cat /proc/sys/vm/swappiness

# Set swappiness value
sudo sysctl vm.swappiness=10
```

- **HugePages**: Using large memory pages to improve performance.

```sh
# Enable HugePages
sudo sysctl -w vm.nr_hugepages=128
```

### Disk Performance Tuning

- **I/O Scheduler**: Changing the I/O scheduler to optimize disk performance.

```sh
# Check current I/O scheduler
cat /sys/block/sda/queue/scheduler

# Set I/O scheduler
echo cfq | sudo tee /sys/block/sda/queue/scheduler
```

- **Filesystem Tuning**: Optimizing filesystem performance.

```sh
# Mount with noatime option to reduce disk writes
sudo mount -o remount,noatime /dev/sda1 /
```

### Network Performance Tuning

- **TCP Tuning**: Adjusting TCP settings for better network performance.

```sh
# Increase maximum buffer sizes
sudo sysctl -w net.core.rmem_max=16777216
sudo sysctl -w net.core.wmem_max=16777216

# Enable TCP window scaling
sudo sysctl -w net.ipv4.tcp_window_scaling=1
```

- **NIC Offloading**: Offloading certain tasks to the network interface card (NIC).

```sh
# Enable/disable offloading features
sudo ethtool -K eth0 tso off
```

## 10.4 Monitoring and Tuning Best Practices

### Regular Monitoring

- **Set up regular monitoring** to proactively detect and address issues.
- **Use monitoring tools** like `nagios`, `zabbix`, or `prometheus` for continuous monitoring.

### Baseline Performance

- **Establish a performance baseline** to understand normal performance levels.
- **Compare current performance** against the baseline to identify anomalies.

### Resource Allocation

- **Allocate resources appropriately** based on the workload requirements.
- **Use cgroups** to limit resource usage by groups of processes.

```sh
# Create a cgroup and limit memory usage
sudo cgcreate -g memory:/mygroup
echo 512M | sudo tee /sys/fs/cgroup/memory/mygroup/memory.limit_in_bytes
sudo cgexec -g memory:/mygroup <command>
```

### Load Testing

- **Perform load testing** to identify performance bottlenecks and optimize accordingly.
- **Use tools** like `apachebench` or `JMeter` for load testing.

### Documentation and Automation

- **Document performance tuning changes** for future reference.
- **Automate performance tuning tasks** where possible to ensure consistency.

## Conclusion

Understanding system monitoring and performance tuning is crucial for maintaining and optimizing system performance. Regular monitoring, proactive tuning, and following best practices will help ensure that systems run efficiently and effectively. Mastery of these concepts will significantly improve your ability to manage and optimize Linux systems.
