#cs61c #cs162 

Parallelism is a core topic in machine structures. It is a principle of efficiency, where our goal as computer engineers is to execute as many instructions as possible at the same time. 

This is generally done by executing non-interfering *instruction sets* on different [[threads]] at the same time.

>[!tip] Amdahl's Law
>The amount of instructions we can run in parallel is limited—some processes must be executed sequentially. This essentially bounds how efficient parallelizing can make our programs.

In general, our runtime is composed of three factors:
1. The number of instructions in the program
2. The number of cycles per instruction
3. The time of each cycle -> cannot be sped up, the absolute limit is the speed of light

### python multiprocessing pool
Pool is a class provided in the Python standard library designed to enable parallelism in **CPU-bound** tasks by leveraging multiple CPU cores or processors. 

Python's **global interpreter lock** (GIL) is a [[threads#synchronization|synchronization]] mechanism that allows only one thread to execute Python bytecode in the interpreter at any given time, even across multiple [[processes]]. Pool side-steps the GIL by instantiating separate processes each with their *own* interpreter and [[virtual memory]] space.

>[!info] Running a Python Program
>Every Python program (or program in general) is a process which spawns one thread called the `main` thread used to execute program instructions.

A **process pool** manages a fixed number of worker processes. When running a program, it can be advantageous to create a pool of workers and keep them around to pick up ad-hoc tasks rather than always instantiating and destroying a new worker process for each peripheral task.

The Pool controls
1. When workers are created (e.g. as they are needed)
2. What workers do when idle (e.g. wait without consuming resources)
Python's `multiprocessing.Pool` class provides a process pool interface to execute ad hoc tasks with variable arguments, and does not require us to specify which process to run on, explicitly start the process, or wait for the task to complete.