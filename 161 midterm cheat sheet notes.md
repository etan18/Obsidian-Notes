- 1 word = 32 bits unless otherwise stated in this class
	- "word" refers to the size of a pointer, which depends on computer architecture
- The size of the address space depends on your operating system and CPU architecture. In a 32-bit system, memory addresses are 32 bits long, which means the address space has $2^{32}$ bytes of memory.
- x86 stores words using a little-endian system.
- registers
	- ebp points to the sfp of the callee frame
	- esp points to the bottom of the stack
	- eip stores the address of the instruction currently being executed
- Function arguments are placed on the stack in reverse order *before* the rip and sfp of the called function

- string formatters
- useful xor properties (lec 7 slide 6)


Topics to cover
- block ciphers
- one time pad
- diffie-hellman
- stream ciphers