#cs162 

**Processes** are an abstract execution environment representing a single instance of a running program. This provides a cleaner interface for the program instead of just communicating with raw hardware.

Processes are provided by the [[operating system]], and contain several vital elements:
- **Virtual [[threads]]**
- **Protected address space**
- **System states** associated with threads (e.g. files)
Each element emulates some piece of machine hardware. 
### protection
One of the four main elements of an OS is [[operating system|protection]]. The process is one of the main protection handlers.

>[!tip] Isolation
>Processes provide **isolation** between programs, creating the illusion that each process can use all of the machine's compute power at all times, which is not actually the case.

Processes provide **reliability** to the system such that bugs can only overwrite memory of the process they're currently in. **Applications** are further abstractions wherein one or more processes are working together.

### multithreading
Allowing multiple threads to run on the same process introduces many optimizations and conveniences for running programs.

Multi-threading introduces **[[parallelism]]** such that we can take advantage of the computational power available in the machine.

---
# managing processes

Everything outside of the kernel is running in a process. Trickily, processes are created and managed by other processes. The first `init` process is created by the kernel on boot-up.
### process control block
The kernel represents processes with a PCB, or process control block.

### lifecycle
As a process executes, it changes between various states:
1. **New**: the process is being created
2. **Ready**: the process is waiting to run
3. **Running**: instructions are being executed
4. **Waiting**: the process is waiting for some event to occur (e.g. I/O or event completion)
5. **Terminated**: the process has finished execution

## inter-process communication
**Inter-process communication** (IPC) provides mechanism for processes to communicate and manage shared data.
### pipes

### sockets
Two-way communication channels between processes. There are three main types of sockets: client, server, and connection sockets.
- Uses two queues, one in each direction
