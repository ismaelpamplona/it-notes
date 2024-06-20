# 4. Process Management and Scheduling

## Introduction

Process management and scheduling are critical components of the Linux operating system. They ensure that system resources are allocated efficiently and processes are executed in a manner that maximizes performance and responsiveness.

## Process Management

### Definition

A process is an instance of a running program. It includes the program code, its current activity, and the state of its execution.

### Process States

Processes can be in one of several states:

- **Running**: The process is actively executing on a CPU.
- **Waiting**: The process is waiting for some event (e.g., I/O completion) to occur.
- **Stopped**: The process has been stopped, usually by receiving a signal.
- **Zombie**: The process has finished execution but still has an entry in the process table.

### Process Lifecycle

1. **Creation**: Processes are created using the `fork()` system call, which creates a new process by duplicating the calling process.
2. **Execution**: The new process can replace its memory space with a new program using `exec()`.
3. **Termination**: Processes terminate using the `exit()` system call. The parent process can retrieve the termination status using `wait()`.

### Process Control Block (PCB)

The PCB is a data structure in the kernel that contains information about a process, such as:

- Process ID (PID)
- Process state
- Program counter
- CPU registers
- Memory management information
- I/O status
- Accounting information

## Process Scheduling

### Definition

Process scheduling is the method by which the operating system decides which process runs at a given time. It aims to optimize CPU usage, response time, and system throughput.

### Scheduling Algorithms

1. **First-Come, First-Served (FCFS)**

   - Processes are scheduled in the order they arrive.
   - Simple but can lead to long waiting times.

2. **Shortest Job Next (SJN)**

   - Selects the process with the shortest expected execution time.
   - Can reduce average waiting time but requires knowledge of execution times.

3. **Priority Scheduling**

   - Processes are assigned priorities, and the highest priority process runs first.
   - Can lead to starvation of low-priority processes.

4. **Round Robin (RR)**

   - Each process is assigned a fixed time slice (quantum) in a cyclic order.
   - Fair and simple but can have high context switching overhead.

5. **Multilevel Queue Scheduling**

   - Processes are divided into different queues based on their priority or type.
   - Each queue can have its own scheduling algorithm.

6. **Multilevel Feedback Queue Scheduling**

   - Similar to multilevel queue scheduling but allows processes to move between queues based on their behavior.

7. **Completely Fair Scheduler (CFS)**
   - The default scheduler in Linux, which aims to divide CPU time fairly among running processes.
   - Uses a red-black tree to maintain processes and assigns each process a virtual runtime.

### Detailed Breakdown

#### Round Robin (RR) Scheduling

- **Concept**: Each process gets to run for a fixed time slice (quantum).
- **How It Works**: Processes are scheduled in a cyclic order. If a process doesn’t finish during its time slice, it is put back at the end of the queue.
- **Pros**: Fair, simple to implement.
- **Cons**: High context switching overhead if the quantum is too short.

#### Priority Scheduling

- **Concept**: Processes are assigned priorities, and the highest priority process runs first.
- **How It Works**: The scheduler selects the process with the highest priority. If two processes have the same priority, another scheduling algorithm (like FCFS) may be used.
- **Pros**: Ensures that important processes get more CPU time.
- **Cons**: Can lead to starvation of low-priority processes.

#### Completely Fair Scheduler (CFS)

- **Concept**: Divides CPU time fairly among running processes.
- **How It Works**: CFS maintains a red-black tree of processes, where each process is assigned a virtual runtime. The process with the smallest virtual runtime is chosen to run next.
- **Pros**: Fairness in scheduling, efficient handling of interactive processes.
- **Cons**: More complex to implement compared to simpler algorithms.

## Example of Process Creation and Scheduling

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();
    if (pid < 0) {
        perror("fork failed");
        return 1;
    }
    if (pid == 0) {
        // Child process
        printf("Child process: PID = %d\n", getpid());
        execlp("/bin/ls", "ls", NULL);
    } else {
        // Parent process
        printf("Parent process: PID = %d\n", getpid());
        wait(NULL);
        printf("Child process finished\n");
    }
    return 0;
}
```

## Detailed Breakdown

### Making a System Call

```mermaid
graph LR;
    A[User Space] -->|"fork()"| B[Kernel \n Space];
    B --> C[Create \n PCB];
    C --> D[Assign \n PID];
    D --> E[Return PID to \n User Space];
    E --> A;
```

- **User Space**: The parent process calls `fork()`.

- **Kernel Space**: The system call transitions from user space to kernel space.

- **Create PCB**: The kernel creates a new Process Control Block (PCB) for the child process.

- **Assign PID**: The kernel assigns a unique Process ID (PID) to the child process.

- **Return PID to User Space**:

  - The `fork()` call returns:
  - In the parent process: the PID of the child.
  - In the child process: 0.

- **User Space**: The parent and child processes continue execution with their respective return values from `fork()`.

### Context Switching

- **Definition**: The process of storing the state of a currently running process and restoring the state of the next process to run.
- **Components**: Save registers, program counter, and stack pointer of the current process; load registers, program counter, and stack pointer of the next process.

## Performance Considerations

- **Context Switching Overhead**: Switching between processes can be costly in terms of CPU cycles.
- **Quantum Size**: The size of the time slice in RR scheduling affects the responsiveness and overhead.
- **Starvation**: Ensuring that lower-priority processes get CPU time in priority scheduling.

## Summary

Understanding process management and scheduling is crucial for system performance and responsiveness. It involves knowing how processes are created, managed, and scheduled by the operating system. Mastery of these concepts will enable you to optimize system performance and prepare you well for your interview.
