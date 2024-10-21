#cs162 

The **file system** is a layer of abstraction provided by the [[operating system]] which groups arbitrary amounts of data under a single, unified name, known as a *file*. Files typically consist of two parts:
1. **Metadata**: information about a file needed by the OS (e.g. size, owner, access control)
2. **Data**: the actual content of the file, just a raw sequence of bytes under the hood

A **directory** is a list of filename to file (or subdirectory) mappings.
- *Hard links* are directory entries that map different names to the same file number
- *Soft links* are directory entries that map a name to another name

---

>[!info] File System Design
>There are three primary components of a file system's design: its index structure, directory structure, and free space management policy.

### fast file system
Files are stored as inode arrays of pointers. Depending on the maximum file size of the system, we use direct and multi-level indirect pointers to create tree structures for quick sequential and random access to blocks in large files.

### file allocation table
The FAT, practically implemented as an array, stores disk blocks as elements in the array.
- A single **file** corresponds to a linked list of FAT entries containing pointers to the next block of file data.
- The first index of the linked list is set to be the file number.
Using a file allocation table is a simple and lightweight implementation, but it does have a hard limit on file size (4kiB) which is non-extensible.
- Good for sequential access, but bad for random access (follows from linked list implementation)
- Fixed block size prevents external fragmentation, but susceptible to internal fragmentation (e.g. storing many small files)
- Metadata and data are stored separately

### transactional file systems
**Transactions** are the fundamental unit of [[distributed systems]] which follow the following properties:
- **Atomicity**: a transaction is an indivisible unit which must occur entirely or not at all
- **Consistency**: a transaction acts upon a consistent state and ends in another consistent state (i.e. meets all integrity and correctness constraints)
- **Isolation**: each transaction must *appear* to execute on its own
- **Durability**: a transactions changes must persist through a crash
- **Indempotence**: transactions must have the same effect when executed once or many times ($f(f(x)) = f(x)$)
Transactional file systems provide reliability.