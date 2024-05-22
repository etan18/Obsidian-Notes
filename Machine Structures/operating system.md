#cs162

The **operating system** is a special layer of software that provides application-level software access to hardware resources.
## virtualizing the machine

The heart of [[systems design]] provides clean, easy-to-use abstractions of physical resources. Operating systems are no different, with a lot of its primary function being to abstract away at the machine hardware to make it easier for programs to interface with. There are a few ways the OS virtualizes the machine.

#### complexity
The OS abstracts underlying hardware to help tame the complexity of the machine. Common abstractions we see include
- Processor -> thread
- Memory -> address space
- Disks, SSDs -> files
- Networks -> sockets
- Machines -> processes

>[!info] Next: Four Fundamental Concepts of OS
>The four fundamental concepts of OS are [[threads]], [[processes]], address spaces, and protection (see below).


---
# protection

Both the OS and the hardware need to have built-in protections to ensure safety when executing programs. These include preserving
- **Reliability**: don't crash
- **Security**: limit the scope of what threads can do
- **Privacy**: limit each thread to the data its able to access
- **Fairness**: each thread should be limited to its appropriate share of system resources (CPU time, memory, I/O, etc.)
Additionally, the OS must ensure **isolation** between threads, such that threads owned by different users cannot impact each other.
### the os kernel
The **kernel** is the single program at the core of every operating system that is running at all times. (NOT to be confused with [[kernels]]).

The kernel has its own *kernel stack*, which is separately from the user stack. This means that all processes have these two independent stacks. The kernel can access the user stack, but it cannot trust the user stack.

The kernel represents [[processes]] using a **process control block**, or PCB. 
##### dual mode operation
The hardware provides at least two modes (1 mode bit):
1. Kernel, or supervisor, mode
2. User mode
Certain operationsn and privileged instructions are prohibited when running in user mode, such as changing the page table pointer, disabling interrupts, or interacting directly with hardware.
##### kernel mode transfer
There are three types of kernel mode transfer, which trigger a toggle between the two modes:
- **Syscall**: calls to functions that exist outside of the process
	- These are safely administered through well-defined syscall entry points, or handlers.
- **Interrupt**: external asynchronous events trigger a context switch, save the current execution state and jump to a kernel interrupt handler.
- **Trap or exception**: If a process triggers an internal hardware event, typically caused by undesired behavior, then execution stops and control is transferred to an exception handler in the kernel to allow the system to continue operating normally.
	- Some examples include segfaults, read/write access violations, and divide by zero errors.

---
## i/o

I/O implementations typically have clean and easy-to-use interfaces. However, because of the hardware cooperation necessary to perform I/O operations, they are typically extremely difficult to implement.

Types of I/O Devices:
- **Character devices**: access data as a character stream (i.e. data not addressable)
- **Block devices**: access data in fixed-sized blocks (i.e. data is addressable)
- **Network devices**: have a separate interface for [[network]] purposes

Device interfaces can have various timing mechanisms as well.
- **Synchronous**: also known as *blocking* interfaces, these devices wait until an I/O request is fulfilled
- **Non-blocking**: return quickly from a request without waiting
- **Asynchronous**: allow for other processing to continue without waiting