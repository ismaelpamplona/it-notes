# 12. Device Drivers and Modules

## 12.1 Introduction to Device Drivers

- **Device Drivers**: Software components that allow the operating system to communicate with hardware devices.
- **Kernel Modules**: Loadable pieces of code that can be added or removed from the kernel at runtime.

### Key Concepts

- **Kernel Space**: The memory area where the kernel executes and provides its services.
- **User Space**: The memory area where user applications run.

## 12.2 Types of Device Drivers

### 1. Character Device Drivers

- **Character Devices**: Devices that are accessed as a stream of bytes (e.g., keyboards, serial ports).
- **Examples**: `/dev/ttyS0` (serial port), `/dev/null`.

### 2. Block Device Drivers

- **Block Devices**: Devices that are accessed as blocks of data (e.g., hard drives, SSDs).
- **Examples**: `/dev/sda` (first SCSI disk), `/dev/loop0` (loopback device).

### 3. Network Device Drivers

- **Network Devices**: Devices that handle network communication (e.g., Ethernet cards, Wi-Fi adapters).
- **Examples**: `eth0` (first Ethernet interface), `wlan0` (first wireless interface).

## 12.3 Kernel Modules

### Introduction to Kernel Modules

- **Loadable Kernel Modules (LKMs)**: Modules that can be loaded or unloaded into the kernel at runtime.
- **Advantages**: Flexibility, reduced memory usage, easier debugging.

### Managing Kernel Modules

#### Loading a Module

- **insmod**: Insert a module into the kernel.

```sh
sudo insmod module_name.ko
```

- **modprobe**: Load a module and its dependencies.

```sh
sudo modprobe module_name
```

#### Unloading a Module

- **rmmod**: Remove a module from the kernel.

```sh
sudo rmmod module_name
```

- **modprobe -r**: Remove a module and its dependencies.

```sh
sudo modprobe -r module_name
```

#### Listing Loaded Modules

- **lsmod**: List all currently loaded modules.

```sh
lsmod
```

### Module Information

- **modinfo**: Display information about a kernel module.

```sh
modinfo module_name
```

## 12.4 Writing Device Drivers

### Basic Structure of a Device Driver

1. **Initialization Function**: Called when the module is loaded.
2. **Exit Function**: Called when the module is unloaded.
3. **File Operations Structure**: Defines the functions that handle file operations (e.g., open, read, write).

### Example: Simple Character Device Driver

```c
#include <linux/module.h>
#include <linux/fs.h>
#include <linux/uaccess.h>

#define DEVICE_NAME "simple_char_dev"
#define BUF_LEN 80

static int device_open(struct inode *, struct file *);
static int device_release(struct inode *, struct file *);
static ssize_t device_read(struct file *, char __user *, size_t, loff_t *);
static ssize_t device_write(struct file *, const char __user *, size_t, loff_t *);

static int major;
static char msg[BUF_LEN];
static int msg_len;

static struct file_operations fops = {
    .read = device_read,
    .write = device_write,
    .open = device_open,
    .release = device_release
};

static int __init simple_char_dev_init(void) {
    major = register_chrdev(0, DEVICE_NAME, &fops);
    if (major < 0) {
        printk(KERN_ALERT "Registering char device failed with %d
", major);
        return major;
    }
    printk(KERN_INFO "I was assigned major number %d. To talk to
", major);
    return 0;
}

static void __exit simple_char_dev_exit(void) {
    unregister_chrdev(major, DEVICE_NAME);
    printk(KERN_INFO "Goodbye, world!
");
}

static int device_open(struct inode *inode, struct file *file) {
    return 0;
}

static int device_release(struct inode *inode, struct file *file) {
    return 0;
}

static ssize_t device_read(struct file *filp, char __user *buffer, size_t length, loff_t * offset) {
    int bytes_read = 0;
    if (*msg == 0) return 0;
    while (length && *msg) {
        put_user(*(msg++), buffer++);
        length--;
        bytes_read++;
    }
    return bytes_read;
}

static ssize_t device_write(struct file *filp, const char __user *buffer, size_t length, loff_t * off) {
    return -EINVAL;
}

module_init(simple_char_dev_init);
module_exit(simple_char_dev_exit);

MODULE_LICENSE("GPL");
MODULE_DESCRIPTION("Simple Character Device Driver");
MODULE_AUTHOR("Your Name");
```

### Compiling and Loading the Driver

1. **Create a Makefile**:

```makefile
obj-m += simple_char_dev.o

all:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

2. **Compile the Module**:

```sh
make
```

3. **Load the Module**:

```sh
sudo insmod simple_char_dev.ko
```

4. **Create a Device Node**:

```sh
sudo mknod /dev/simple_char_dev c <major_number> 0
```

5. **Interact with the Device**:

```sh
echo "Hello, World!" > /dev/simple_char_dev
cat /dev/simple_char_dev
```

## 12.5 Kernel Module Parameters

- **Module Parameters**: Allow parameters to be passed to a kernel module at load time.

### Example: Module Parameters

```c
#include <linux/module.h>
#include <linux/moduleparam.h>

static int param = 0;
module_param(param, int, 0);
MODULE_PARM_DESC(param, "An integer parameter");

static int __init param_init(void) {
    printk(KERN_INFO "Parameter value: %d
", param);
    return 0;
}

static void __exit param_exit(void) {
    printk(KERN_INFO "Goodbye, world!
");
}

module_init(param_init);
module_exit(param_exit);

MODULE_LICENSE("GPL");
MODULE_DESCRIPTION("Module with Parameters");
MODULE_AUTHOR("Your Name");
```

### Loading Module with Parameters

```sh
sudo insmod module_param.ko param=42
```

## 12.6 Debugging and Logging

### Kernel Logging

- **printk**: Kernel logging function.

```c
printk(KERN_INFO "Hello, Kernel!
");
```

### Viewing Kernel Logs

- **dmesg**: View the kernel ring buffer.

```sh
dmesg
```

- **/var/log/kern.log**: Kernel log file.

```sh
cat /var/log/kern.log
```

### Debugging Tools

- **gdb**: GNU Debugger.
- **kgdb**: Kernel GNU Debugger.
- **ftrace**: Function Tracer.

## 12.7 Best Practices for Writing Device Drivers

- **Follow Coding Standards**: Maintain readability and consistency.
- **Handle Errors Gracefully**: Ensure robust error handling.
- **Minimize Kernel Footprint**: Keep the code efficient and lightweight.
- **Documentation**: Document the code and provide usage instructions.
- **Testing**: Thoroughly test the driver in different scenarios.

## Conclusion

Understanding device drivers and kernel modules is crucial for interacting with hardware in Linux. This knowledge allows you to write, load, and manage drivers effectively. Mastery of these concepts will significantly improve your ability to develop and troubleshoot device drivers in Linux.
