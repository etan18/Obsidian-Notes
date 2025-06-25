#cs61c #cs161 #cs162 

The physical memory structure of a computer consists of different layers of storage, including the CPU registers, CPU [[cache]], RAM, and disk. Accessing these different layers of memory consumes increasingly more time, as they are physically spaced farther and farther away from the CPU.

At runtime, the [[operating system]] allocates the program an **address space** in [[virtual memory]] to store any state necessary for the program's execution. 
- The size of the address space is the size of a CPU register. For example, $32$-bit systems can address up to $2^{32}$ addresses, or $4$ GB of memory.
The address space is a large, contiguous section of the computer's memory. Critically, the address space is further split into 4 sections, detailed in the next sections. 
## code segment
The **code segment** is the program software. It stores the written program as bytecode. This bytecode is what's output by the [[compiler |assembler and linker]]. 
- Ideally fixed in size, more memory should not be allocated after the program is loaded
- Machine instructions—what’s being executed

## static data segment
**Static data** contains all memory that must be explicitly allocated space. This includes
- Global variables—variables declared outside of a function/outside of main
- String literals—immutable strings (char arrays) initialized with an exact value
Memory stored in this section never changes during the program's execution.  Variables declared in the static portion of memory are filled in from the bottom up. This means that variables are stored from the *lowest memory address first*.

## the heap
The **heap** contains dynamically-allocated memory that persists across functions. All variables that are `malloc`'ed and must be `free`'d are store on the heap.

>[!warning] Heap Overflow
> C++ [[vtables]] are a classic example of *heap overflow*. 

The heap fills in memory from the lowest memory addresses first and *grows upward.*
## the stack
The **stack** stores all temporary variables that are declared within a limited scope, such as a function. This includes
- Local variables—variables declared within a function that are destroyed upon returning
- String arrays—strings that are initialized dynamically, as an array

When extra memory needs to be allocated, such as during a function call, the additional variables are stored at the *highest memory address first*, with the stack growing downward as more variables are added. Otherwise, data is stored at the lowest memory address, just like the static data segment.

>[!info] Stack Canaries
> A **stack canary** is a method of mitigating computer security attacks like [[buffer overflows|stack smashing]]. Upon any function call, some dummy value is placed onto stack. In the function's prologue, we will check that the canary's value remains unchanged. If it has been changed, someone is probably trying to attack our code. This is a very cheap method to mitigate lots of *common attacks*.

#### segmentation faults
A **segmentation fault**, or segfault, is a memory error that gets thrown when a program attempts to operate on or access memory in a way that is not allowed.
- For example, a program tries to write to a read-only data segment.
- Commonly, these are thrown when the stack (which is allocated a fixed and limited size in the address space) runs out of space.

---
# memory vulnerabilities
**Memory safety bugs** are cases where an attacker can read or write beyond the valid range of memory regions.
### address space layout randomization (ASLR)
ASLR is a security measure that makes it more difficult for attackers to predict the memory addresses they need to access. Although we showed that C memory is traditionally arranged with the code section starting at the lowest address and the stack section starting at the highest address, nothing is stopping us from shifting or rearranging the memory layout. 

- With ASLR, the addresses of variables, saved registers, and code instructions will be different each time the program is run.
- Each time the program is run, the beginning of each section of memory is randomly chosen. 
- If the program imports libraries, we can also randomize the starting addresses of each library’s source code.