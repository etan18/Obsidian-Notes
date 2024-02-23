#cs162 

A **thread** is one of the base concepts of an [[operating system]]. It encompasses all information needed for a single, unique execution context. Multi-threading is introduced by [[processes]] to be able to execute multiple sets of instructions at once.

A single thread executes on a processor, or core, when it is the **resident** in the processor registers. When a thread's state is not loaded into the processor, it is said to be *suspended*, and copies of the most recent state of that thread are stored in memory.

>[!info] Virtualizing the Core
>A thread is essentially a virtual core. Each thread mimics its own processor, then when it's actually being run on the hardware, multiple threads take turns on the same processor, but all of that is abstracted by the OS.

## elements
A thread consists of multiple elements that each provide some important context for the executing program.
1. **Program counter**: register pointing to the next instruction in memory (address space)
2. **Registers**: store intermediate values for ongoing computations--these can be literal values *or* pointers to values stored in memory
3. **Stack pointer**: holds the address at the top of the stack
Everything else is stored in memory.

---
# multithreading

A multi-threaded program allows a single application to run multiple threads which have shared states, allowing for both [[parallelism]] and data transfer between multiple threads. These are called *cooperating threads*. This is enabled by the fact that 
- Threads inside the same process are not isolated from one another
- Threads inside the same process share an address space and file descriptor table
### synchronization
Concurrency with threads is *non-deterministic* in nature. The OS [[scheduling|scheduler]] can run threads in any order, and switch between threads at any time. This means that the OS must ensure that the correct behavior is achieved every time *by design*.

**Synchronization** enables the cooperation of multiple threads. 

>[!pencil] Atomic Operations
>Synchronization is made possible via atomic operations. These are methods which are guaranteed to always run to completion or not run at all. These are indivisible operations (commonly, loads and stores are atomic).

**Mutual exclusion** is a basic method for synchronization that uses *locks*. This method ensures that only a single thread is performing an action at any given time. 
- Only one thread can "hold" the lock at any time. Before performing an action, check if the lock is available and acquire it.
- Perform the action. This part is known as the **critical section**.
- Return the lock upon completion of the action.
##### busy waiting
Busy waiting is a naive synchronization method that relies on atomic loads and stores to continuously check if a thread can proceed execution.
```
// Thread A


// Thread B

```

This technique burns CPU cycles and makes it such that the waiting thread cannot execute other tasks in the meantime.
##### semaphores
Semaphores are essentially integer variables used to ensure synchronization. They were introduced by Dijkstra in the 1960s, and they have two primary atomic operations:
- **Down/Wait/P**: waits for semaphore’s value to become strictly positive, then decrements it by 1.
- **Up/Post/V**: increments the value of the semaphore by 1.
Semaphores can be used as locks (down to acquire, up to release), or as a scheduling tool. 

### scheduling
There are a few POSIX built-in functions which allow for forced [[scheduling]] manipulation. 
- `sched_yield()`: calling thread relinquishes the CPU and is put at the end of the run queue
	- The order in which threads execute is now dependent on the scheduling algorithm
- `pthread_join(pthread_t thread)`: suspend execution of the calling thread until the target _thread_ terminates
	- This is better than `sched_yield` to better ensure the order of thread execution. 
	- Calling `pthread_create` without `pthread_join` is dangerous and can waste threads such that they are never run.