These notes focus on C memory structure, specifically.
###### code segment
The **code segment** is the program software. It stores the written program as bytecode.
- Ideally fixed in size, more memory should not be allocated after the program is loaded
- Machine instructions—what’s being executed

## static data segment
**Static data** contains all memory that must be explicitly allocated space. This includes
- Global variables—variables declared outside of a function/outside of main
- String literals—immutable strings (char arrays) initialized with an exact value

Variables declared in the static portion of memory are filled in from the bottom up. This means that variables are stored from the *lowest memory address first*.

## the stack
The **stack** stores all temporary variables that are declared within a limited scope, such as a function. This includes
- Local variables—variables declared within a function that are destroyed upon returning
- String arrays—strings that are initialized dynamically, as an array

When extra memory needs to be allocated, such as during a function call, the additional variables are stored at the *highest memory address first*, with the stack growing downward as more variables are added. Otherwise, data is stored at the lowest memory address, just like the static data segment.

## the heap
The **heap** contains dynamically-allocated memory that persists across functions. All variables that are `malloc`'ed and must be `free`'d are store on the heap.

>[!warning] Heap Overflow
> C++ [[vtables]] are a classic example of *heap overflow*. 


## memory vulnerabilities
**Memory safety bugs** are cases where an attacker can read or write beyond the valid range of memory regions.