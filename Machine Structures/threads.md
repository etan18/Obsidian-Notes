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

#### scheduling
There are a few POSIX built-in functions which allow for forced scheduling manipulation. 
- `sched_yield()`: calling thread relinquishes the CPU and is put at the end of the run queue
	- The order in which threads execute is now dependent on the scheduling algorithm
- `pthread_join(pthread_t thread)`: suspend execution of the calling thread until the target _thread_ terminates
	- This is better than `sched_yield` to better ensure the order of thread execution. 
	- Calling `pthread_create` without `pthread_join` is dangerous and can waste threads such that they are never run.
