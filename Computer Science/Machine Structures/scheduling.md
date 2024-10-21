#cs162 

In the [[operating system]], **scheduling** is the process of deciding which [[threads]] are given access to various machine resources at any given time.
## goals
An optimal scheduler takes into account the following goals
- **Minimize completion time**: waiting time + run time of [[processes]]
- **Maximize throughput**: the rate at which tasks are completed, deals with efficient use of resources (minimize overhead)
- **Maintain fairness**: sharing resources between threads in some equitable manner
The fairness criterion is the most subjective and vague of them all. It often times contradicts the goal of minimizing completion time. 

>[!tip] Benchmark
>[[C]] achieves around 90% disk utilization, which will be considered our benchmark for efficient scheduling.

As a general rule, scheduling policies should be designed to prevent **starvation**, a situation where a thread fails to make progress for an indefinite period of time. If a scheduling policy never runs a particular thread on the CPU, the thread will starve. Threads can also starve if they wait for each other or are spinning in a way that will never be resolved.

### posix
There are a few POSIX built-in functions which allow for forced [[scheduling]] manipulation. 
- `sched_yield()`: calling thread relinquishes the CPU and is put at the end of the run queue
	- The order in which threads execute is now dependent on the scheduling algorithm
- `pthread_join(pthread_t thread)`: suspend execution of the calling thread until the target _thread_ terminates
	- This is better than `sched_yield` to better ensure the order of thread execution. 
	- Calling `pthread_create` without `pthread_join` is dangerous and can waste threads such that they are never run.

---
# scheduler policies

>[!definition] Pre-emption
>In the context of the OS, preemption is the ability of the OS to pause or stop a currently scheduled task. This is how we implement **context switching** to schedule higher-priority tasks. 
### first come first serve
First come first serve (FCFS) scheduling simply schedules tasks in the order they arrive in the [[queue]].
- Cheap to implement, and good for maximizing throughput because it minimizes the overhead of context switching
- **Convoy effect**: short tasks will get stuck with long wait times behind long tasks, which makes the average completion time vary a lot.

### shortest job first
Two similar scheduling policies are *shortest job first (SJF)* and *shortest remaining time first (SRTF)*. 
- **SJF**: schedule the shortest task first
- **SRTF**: preempt the resource if a task arrives in the queue with a shorter completion time than the currently-running task
These policies are provably optimal for minimizing the average completion time for both pre-emptive and non-preemptive policies, respectively. 

>[!danger] SRTF achieves our optimal 90% disk utilization.
>Unfortunately, these policies also involve the **impossible** idea of knowing how long a task will take ahead of time, making this a theoretic upper bound on the efficiency of a scheduler.

### round robin
Round Robin (RR) schedules tasks such that each thread takes turns using the resource for a small amount of time, known as our **time quantum** $q$.
- Once $q$ elapses, the ongoing task is pre-empted and added to the end of the ready queue.
- When $q$ is sufficiently large, RR resembles FCFS, because most or all tasks are able to run to completion within a single quanta. However, a small $q$ requires a lot of overhead with frequent context switching.
Round Robin ensures fairness because of the uniform $q$. For example, if there are $n$ tasks in the queue, each task gets exactly $\frac{1}{n}$ of the resource, and will not wait more than $(n-1) \cdot q$ time units to be scheduled.

### multi-level feedback queue
Multi-level Feedback [[queue]] (MLFQ) uses multiple queues which each follow different scheduling policies. Tasks begin at the highest priority queue and move down to lower priority queues as they hog up more and more of a resource.
- Ensures that long running tasks (e.g. CPU bound) can't hog resources by keeping short running tasks (e.g. I/O bound) at higher priority

![mlfq](mlfq.png)

## strict policy
A strict scheduling policy assigns tasks a *priority*, and always schedules the task with the highest priority.
- Threads with the same priority can be scheduled in some round robin fashion
- Strict policies do *not* ensure fairness, because it starves lower priority threads

