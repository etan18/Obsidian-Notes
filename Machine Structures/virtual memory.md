#cs61c #cs162 

>[!info] Related: [[memory structure]]

Instead of directly accessing physical memory, [[processes]] are assigned **virtual address spaces** which are translated by the [[operating system]] into a physical address. There's a few different ways which we can represent a virtual memory address space.

>[!note] Base and Bounds
>This is a simple method of protection to limit the access that threads have to memory from the hardware side. To start, each process is allocated a fixed chunk of memory. 
>
>We introduce two registers, the base and bound registers; the base register stores the address of the start of the allocated chunk of memory, and the bound register stores the size of the chunk.

The **memory management unit (MMU)** is the actual hardware component in charge of translating virtual addresses to physical ones.

## pages
Memory is allocated in fixed-sized chunks (typically 4kB) called **pages**. All pages are assigned a **virtual page number (VPN)**. This virtual page number is used to index that page in a process' **page table**, which maps the VPN to the PPN (physical page number). 
- Each process maintains its own page table, so the same VPN may not map to the same physical page across processes. 
- This structure enables shared memory across processes, because each process can have a VPN map to the same physical page
- The page table is itself also stored within a page.
- The **page table base register** (PTBR) contains the starting address of that process' page table.
#### translation lookaside buffer
The TLB is essentially a *cache* containing the results of recently computed address translations. It maps VPNs to PPNs (and also assiciated metadata, but not that actual page data itself).

It is usually contained as part of the MMU.
#### page faults
Page faults occur when a program attempts to access a virtual address not currently located in physical memory.

#### demand paging
When a program is actually executing, the **working set** is the subset of the address space which will actually be accessed or used. **Demand paging** stores certain working sets at disk, and only brings them into memory as necessary.

