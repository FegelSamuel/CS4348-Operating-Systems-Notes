# Fragmented Memory
To deal with fragmented memory, especially when it consists of many small holes that can't accommodate larger allocations, here are a few strategies:

### 1. **Compaction**
   - **Definition**: Memory compaction is a process of shifting the allocated blocks of memory to eliminate gaps between them, thus creating a larger contiguous block of free memory.
   - **How**: This is usually handled by the operating system or memory manager. The allocated memory is relocated to consolidate the free fragments into one large contiguous block.
   - **Use Case**: Useful in systems where memory can be dynamically moved (like in Java’s garbage-collected heaps).

### 2. **Segmentation and Paging**
   - **Segmentation**: Divide memory into segments of varying sizes, allowing processes to access memory in a more flexible manner.
   - **Paging**: Break memory into fixed-size pages. This allows the system to load and use non-contiguous memory, minimizing the impact of fragmentation.
   - **Use Case**: This approach is common in modern operating systems (like Linux or Windows) with virtual memory systems.

### 3. **Memory Pooling**
   - **Definition**: Create separate memory pools for allocations of different sizes. This prevents fragmentation by only allocating from pools that match the requested size.
   - **How**: You preallocate chunks of memory for small, medium, and large objects. This reduces fragmentation because each pool is optimized for a specific size.
   - **Use Case**: Used in real-time or embedded systems where memory management is performance-critical.

### 4. **Buddy System Allocator**
   - **Definition**: This technique divides memory into partitions of sizes that are powers of two, and it combines or splits these partitions as needed.
   - **How**: When you free a memory block, the system checks if the adjacent buddy block is also free and merges them. This results in progressively larger free blocks.
   - **Use Case**: Helps efficiently manage memory and avoid fragmentation when dealing with allocations of varying sizes.

### 5. **Best-Fit or First-Fit Allocator**
   - **Best-Fit**: Allocate memory from the smallest available hole that is big enough. It minimizes the amount of wasted space but can lead to more fragmentation.
   - **First-Fit**: Allocate memory from the first available hole that is big enough. It's simpler and faster but may not handle fragmentation as well as best-fit.
   - **Use Case**: These are simple techniques that work well in environments with limited memory requirements.

### 6. **Defragmentation**
   - **Definition**: Rearrange memory to eliminate small holes and consolidate them into larger free blocks. It’s similar to compaction but can involve copying objects in memory.
   - **How**: Similar to file system defragmentation, this may involve moving data to combine free blocks into one contiguous region.
   - **Use Case**: Suitable for systems that experience heavy fragmentation over time.

Each strategy is suited for different use cases depending on the memory management system in place and performance requirements. Would any of these approaches fit your project or system?
 
# Stack vs. Heap
The **stack** and **heap** are two areas of memory used by programs during execution, but they have different characteristics, purposes, and management approaches. Here’s a breakdown of the key differences:

### 1. **Memory Allocation**
   - **Stack**: 
     - Memory is allocated in a **LIFO (Last In, First Out)** order.
     - Used for static memory allocation. This includes local variables and function call-related information (such as return addresses, parameters, etc.).
     - Memory is automatically allocated and deallocated when functions are called and return, respectively.
   - **Heap**:
     - Memory is dynamically allocated at runtime via functions like `malloc()`/`free()` in C/C++ or `new`/`delete` in C++.
     - Used for dynamic memory allocation, which persists until explicitly freed by the program.
  
### 2. **Size**
   - **Stack**:
     - Usually much smaller and has a fixed size, which can lead to stack overflow if too much memory is used (e.g., deep recursion).
     - Memory is limited because it's tied to the size of the call stack in the operating system.
   - **Heap**:
     - Typically much larger and grows dynamically as more memory is requested.
     - The size is limited only by the amount of available system memory.

### 3. **Speed**
   - **Stack**:
     - Very fast because memory allocation and deallocation are simple and predictable (LIFO).
     - Accessing variables on the stack is quicker since it is managed directly by the CPU (using registers like the stack pointer).
   - **Heap**:
     - Slower to allocate and deallocate because it involves complex memory management (e.g., finding a free block, managing fragmentation).
     - Heap allocation may also require more time due to fragmentation, causing it to be less efficient over time.

### 4. **Access**
   - **Stack**:
     - Variables in the stack are usually of a **fixed size** and have a **known lifetime** (they exist only within the scope of a function).
     - Stack variables are automatically destroyed when the function exits.
   - **Heap**:
     - Objects can be dynamically created and destroyed with a flexible lifetime, but must be manually freed by the programmer.
     - Improper management (like failing to free memory) can lead to **memory leaks**.