>[!info] Priority Inversion
>Consider the case where a system using a strict scheduling policy has a high priority thread which is stuck waiting for some low priority thread to complete a task. The important task cannot be scheduled, so some medium priority threads are scheduled instead, thus starving both the low priority and, by proxy, the high priority threads. 
##### priority donation
To address priority inversion, the scheduler can use **priority donation** where the lower priority task is temporarily granted the same priority as the higher priority task—known as its **effective priority**—so it can run. Once the high priority thread is no longer blocked, the low priority thread is re-assigned its **base priority**.

### lottery ticket
Give each task some number of *lottery tickets*, where the number of tickets assigned can be thought of as the priority of that task. At each time slice, a random ticket is drawn, and the task holding that ticket is granted the resource.

### stride
This is a deterministic version of lottery scheduling. Each task is defined a *stride* which is inversely proportional to the number of tickets. 
$$\text{stride} = \frac{W}{n_i}$$
Where $W$ is a really big number and $n_i$ is the number of tickets given to task $i$. At every time slice, the task with the lowest *pass* is chosen. All tasks start with pass equal to 0. When a task is chosen, its pass is incremented by $\text{stride}$. Hence, a smaller stride will allow a task to run more often.

### linux completely fair scheduler
The Linux Completely Fair Scheduler (CFS) aims to give each task an equal share of the CPU by giving an illusion that each task executes simultaneously on $\frac{1}{n}$ of the CPU.

---
## deadlock
**Deadlocking** occurs when there is a cycle of waiting amond a set of threads, where each thread is waiting for some other thread in the cycle to take some action. This is a stronger form of starvation.

There are four conditions which indicate that a deadlock *could* occur. If any one of these conditions is not met, then a deadlock *cannot* occur.
1. **Mutual Exclusion**: only a finite number of threads are able to use some resource at the same time
2. **Hold & Wait**: while a thread waits to acquire blocked resources, it is also actively holding another resource
3. **No Preemption**: once a thread acquires a resource, its ownership cannot be revoked until the thread acts to release it
4. **Circular Waiting**: there exists a set of waiting threads such that each thread is waiting for a resource held by another
Whether or not a deadlock actually occurs when these conditions are met is dependent on the order for which threads are scheduled, and what tasks those threads are performing.
#### banker's algorithm
Banker's algorithm is a technique for avoiding deadlocks. The algorithm requires the following information to be given as inputs: 
- **`resources_needed`**, an array of size $n$, where $n$ is the number of threads, and `resources_needed[i]` corresponds to the maximum amount of the given resource that thread $i$ will need (must be estimated in advance)
- **`resources_allocated`**, an array where the $i$-th element stores how many of the given resource thread $i$ currently holds.
- **`available`**, how much of the resource is currently available to be given out.
This can be expanded to handle multiple resources at once by adding an extra dimension to all inputs representing the different resources.

```
function bankers_algorithm(*args) { //inputs are described above
	safe_to_proceed = False
	unfinished_threads = list of all threads

	while not safe_to_proceed {
		safe_to_proceed = True
		for thread in unfinished_threads:
			if resources_needed[thread] - resources_allocated[thread] 
			   <= available:
				unfinished_threads.remove(thread)
				available += resources_allocated[thread]
				safe_to_proceed = False
	}
}
```


## multi-core scheduling
Implementation-wise, when we have multiple resources that each need to have efficient scheduling (i.e. multiple processor cores), each core should maintain its own set of scheduling data structures. Remember that the OS oversees *all* scheduling for all cores, each core does not have its own scheduler.
- **Affinity scheduling**: once a thread has been scheduled on a CPU, the OS tries to always reschedule it on the same CPU
	- Cache reuse
	- However, if threads are scheduled across the CPUs in a very imbalanced manner (many threads on one core), the OS will have a background thread tasked with rebalancing.
- **Gang scheduling**: when multiple threads work together, the OS will try to parallelize their running time across multiple cores. 
	- In these situations, threads may get stuck [[threads#condition variables|busy waiting]] until all of its reliant threads also finish.
