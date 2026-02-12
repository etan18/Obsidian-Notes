
**Operating systems**
- [Leetcode notes](https://leetcode.com/discuss/interview-question/operating-system/6038667/Operating-System-Last-Minute-Notes)
- [[scheduling]]
- [[operating system]]

**Networking notes**
- [[internet]]
- [[cookies]]
- [What happens when you search a URL in your browser?](https://medium.com/@alysachan830/tcp-and-tls-handshake-what-happens-from-typing-in-a-url-to-displaying-a-website-part-2-243862438cd9)

**What happens during the boot process of a Linux system, between power on and the time you get a login prompt?**

1. Firmware (BIOS) initializes the hardware of the system (e.g. keyboard, display, storage controllers) and performs the POST (power on self test) to check hardware integrity. It then executes the boot loader. 
2. Boot loader (in Linux, usually LILO) starts the Linux [[operating system#the os kernel|kernel]]
	- Boot loader is a specialized type of software specifically for starting the boot process and loading the OS from memory
3. The kernel process is responsible for initializing the root filesystem, drivers, and starting the `init` process. Technically, the kernel spawns the idle process (PID 0) which spawns `init`.
	- The `init` process is always the first user process started in a Linux/Unix-based system. It's spawned directly by the kernel, is a daemon (background process), and remains running until the system is shut down.
4. The `init` process (PID 1) is the actual software responsible for showing the login prompt and initializing the user-facing software components of the system.
	- Runs startup scripts, mounts additional filesystems, starts background daemons, and prepares user sessions

**What happens internally when you type a command into the shell?**

1. At its core, the shell is a computer program that serves as a command line interpreter. It is a running process that spawns a child process to execute each command a user gives it. The general format for an input command is
``` 
[PROGRAM/CMD] [OPTIONS] [ARGUMENTS]
- essential linux system binaries like ls, cp, mv, etc. are stored in /bin/
- non-essential system binaries like vim, wget, git are stored in /usr/bin/
- directories stored in the $PATH env variable are where the OS searches for executables
```
1. Given these components, the shell spawns a child process, which will use the `exec` system call, or a variant of it, to execute `PROGRAM` given the `ARGUMENTS` passed in.
2. The process will be able to find the executable for the command because essential commands are stored in the /bin/ directory by default in Linux, that's why they're always available. By default as well, the /bin/ directory is also stored within the $PATH environment variable, which is used to specify which paths to look for executable files in.

## troubleshooting

**Framework**:
1. Ask clarifying questions about the system set-up, if any.
2. Quickly brainstorm a few points where the issue may be arising from. **Try to reproduce the problem.**
3. For the main points, explain how to go about checking whether that is the problem. First want to isolate what layer of the system the error is occurring at (network, application, memory)
	- Is the server/process running? -> use `ps aux | grep` to check
	- Is memory full? -> use `df`, `du`, `free`, `top`
	- These are ways to get a high level overview of the system and see if anything glaring sticks out
4. To get more information on the problem, go into the logs.
	- Stored in `/var/log/`, with separate logs for authentication, sudo, etc.
		- `/var/log/syslog` is the standard logging facility (need sudo)
	- The `dmesg` command prints kernel-specific log messages (most useful for boot troubleshooting)
	- Check `/proc/interrupts` for information on interrupts

**Commands to check system performance**:
- `top`: displays a system summary (uptime, # running tasks/processes, active users, load averages), CPU usage, memory usage (RAM, cache, swap memory)
	- `htop` is a newer command that prints the same info in prettier display that allows for cursor movement
- `ls -l`: lists the permissions, # of hard links, owning user, owning user group, size, and modification timestamp of all files/directories in the CWD
- `df -h`: displays disk usage of the entire filesystem, where each line in the output is a partition of the system
- `du -h`: displays disk usage of files and directories
	- `-d 1` option limits the depth of search (default will print *all* recursive subdir sizes)
	- `du -sh [DIRECTORY]`  will summarize the DIRECTORY size only
- `free -h`: displays RAM/swap memory usage of the whole system 
- `ps aux`: displays the process status of all users, including background/daemon processes
	- Commonly used with 
		- `--sort=-%mem` to sort by memory usage
		- `| head -n [NUM]` to limit output
		- `| grep [STRING/PATTERN]` to find entries that match
- `vmstat`: high-level summary of system CPU, RAM, swap, disk I/O usage

### **Key Components to Consider**
1. **Resource Utilization**
    - CPU, memory, disk, and network usage
    - Are system limits being exceeded?
2. **Processes and Services**
    - Are critical services running or failing?
    - Are there memory leaks or high CPU usage?
3. **Networking**
    - Packet loss, latency, firewall rules
    - External vs. internal connectivity issues
4. **Logs and Error Messages**
    - Kernel logs, system logs, application logs
    - Are there segmentation faults, crashes, or permission issues?
5. **Filesystem and Disk I/O**
    - Is the disk full? Are there corrupt files?
    - Are IOPS or read/write latencies too high?
6. **Security and Permissions**
    - Are there permission changes or failures?
    - Are there unauthorized access attempts?

### **Important Tools & Commands**

#### **System Resource Monitoring**
- `top` / `htop` – CPU, memory usage per process
- `vmstat 1` – Real-time system performance overview
- `iotop` – Disk I/O per process
- `df -h` – Disk space usage
- `du -sh /path/to/dir` – Find large directories
- `free -m` – Memory and swap usage

#### **Process and Service Debugging**
- `ps aux --sort=-%mem` – Find high memory usage processes
- `strace -p <PID>` – Trace system calls for a process
- `lsof -p <PID>` – List files opened by a process
- `systemctl status <service>` – Check service status (for systemd)
- `journalctl -u <service> --since "1 hour ago"` – View recent logs for a service

#### **Networking Issues**
- `ping <host>` – Check basic connectivity
- `traceroute <host>` – Identify network path issues
- `netstat -tulnp` / `ss -tulnp` – Show open ports and listening services
- `iptables -L -v -n` – Check firewall rules
- `tcpdump -i eth0 port 80` – Capture packets for analysis
- `curl -v <url>` / `wget --spider <url>` – Test HTTP connectivity

#### **Logs & Debugging**
- `dmesg -T | tail -50` – View recent kernel logs
- `cat /var/log/syslog | grep <keyword>` – Search system logs
- `tail -f /var/log/nginx/error.log` – Monitor live logs

#### **Disk & Filesystem Issues**
- `lsblk` – View disk and partition layout
- `mount | grep <mountpoint>` – Check mount status
- `fsck /dev/sdX` – Check and repair filesystem
- `iostat -xz 1` – Monitor disk I/O

#### **Security & Permissions**
- `who` / `w` – Show logged-in users
- `ps aux | grep root` – Find root-owned processes
- `sudo -l` – Check sudo privileges
- `grep 'authentication failure' /var/log/auth.log` – Check failed logins

### **How to Fix Common Issues**

#### **High CPU Usage**
- Identify the culprit using `top` or `htop`.
- Kill misbehaving processes: `kill -9 <PID>`.
- Optimize or restart the service causing issues.
#### **Out of Memory (OOM)**
- Check memory usage: `free -m`.
- Kill high-memory processes: `pkill -f <process_name>`.
- Increase swap space if needed.
#### **Disk Full**
- Find large files: `du -ah / | sort -rh | head -20`.
- Remove old logs: `find /var/log -type f -name "*.log" -delete`.
- Check inode usage: `df -i`.

#### **Network Latency / Connection Issues**
- Test local vs. external connectivity (`ping`, `traceroute`).
- Check firewall settings: `iptables -L -v -n`.
- Restart network services: `systemctl restart networking`.

#### **Service Failing**
- Check logs: `journalctl -u <service> --since "10 minutes ago"`.
- Restart: `systemctl restart <service>`.
- Inspect dependencies: `systemctl list-dependencies <service>`.

#### **Filesystem Corruption**
- Run `fsck /dev/sdX` on unmounted disks.
- Remount filesystems: `mount -o remount,rw /`.

## behavioral
A great Production Engineer tends to be strong in a few areas:
- Quick and continuous learner
- Ability to understand and concisely explain complex designs and problems
- Ability to determine and remember what is important and what are distractions.
- Ability to easily ascend and descend between layers of abstraction and to see the interactions of different design choices
- Good time management - especially ensuring that small things that unblock others or that have time constraints get done quickly, while making progress on larger work items.
- General professional work relationships - being able to work well with others - people with different personalities, people in different roles (whether in general, or just in this project), contributing appropriately in various fora (not sitting quietly, not dominating)
- General professional communication - letting people know your progress and what you need from them.

In terms of technical skills:  
- Solid understanding of how computers work, kernels, operating systems, tools to introspect what they are all doing. This is the vmstat/iostat/netstat/atop sort of system introspection commands, **understanding /proc data such as smaps/fd/etc**, data and memory allocation in heap/stack/data segment, **objdump/ldd/etc stuff, profiling tools**, ...
- Solid understanding of how networks work, the responsibilities and duties of various devices, the kernel, and userland processes, **failure cases (bad link quality/packet loss, misbehaving/broken devices doing full packet drops or forgetting connections or rehashing to a different flow) and the responses to those failure cases**, understanding of flow/congestion control.
- Ability to write good, idiomatic, code in various languages, in the prevailing style of an existing codebase (or company style, even if you dislike it), and to be able to conceptualise the working of the large code bases.

---
# concurrency

#### synchronization

```
import threading

lock = threading.Lock()
lock.acquire()
...
lock.release()

sema = threading.Semaphore(initial_value)
sema.acquire()     # sema value -= 1
...                # sema blocks if initial_value = 0
sema.release()     # sema value += 1


event = threading.Event()
event.wait(timeout=10)   # calling thread blocks until event is set 
                         # or (optional) timeout expires (have to check which)
event.set()              # set event flag to True, unblock waiting threads
event.clear()            # reset event flag to False for reuse

```

#### asyncio

```
import asyncio
import aiohttp

async def fetch_url(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main():
    urls = [
        'https://example.com',
        'https://httpbin.org/get',
        'https://python.org'
    ]
    async with aiohttp.ClientSession() as session:
        tasks = [fetch_url(session, url) for url in urls]
        results = await asyncio.gather(*tasks)
        for i, content in enumerate(results):
            print(f"URL {urls[i]} returned {len(content)} characters")

asyncio.run(main())
```

- `result = await asyncio.to_thread(blocking_function, *args)`
	- offload a blocking function to another thread. the thread does not schedule until `await` is called on it.
	- Alternative: wrap it in a task to schedule it now and `await` later 
```
task = asyncio.create_task(asyncio.to_thread(blocking_function, *args))
... ...
result = await task
```

- `asyncio.run(main())`
	- Creates the event loop and handles cleanup - pass top-level entrypoint
- `asyncio.create_task()`:
	- Schedules a coroutine immediately
	- Returns a Task object
- `asyncio.gather(*iterable, return_exceptions=True)`:
	- Awaits multiple awaitables
	- Aggregates results
	- Cancels remaining tasks if one fails (by default)

![[Pasted image 20260212123336.png]]

**concurrent.futures**
![[Pasted image 20260212124800.png]]
### parallelism
**Multiprocessing**
```
import multiprocessing as mp

# ONE CHILD EXAMPLE
def child_process(arg1, arg2):
	...
	return 
	
process = multiprocessing.Process(target=child_process, args=(arg1, arg2))

# fork and execute the child process
process.start()

# caller is blocked until process terminates
process.join(timeout=optional_int)

```

- `process.exitcode`
- `process.is_alive()`

### Multiprocessing Pool
**Synchronous**: caller will block until the submitted task(s) is completed
```
with multiprocessing.Pool(processes=N) as pool:
	result = pool.apply(task, args, kwargs)          # submit single task
	results = pool.map(task, lst, chunksize=n)       # parallelize repeated tasks
	results = pool.starmap(task, lst_of_tuples)      # map function w/ args	
```

- `results = pool.imap(task, lst, chunksize=n)`
- `results = pool.imap_unordered(tasl, lst, chunksize=n)`
	- Iterable, async, memory efficient
	- Can process result from one element/chunk as soon as available, don't need to wait for whole iterable to be processed
	- use when iterable is large enough that converting it to a list would cause you to run out of/use too much memory.

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