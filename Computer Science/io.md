Input/Output (I/O) operations, at a high level, are anything that involves reading or writing data. They typically require communication with external resources or devices (anything that is not happening directly in the CPU), such as file read/writes and network requests.

I/O implementations typically have clean and easy-to-use interfaces. In [[Unix]]-based systems, they are typically integrated as virtual [[file systems]]. However, because of the hardware cooperation necessary to perform I/O operations, they are typically extremely difficult to implement.

Types of I/O Devices:
- **Character devices**: access data as a character stream (i.e. data not addressable)
- **Block devices**: access data in fixed-sized blocks (i.e. data is addressable)
	- Enables seeks and random accesses
- **Network devices**: have a separate interface for [[network]] purposes
In order for a computer to interact with a specific type of device, the OS must implement **device drivers**, which are a special type of software that allows the OS kernel to interact with hardware devices.

Device interfaces can have various timing mechanisms as well.
- **Synchronous**: also known as *blocking* interfaces, these devices wait until an I/O request is fulfilled
- **Non-blocking**: return quickly from a request without waiting
	- Polling, interrupts, signals, spinning
	- **Asynchronous**: allow for other processing to continue without waiting

### blocking interfaces
Calling an API that requests data from IO will cause the running thread to **block**---i.e. it is waiting until the requested data has returned to the caller. 

When a thread is blocked in Linux, it will be put in a **sleep** state by the [[operating system#the os kernel|kernel]] until data has returned to the caller. Threads in sleep state immediately give up its access to the CPU, so to not waste CPU time. After IO is ready, the thread is taken out of the Sleep state and put in Runnable state.
## non-blocking interfaces
Non-blocking I/O is an event-based [[parallelism]] model that initiates I/O tasks and immediately continues execution of other tasks without waiting for the task to complete. This type of model is necessary for **I/O-bound** applications, which may spend a lot of time waiting on external resources. 

The **event loop** is the core of non-blocking interfaces, responsible for managing coroutines. It is a [[scheduling|scheduler]] that runs in a single thread and switches between async tasks when they perform non-blocking I/O.
- Managing concurrency with event loops generally needs fewer threads to handle the same number of requests compared to **thread-per-request** or **thread-per-connection** models
- Executing an I/O request on a non-blocking API will return immediately, providing a `Promise` or state data structure which can accept a **callback** to update when the data is ready.
#### asyncio
While [[threads#multithreading|multi-threading]] is one solution for I/O-bound tasks, because of the Python GIL it can still be suboptimal for high-concurrency I/O tasks. `asyncio` is a Python standard library that enables scalable concurrency while still running in a single thread (i.e. bad for CPU-bound tasks) through two main operations:
- `async`: the `async` keyword is used before the normal function header for defining asynchronous functions, also known as **coroutines**, allowing for non-blocking I/O operations
- `await`: the `await` keyword pauses coroutines without blocking the event loop, allowing other tasks to run during I/O waits.