### 5. **Management**
   - **Stack**:
     - Managed by the CPU with no need for explicit intervention by the programmer.
     - The memory is automatically allocated when a function is called and deallocated when the function exits.
   - **Heap**:
     - Managed by the programmer or runtime system, requiring explicit allocation (`malloc()` or `new`) and deallocation (`free()` or `delete`).
     - Incorrect memory management can lead to fragmentation or memory leaks.

### 6. **Typical Use Cases**
   - **Stack**:
     - For small, fixed-size data like local variables, function parameters, return addresses.
     - For recursive function calls (where each function call gets its own stack frame).
   - **Heap**:
     - For large or unknown-size objects, like dynamic data structures (linked lists, trees, etc.).
     - For data that needs to persist beyond a single function call or through the program's execution.

### 7. **Scope and Lifetime**
   - **Stack**:
     - The lifetime of variables is confined to the scope of the function in which they are declared. Once the function exits, the variables are destroyed.
   - **Heap**:
     - The lifetime of objects can persist across multiple function calls and can be controlled by the programmer.

### Summary Table:

| Aspect             | Stack                                | Heap                             |
|--------------------|--------------------------------------|----------------------------------|
| **Memory Type**     | Static (automatic) allocation        | Dynamic allocation               |
| **Size**            | Fixed and small                      | Dynamic and large                |
| **Speed**           | Faster (LIFO, managed by CPU)        | Slower (complex management)      |
| **Lifetime**        | Determined by function scope         | Determined by manual management  |
| **Management**      | Managed by CPU (automatically)       | Manually by the programmer       |
| **Use Case**        | Local variables, function calls      | Dynamic data structures, large objects |
| **Risks**           | Stack overflow (limited space)       | Memory leaks, fragmentation      |

In summary, **stack memory** is limited, fast, and automatically managed by the CPU, while **heap memory** is larger, flexible, but manually managed and slower to allocate.

# Address Translation and Segmenting
As a reminder, Segment Table is stored in Main Memory
## Logical Address (is a tuple)
* Higher order bits denote the segment number (`s`)
* Lower order bits denote the offset (`d`) within the segment.
## Steps
1. Split logical address into `s` and `d`
2. Use s as an index into the segment table and retrieve the base address (`b`) and length (`l`) of the segment
3. Compare `d` with `l` 
  > if `d` >= `l`, then generate a `trap`
  > if `d` < `l`, then add `d` to `b` to generate the physical address
Other attributes in the table can be used to perform additional checks like "is this seg number valid?" "Is the instruction comptible with the access permissions?"' 

# Calculating Seg Table Size
Let's say that:
* Virtual address space is 24 bits
* Physical address space is 32 bits
* Segment number is 6 bits
* Segment table entry contains 8 bytes (64 bits)
  * Base address needs 32 bits (because it's a physical address)
  * Limit value needs 24 - 6 = 18 bits (depends on the offset field in the virtual or logical address)
  * Other attributes can use up to 14 bits (32 + 18 + 14 = 64, we are filling out a 64-bit page line)
```bash
Segment Table Size = (Number of Entries in the Table) * (Size of each Entry in the Table) * 8 bytes * 2^6 = 512 bytes
```
# Paging
* A process is divided into fixed size blocks referred to as `pages`.
* The main memory is divided into fixed size blocks referred to as `frames`.
* Page Size = Frame Size
## Logical Addresses
Viewed as tuple

* Higher order bits denote page number (p)
* Lower order bits denote offset (d)
## Physical Addresses
These are also viewed as a tuples in which:
* Higher order bits denote the frame number (f)
* Lower order bits denote the offset (d)

## Storage
Page Table is stored in page table base register (PTBR)
## Calculating Size
The **number of entries in the table** depends on the logical address space size and the page size
The **size of each entry in the table** depends on the number of bits in the frame number, which in turn depends on page size.
## Exercise
Find Page Table Size


* Virtual address space is 24 bits
* Physical address space is 32 bits
* Page size is 1 KiB = 2^10 bytes
> Page number field needs 24 - 10 = 14 bits
> Page table entry contains 4 bytes
  > Page Frame number needs 32 - 10 = 22 bits
  > Other attributes: up to 10 bits
> 
### Advantages
* Paging eliminates external fragmentation, but suffers from very small internal fragmentation (the last page size is <= the max size of a given page)
* Memory allocation is easier
