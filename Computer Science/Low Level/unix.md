Unix is a standard for a family of [[operating system]] variants, which include some of the most commonly used modern systems, such as **Linux** and **MacOS**, which is based on the Berkeley Software Distribution (BSD).

$100$% of supercomputers and $96.3$% of servers (both on-site and cloud-based) today run Linux.

>[!info] GNU C Library
Almost all Unix-based systems are written in [[C]], making them more portable to run on different computer architectures. The **GNU C Library** (glibc) provides a [[operating system#kernel mode transfer|system call]] interface to connect the user space and kernel space by allowing safe transitions between the two.

The basic structure of a Linux system can be summarized in the following pyramid:
![[linux.png]]

Most commonly, users interface with Linux using a **command-line interface** (CLI), although there also exist Linux graphical user interfaces (GUIs). A **shell** is a computer program that interprets user-inputted commands and executes the appropriate system calls to communicate directly with the OS. Some common Linux shells include 
- Bourne again shell (bash) and the Bourne shell (sh) - default in most Linux systems
- Z shell (zsh)
- C shell (csh)
## users
Users are individuals or entities that can manipulate files and perform operations within their defined permissions. Information about users are stored in the `/etc/passwd` file by default.

Each user is assigned a unique user ID, and users can optionally also be members of one or more **groups** with pre-defined permissions. Groups (e.g. `accounting`) are assigned a unique group ID which are listed in the `/etc/group` file. 

>[!tip] `root` 
>All Unix systems have a **superuser**, commonly called the `root` user. The root user has UID $0$ and access to the user is typically known only by the system admins.
>
>The OS kernel grants the root user to execute any command, alter any file, and change the permissions or ownership of files and directories, even ones it does not own.
#### permissions
Every file has permissions defined for the
1. Owning user [u]
2. Owning group [g]
3. Everyone else [o]
There is exactly one owning user and owning group. These permission sets are stored within the file's metadata. Each of these groups has a set of three permissions that can be added or removed: read (`r`), write (`w`), and execute (`x`). 

Only the owning user (or the `root` user) can set the permissions for their file using the `chmod` command.

## directories
Most Unix/Linux-based systems have the same default directory structure.
- `/bin`: binaries, which are compiled programs or scripts (executables)
- `/sbin`: system binaries
- `/etc`: system-wide configuration files, such as `passwd` and `group`
- `/dev`: device special files, including files to perform pseudorandom number generation, or give null and zero values
- `/proc`: process/system special files
- `/var`: variable and temporary data, such as caches and log files
- `/tmp`: created at system runtime and cleaned on each startup
- `/lib`: stores all system libraries

##### `/proc`
The `/proc` directory is important for storing information about the entire Linux system, the kernel, and [[processes]] running on it. This directory is created on system boot up.

A quick inspection of the directory will show that many files are listed, but all are zero-length. That is because, in Linux, *everything is a file*. In this case, all system and process data is organized as a **virtual [[file systems|file system]]** within the proc directory. The files listed do not exist on the disk, and are created on the fly when accessed. 

Within the directory, there will appear many virtual subdirectories, including
- **Process directories**, named with their PID
- **`self`**, a symbolic link to the current process
- **Hardware information**, stored in directories such as `cpuinfo`, `meminfo`, and `interrupts`
- **File-related information**, stored in directories such as `filesystems` and `partitions`
Many well-known utilities read information from files within `/proc`. For example, `free` pulls from `/proc/meminfo`.

>[!tip] `/proc/sys`
>While most files within `/proc` are read-only, one important directory is `/proc/sys`, which contains writeable files pertaining to kernel configuration parameters.