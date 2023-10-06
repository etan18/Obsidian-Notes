In C, there are four main stages that comprise of taking the code from the *.c* file to a fully-functional executable. These stages are the **compiler**, **assembler**, **linker**, and **loader**.

### 1. compiler
The compiler converts the program from the source language—Python, Java, C/C++, etc.— into a lower-level assembly language, such as x86 or RISC-V.

### 2. assembler
The *assembler* translates the assembly instructions from the compiler into **machine code**, which is just raw bits.

### 3. linker
The *linker* pulls from all necessary object files to combine them into a single executable file. This process resolves dependencies on external libraries. 

### 4. loader
The *loader* prepares the executable file such that it's able to run. In C [[memory structure]], this includes setting up an address space in memory and running machine code instructions in the executable.