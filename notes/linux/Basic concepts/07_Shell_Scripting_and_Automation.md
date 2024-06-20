
# Shell Scripting and Automation

## 7.1 Introduction to Shell Scripting

- **Shell**: A command-line interface used to interact with the operating system.
- **Shell Scripting**: Writing scripts using shell commands to automate tasks.

### Common Shells

- **Bash (Bourne Again SHell)**: The most widely used shell in Linux.
- **Zsh (Z Shell)**: An extended version of Bash with more features.
- **Sh (Bourne Shell)**: The original Unix shell.
- **Ksh (Korn Shell)**: A shell with scripting capabilities similar to Bash.

## 7.2 Basic Shell Scripting Concepts

### Shebang

- **Shebang (`#!`)**: Specifies the interpreter to be used for the script.
  
```sh
#!/bin/bash
```

### Variables

- **Defining Variables**: Assigning values to variables.

```sh
#!/bin/bash
name="John Doe"
echo "Hello, $name"
```

- **Environment Variables**: Variables that are available system-wide.

```sh
#!/bin/bash
echo "Home directory: $HOME"
```

### Comments

- **Single-line Comments**: Use `#` for comments.

```sh
# This is a comment
```

### Basic Commands

- **echo**: Prints text to the terminal.

```sh
echo "Hello, World!"
```

- **read**: Reads input from the user.

```sh
echo "Enter your name: "
read name
echo "Hello, $name"
```

### Control Structures

#### Conditional Statements

- **if-else**: Executes commands based on conditions.

```sh
#!/bin/bash
if [ $1 -gt 10 ]
then
    echo "The number is greater than 10."
else
    echo "The number is 10 or less."
fi
```

- **elif**: Adds more conditions.

```sh
#!/bin/bash
if [ $1 -gt 10 ]
then
    echo "Greater than 10."
elif [ $1 -eq 10 ]
then
    echo "Equal to 10."
else
    echo "Less than 10."
fi
```

#### Loops

- **for loop**: Iterates over a list of items.

```sh
#!/bin/bash
for i in 1 2 3 4 5
do
    echo "Number: $i"
done
```

- **while loop**: Repeats commands as long as a condition is true.

```sh
#!/bin/bash
count=1
while [ $count -le 5 ]
do
    echo "Count: $count"
    ((count++))
done
```

- **until loop**: Repeats commands until a condition is true.

```sh
#!/bin/bash
count=1
until [ $count -gt 5 ]
do
    echo "Count: $count"
    ((count++))
done
```

### Functions

- **Defining Functions**: Creating reusable blocks of code.

```sh
#!/bin/bash
greet() {
    echo "Hello, $1"
}
greet "World"
```

### Exit Status

- **Exit Status**: Indicates the success or failure of a command.

```sh
#!/bin/bash
if [ -f /etc/passwd ]
then
    echo "File exists."
    exit 0
else
    echo "File does not exist."
    exit 1
fi
```

## 7.3 Advanced Shell Scripting Concepts

### Arrays

- **Defining Arrays**: Storing multiple values in a single variable.

```sh
#!/bin/bash
fruits=("Apple" "Banana" "Cherry")
echo "First fruit: ${fruits[0]}"
echo "All fruits: ${fruits[@]}"
```

### String Manipulation

- **Extracting Substrings**: Using parameter expansion.

```sh
#!/bin/bash
text="Hello, World!"
echo ${text:7:5}  # Output: World
```

- **Replacing Substrings**: Using parameter expansion.

```sh
#!/bin/bash
text="Hello, World!"
echo ${text/World/Universe}  # Output: Hello, Universe!
```

### File Operations

- **Reading Files**: Using `while` loop.

```sh
#!/bin/bash
while IFS= read -r line
do
    echo $line
done < "file.txt"
```

- **Writing to Files**: Using redirection.

```sh
#!/bin/bash
echo "This is a line." > file.txt
```

### Process Management

- **Starting Background Processes**: Using `&`.

```sh
#!/bin/bash
sleep 10 &
echo "Background process started."
```

- **Killing Processes**: Using `kill`.

```sh
#!/bin/bash
kill 1234  # Kills process with PID 1234
```

### Signal Handling

- **Trapping Signals**: Using `trap`.

```sh
#!/bin/bash
trap "echo 'Signal received!'" SIGINT
while :
do
    sleep 1
done
```

## 7.4 Automation with Shell Scripts

### Scheduled Tasks

- **cron Jobs**: Scheduling recurring tasks.

```sh
# Edit the crontab file
crontab -e

# Add a job to run a script every day at 2 AM
0 2 * * * /path/to/script.sh
```

- **at Jobs**: Scheduling one-time tasks.

```sh
# Schedule a job to run at a specific time
echo "/path/to/script.sh" | at 14:00
```

### Configuration Management

- **Environment Setup**: Automating environment setup tasks.

```sh
#!/bin/bash
# Update package lists
sudo apt update

# Install necessary packages
sudo apt install -y git vim

# Set environment variables
export MY_VAR="value"
```

### Backup and Recovery

- **Automating Backups**: Using tar for backups.

```sh
#!/bin/bash
tar -czvf backup.tar.gz /path/to/directory
```

### Network Automation

- **Configuring Network Interfaces**: Automating network configuration.

```sh
#!/bin/bash
ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up
```

### Monitoring and Alerts

- **System Monitoring**: Automating system health checks.

```sh
#!/bin/bash
# Check disk usage
disk_usage=$(df -h | grep '/dev/sda1' | awk '{print $5}')
echo "Disk usage: $disk_usage"
```

## 7.5 Best Practices for Shell Scripting

- **Use Comments**: Document your code.
- **Handle Errors**: Check exit statuses and handle errors gracefully.
- **Use Functions**: Modularize your code using functions.
- **Follow Naming Conventions**: Use meaningful variable and function names.
- **Secure Scripting**: Avoid using hardcoded credentials, validate inputs.

```sh
#!/bin/bash
# Example of handling errors
copy_file() {
    if cp "$1" "$2"; then
        echo "File copied successfully."
    else
        echo "Error copying file."
        return 1
    fi
}

# Usage
copy_file source.txt destination.txt
```

## Conclusion

Understanding shell scripting and automation is essential for managing and automating tasks in a Linux environment. This knowledge will enable you to write efficient scripts to automate routine tasks, manage system configurations, and enhance your productivity.

