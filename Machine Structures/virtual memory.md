#cs61c #cs162 

>[!info] Related: [[memory structure]]

Instead of directly accessing physical memory, [[processes]] are assigned **virtual address spaces** which are translated by the [[operating system]] into a physical address. This allows the OS to 
- Give each process the *illusion* of having all hardware resources all to itself. 
- Invoke protection by preventing access to private memory of other programs
There's a few different ways which we can represent a virtual memory address space.

### translation
In order for safe virtual memory to be implemented, the assigned virtual address needs to *translated* into its physical location in memory.

Translation can occur at any point in from the [[compiler]] to execution time.
- **Primitive multiprogramming** binds addresses to physical memory in the linking stage

>[!note] Base and Bounds
>This is a simple method of protection to limit the access that threads have to memory from the hardware side. To start, each process is allocated a fixed chunk of memory. 
>
>We introduce two registers, the base and bound registers; the base register stores the address of the start of the allocated chunk of memory, and the bound register stores the size of the chunk.

The **memory management unit (MMU)** is the actual hardware component in charge of translating virtual addresses to physical ones.

Virtual memory is usually stored in chunks, or [[pages]].

