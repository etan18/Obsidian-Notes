#cs162 

**Processes** are an abstract execution environment representing a single instance of a running program. This provides a cleaner interface for the program instead of just communicating with raw hardware.

Processes are provided by the [[operating system]], and contain several vital elements:
- **Virtual [[threads]]**
- **Protected address space**
- **System states** associated with threads (e.g. file descriptor table)
Each element emulates some piece of machine hardware. 
## protection
One of the four main elements of an OS is [[operating system|protection]]. The process is one of the main protection handlers. The OS is in charge of
- Giving every process the illusion of running on a private CPU 
- Giving every process the illusion of running on private memory
- Managing resources to allocate to each process 
- Isolating processes from all other processes and protect OS

>[!tip] Isolation
>Processes provide **isolation** between programs, creating the illusion that each process can use all of the machine's compute power at all times, which is not actually the case.

Processes provide **reliability** to the system such that bugs can only overwrite memory of the process they're currently in. **Applications** are further abstractions wherein one or more processes are working together.

---
# managing processes

Everything outside of the kernel is running in a process. Trickily, processes are created and managed by other processes. The first `init` process is created by the kernel on boot-up.

Allowing multiple threads to run on the same process introduces many optimizations and conveniences for running programs.

### process control block
The kernel represents processes with a PCB, or process control block. The PCB stores metadata on the process state, such as
- PID
- Open files list
- Page table base register

### lifecycle
As a process executes, it changes between various states:
1. **New**: the process is being created
2. **Ready**: the process is waiting to run
3. **Running**: instructions are being executed
4. **Waiting**: the process is waiting for some event to occur (e.g. I/O or event completion)
5. **Terminated**: the process has finished execution

### inter-process communication
**Inter-process communication** (IPC) provides mechanism for processes to communicate and manage shared data.
#### pipes
One-way communication between two processes on the same physical machine—one process is *write*-only and the other is *read*-only. Pipes are allocated their own finite buffer space which is the intermediary for data transfer between processes.
- The OS blocks write actions when the pipe's buffer is *full*
- The OS blocks read actions when the pipe is *empty*
#### sockets
Two-way communication channels between any two processes. There are three main types of sockets: client, server, and connection sockets.
- Uses two [[queue|queues]], one in each direction
