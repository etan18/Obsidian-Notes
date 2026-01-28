#cs162 

Memory is allocated in fixed-sized chunks (typically 4kB) called **pages**. All pages are assigned a **virtual page number (VPN)**. This virtual page number is used to index that page in a process' **page table**, which maps the VPN to the PPN (physical page number). 
- Each process maintains its own page table, so the same VPN may not map to the same physical page across processes. 
- This structure enables shared memory across processes, because each process can have a VPN map to the same physical page
- The page table is itself also stored within a page.
- The **page table base register** (PTBR) contains the starting address of that process' page table.

>[!note] Translation Lookaside Buffer
>The TLB is essentially a *cache* containing the results of recently computed address translations. It maps VPNs to PPNs (and also assiciated metadata, but not that actual page data itself).
>
>It is usually contained as part of the **memory management unit**.

>[!note] Page Table
>The page table is a **transparent level of indirection**, because of the way it liases physical memory and [[virtual memory]]. It offers a layer of abstraction such that the OS does not need to know the actual location of the data it is trying to access.
### page faults
Page faults occur when a program attempts to access a virtual address not currently located in physical memory. Page faults are handled by the [[operating system]], specifically inducing an interrupt to trap back to the kernel, which decides what to do in the given context. 

Page faults, unlike segmentation faults, do *not* always result in an error or exception. Sometimes, we get situations where
- The address we accessed *should* be accessible, so the page fault handler allocates space for the next page and returns to the original instruction, where we are then able to proceed with our access.
- We need to perform a copy-on-write to a read-only page.
- We are trying to access a page that is currently out on disk. The page fault would load this page back into memory so that we can use it. (*demand paging*)

---
## demand paging
When a program is actually executing, the **working set** is the subset of the address space which will actually be accessed or used in a given time slice $(t_1, t_1 + \Delta)$.  **Demand paging** stores certain working sets at disk, and only brings them into memory as necessary. 

>[!tip] Thrashing
>When there's not enough DRAM or memory to store the entire working set, the OS will experience *thrashing,* which is when the OS spend excessive overhead on page swapping, thus deducting from meaningful execution time. 
>
>One solution to thrashing to is pre-empt execution of a process altogether and move its relevant pages to disk. This will allow other processes to execute smoothly, and we can resume execution of the preempted process when the working set is sufficiently small.

Paging is a different concept from *pages* as a whole. Paging refers specifically to the process of fetching *pages* of memory from disk to main memory. This is also different from a [[cache]], which brings data from memory into the processor itself, although demand paging does act similarly to a write-back cache.

### implementation
When we look up a page table entry (PTE), we can check the `valid` bit of the entry's metadata. 
- `true` indicates that the page is loaded in memory and points to a physical page
- `false` means the page is not in memory, and needs to be loaded from the disk

As mentioned previously, accessing an invalid PTE causes a page fault. While in the OS, we will
1. Replace a loaded page based on our replacement policy
2. Write the contents of the old page back to disk if its `dirty` bit is set
3. Load the new page and update the PTE
4. Return to the thread at its original location