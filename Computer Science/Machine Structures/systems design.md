#cs61c #cs161 

Computer systems is a sub-field of computer science that involves low-level implementations like the [[operating system]], [[compiler]], databases, and distributed systems.

Systems design deals with multiple interrelated and interacting parts.
### programming languages
Not all programming languages are designed for writing systems software. Some properties of a good systems language include
- **Low-level memory access and management**: allow direct manipulation of memory addresses and registers. We should also be able to manually allocate memory.
- **Close mapping to assembly language**: systems software operates very closely to assembly-level, hardware-specific code. 
- **Limited abstraction**: compared to higher-level languages, they have relatively little abstraction over the underlying hardware. This makes systems programming more complex but allows finer control.
- **Lightweight runtime**: systems software must be optimized to the $n$-th degree. We want a lightweight language to be able to minimize runtime overhead.

[[C|C/C++]] are standard systems programming languages that encompass all of the above properties. Popular alternatives include [[Golang]] and [[Rust]], which are modern examples of systems programming languages. Go trades some of the granularity you get with C/C++ for an easier-to-learn syntax and (importantly) built-in safety checks. 

---
## design philosophy

In general, a system should be designed to comprise of a small number of basic elements that can be combined in an infinite variety of ways. A basic guideline in support of this is to make it such that every program should just do one thing very well. For example, the `ls` program produces listings, `cp` copies files, and so on without overlap in function among programs.
#### uniformity
All I/O is regularized behind a single common interface. 
- Open before use
	- metadata bookkeeping, implement checks
- Everything is a file: at the lowest level, a file is just a collection of bytes
- Byte-oriented: all data from devices are addressed in bytes, regardless of block size
- Close after use

The *principle of least surprise* dictates that a system should behave in a way that aligns with user expectations, minimizing unexpected outcomes. For example, if the command `ls A*` lists all files in the current working directory beginning with "A", then the command `rm A*` should remove all files beginning with "A".
###### file descriptor table
Each process has its own FDT.
#### data streams
Operations are performed on unformatted sequences of bytes, or *streams*, which are usually represented by `FILE*`. The data stream represents the high-level API. 