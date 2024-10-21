#cs61c #cs161 

Computer systems is a sub-field of computer science that involves low-level implementations like the [[operating system]], [[compiler]], databases, and distributed systems.

Systems design deals with multiple interrelated and interacting parts.
### programming languages
Not all programming languages are designed for writing systems software. Some properties of a good systems language include
- **Low-level memory access and management**: allow direct manipulation of memory addresses and registers. We should also be able to manually allocate memory.
- **Close mapping to assembly language**: systems software operates very closely to assembly-level, hardware-specific code. 
- **Limited abstraction**: compared to higher-level languages, they have relatively little abstraction over the underlying hardware. This makes systems programming more complex but allows finer control.
- **Lightweight runtime**: systems software must be optimized to the $n$-th degree. We want a lightweight language to be able to minimize runtime overhead.

[[C|C/C++]] are standard systems programming languages that encompass all of the above properties. Popular alternatives include [[Golang]] and [[Rust]], which is a modern example of a systems programming language. Go trades some of the granularity you get with C/C++ for an easier-to-learn syntax and (importantly) built-in safety checks. 

---
## design philosophy

#### uniformity
All I/O is regularized behind a single common interface. 
- Open before use
	- metadata bookkeeping, implement checks
- Everything is a file
- Byte-oriented: all data from devices are addressed in bytes, regardless of block size
- Close after use
###### file descriptor table
Each process has its own FDT.

#### data streams
Operations are performed on unformatted sequences of bytes, or *streams*, which are usually represented by `FILE*`. The data stream represents the high-level API. 