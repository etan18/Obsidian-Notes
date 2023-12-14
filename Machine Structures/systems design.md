#cs61c #cs161 

Computer systems is a sub-field of computer science that involves low-level implementations like the operating system, [[compiler]], databases, and distributed systems.
#### programming languages
Not all programming languages are designed for writing systems software. Some properties of a good systems language include
- **Low-level memory access and management**: allow direct manipulation of memory addresses and registers. We should also be able to manually allocate memory.
- **Close mapping to assembly language**: systems software operates very closely to assembly-level, hardware-specific code. 
- **Limited abstraction**: compared to higher-level languages, they have relatively little abstraction over the underlying hardware. This makes systems programming more complex but allows finer control.
- **Lightweight runtime**: systems software must be optimized to the $n$-th degree. We want a lightweight language to be able to minimize runtime overhead.

**C/C++** are standard systems programming languages that encompass all of the above properties. A popular alternative is [[golang]], which is a modern example of a systems programming language. Go trades some of the granularity you get with C/C++ for an easier-to-learn syntax and (importantly) built-in safety checks.