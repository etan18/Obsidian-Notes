#cs61c #cs162 

Parallelism is a core topic in machine structures, dealing with managing many tasks across many cores or processes. **Concurrency** is the similar concept of managing multiple tasks at once to give the *illusion* that they are running simultaneously, even though they may all be taking turns on a single processor. This is managed 

Parallelism can occur at the 
- **Thread-level**: this is generally done by executing non-interfering *instruction sets* on different [[threads]] at the same time. [[threads#multithreading|Multi-threading]] is discussed in the threads page.
- **Process-level**: this page describes multi-processing.

>[!tip] Amdahl's Law
>The amount of instructions we can run in parallel is limited—some processes must be executed sequentially. This essentially bounds how efficient parallelizing can make our programs.

In general, our runtime is composed of three factors:
1. The number of instructions in the program
2. The number of cycles per instruction
3. The time of each cycle -> cannot be sped up, the absolute limit is the speed of light

At scale, Python tasks fall into two main bins:
- **I/O bound**: frequent operations like [[network]] requests, reading/writing to [[file systems]], or querying [[databases]], wherein the program is waiting for external resources
	- Solution: [[threads#multithreading|multithreading]], asyncio
- **CPU bound**: computation-heavy operations and data processing that max out CPU cycles
	- Solution: multiprocessing
### python multiprocessing pool
Pool is a class provided in the Python standard library designed to enable parallelism in **CPU-bound** tasks by leveraging multiple CPU cores or processors. 

>[!info] Python Global Interpreter Lock
>Python's **global interpreter lock** (GIL) is a [[threads#synchronization|synchronization]] mechanism that allows only one thread to execute Python bytecode in the interpreter at any given time, even across multiple [[processes]]. Pool side-steps the GIL by instantiating separate processes each with their *own* interpreter and [[virtual memory]] space.
>
>Every Python program (or program in general) is a process which spawns one thread called the `main` thread used to execute program instructions.

A **process pool** manages a fixed number of worker processes. When running a program, it can be advantageous to create a pool of workers and keep them around to pick up ad-hoc tasks rather than always instantiating and destroying a new worker process for each peripheral task.

The Pool controls
1. When workers are created (e.g. as they are needed)
2. What workers do when idle (e.g. wait without consuming resources)
Python's `multiprocessing.Pool` class provides a process pool interface to execute ad hoc tasks with variable arguments, and does not require us to specify which process to run on, explicitly start the process, or wait for the task to complete. 

Tasks are submitted to the Pool as functions, and can be submitted synchronously or asynchronously.
- **Synchronous**: caller will block until the submitted task(s) is completed
```
with multiprocessing.Pool(processes=N) as pool:
	result = pool.apply(task, args, kwargs) # submit single task
	results = pool.map(task, items)         # parallelize repeated tasks
	results = pool.starmap(task, data)      # map function w/ args
```

- **Asynchronous**: caller continues working and checks the result when it is needed
	- Returns an `AsyncResult` object, which can be used to check the status of the task or read the final result if it is completed
```
result = pool.map_async(task, items)

# keep working
...

# when needed, wait for issued task to complete
result.wait(timeout=50)

# we don't know if wait returned due to completion or timeout
if result.ready(): 
	value = result.get() # blocks if result not ready yet
	# continue with code
else:
	result.wait()
```
