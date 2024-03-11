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
## synchronization
Concurrency with threads is *non-deterministic* in nature. The OS [[scheduling|scheduler]] can run threads in any order, and switch between threads at any time. This means that the OS must ensure that the correct behavior is achieved every time *by design*.

**Synchronization** enables the cooperation of multiple threads. 

>[!pencil] Atomic Operations
>Synchronization is made possible via atomic operations. These are methods which are guaranteed to always run to completion or not run at all. These are indivisible operations (commonly, loads and stores are atomic).

**Mutual exclusion** is a basic method for synchronization that uses *locks*. This method ensures that only a single thread is performing an action at any given time. 
- Only one thread can "hold" the lock at any time. Before performing an action, check if the lock is available and acquire it.
- Perform the action. This part is known as the **critical section**.
- Return the lock upon completion of the action.
##### condition variables
**Busy waiting**, or *spinlocking*, is a naive synchronization method that relies on atomic loads and stores to continuously check if a thread can proceed execution.
```
// Thread A


// Thread B

```

This technique burns CPU cycles and makes it such that the waiting thread cannot execute other tasks in the meantime.

**Condition variables** is another synchronization method which implements a queue of threads which are all waiting to access some critical section. They go a step beyond solely providing mutual exclusion—they also allow threads to atomically sleep *inside* the critical section until some waking condition is met.
- **`wait(condition, lock)`**: release lock, put thread to sleep until condition is signaled; when thread wakes up again, re-acquire lock before returning.
- **`signal(condition, lock)`**: if any threads are waiting on condition, wake up one of them. Caller must hold lock, which must be the same as the lock used in the wait call.
- **`broadcast(condition, lock)`**: same as signal, except wake up all waiting threads.
### semaphores
Semaphores are essentially integer variables used to ensure synchronization. They were introduced by Dijkstra in the 1960s, and they have two primary atomic operations:
- **Down/Wait/P**: waits for semaphore’s value to become strictly positive, then decrements it by 1.
- **Up/Post/V**: increments the value of the semaphore by 1.
Semaphores can be used as locks (init to $1$, down to acquire, up to release). 

Another semaphore workflow allows it to act as a [[scheduling]] constraint, where one thread needs to wait for another thread to terminate.
1. Initialize the semaphore to $0$
2. Waiting thread downs the semaphore (goes to sleep)
3. The current thread ups the semaphore (waking the other thread) when it finishes execution.
### monitors
Monitors compose of a lock and zero or more condition variables. Monitors represent a higher-level abstraction of the synchronization logic of the program. 
```
// Basic structure of MESA MONITOR program
acquire(&lock);
while (waiting condition) {
	cond_var.wait();
}
release(&lock);

// Do stuff in non-critical section

// Wake waiting thread in queue
acquire(&lock);
cond_var.signal()
release(&lock);

```