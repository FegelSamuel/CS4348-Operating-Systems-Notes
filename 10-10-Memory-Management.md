# Banker's Algorithm
The **Banker's Algorithm** is a resource allocation and deadlock avoidance algorithm that determines if it’s safe to grant a resource request in a multi-process system. The algorithm helps prevent deadlocks by ensuring that resource allocation leaves the system in a safe state, where every process can complete if it’s allocated the maximum resources it could request.

### Key Concepts:
1. **Available**: The number of available instances of each resource.
2. **Maximum**: The maximum number of resources each process might request.
3. **Allocation**: The number of resources currently allocated to each process.
4. **Need**: The remaining resources each process needs to finish its task (calculated as `Need = Maximum - Allocation`).

### Steps of the Algorithm:
1. **Check Resource Request**: When a process requests resources, the algorithm checks if the request is valid:
   - If the request exceeds the **Need** of the process, it's invalid.
   - If the request exceeds the **Available** resources, the process must wait.
   
2. **Pretend to Allocate Resources**: Temporarily allocate the requested resources and update the **Available**, **Allocation**, and **Need** matrices.

3. **Check for Safe State**: After pretending to allocate resources, the system checks if it’s in a safe state. A safe state is one where there is a sequence of processes that can finish with the currently available resources.
   - If there’s a safe sequence, the resources are allocated to the process.
   - If there’s no safe sequence, the request is denied, and the system remains in the previous state.

### Example:
Imagine there are 3 types of resources: R1, R2, R3, and 5 processes P1, P2, P3, P4, P5. Each process has a maximum demand for these resources, and some resources are already allocated to each process. When a process requests additional resources, the Banker's Algorithm determines if it’s safe to grant the request.

### Why it’s called the “Banker’s” Algorithm:
It’s like a banker lending money. The banker only lends if they know they will be repaid. Similarly, the algorithm only allocates resources if it knows the system can safely avoid deadlock.

The algorithm is widely used in operating systems to handle resource allocation in multi-processing environments, ensuring that the system doesn't enter a deadlock state where no processes can proceed.

# Storage
## Types of Storage
### Primary Storage
* Directly accessible by a CPU. It includes:
  * Main Memory or RAM (random access memory)
  * Registers
  * Cache
* Typically `volatile`
### Secondary Storage
* Not directly accessible, but can be accessible by I/O channels. It includes:
  * HDD (Hard Disk Drive)
  * Solid State Drive (SSD)
### Tertiary Storage
* This is the kind of storage that persists when the machine is turned off like Disk Memory
## Main Memory
* Fetch-decode-execute cycle of a CPU
* fetch an instruction from main mem
* decode it
* fetch operands from main memory (if needed)
* execute instruction
* store results in main memory (if needed)
* Programs have to reside in main memory to `run`
  * Program has to be copied from secondary storage to main memory
# Thrashing
## swap-out
process from memory to hard to free up memory
## swap-in
a process from hard disk to memory when more memory becomes available

**swapped process may occpy a different portion of the memory after**

# Static Partitioning
**Static Partitioning** is a memory management technique where the main memory is divided into fixed-size partitions at system startup. Each partition can hold exactly one process, and the size of the partitions remains unchanged throughout the system's operation. This approach is straightforward but has some limitations in terms of memory utilization and process allocation.

### Key Characteristics:
1. **Fixed-Size Partitions**: Memory is divided into a predefined number of partitions, each with a fixed size. The number and size of these partitions are set when the system starts and cannot change during runtime.

2. **One Process per Partition**: Each partition can hold only one process. If a process requires memory, it is allocated to the smallest available partition that can fit it. If no partition is available, the process has to wait.

3. **Simpler Memory Management**: Because partitions are fixed, the operating system’s memory management is relatively simple. It just needs to keep track of which partitions are in use and which are free.

### Types of Static Partitioning:
1. **Equal-Sized Partitions**: All partitions are of the same size. This is easy to implement, but it can lead to inefficiencies, especially if the processes vary significantly in size.
   - Example: If each partition is 100 MB and a process only needs 30 MB, the remaining 70 MB of that partition goes unused, leading to **internal fragmentation** (wasted space inside the partition).

2. **Unequal-Sized Partitions**: Partitions are created with different sizes to accommodate processes with varying memory needs. This helps reduce internal fragmentation but can still leave some memory underutilized.
   - Example: A system may have partitions of 50 MB, 100 MB, and 200 MB to better fit processes of different sizes.

### Memory Allocation Process:
1. **Process Arrival**: When a process arrives and requests memory, the operating system places it into the smallest available partition that is large enough to accommodate it.
   
2. **Process Execution**: The process runs in its allocated partition until it finishes.

3. **Deallocation**: Once the process completes, the partition it was using becomes free, and another process can be assigned to it.

### Example:
Consider a system with 512 MB of memory, divided into 4 fixed-size partitions:
- Partition 1: 128 MB
- Partition 2: 128 MB
- Partition 3: 128 MB
- Partition 4: 128 MB

If a process that requires 100 MB arrives, it is allocated to one of the 128 MB partitions. The remaining 28 MB in the partition goes unused, leading to **internal fragmentation**. If another process requires 150 MB, it cannot be allocated to any of the partitions and must wait, even though there is 128 MB of free memory in each partition.

### Advantages of Static Partitioning:
1. **Simple to Implement**: The operating system doesn’t need to constantly manage partition sizes or handle compaction. It only needs to manage which partitions are occupied.
2. **Fast Allocation**: Since partition sizes are fixed, finding an appropriate partition for a process is fast and straightforward.
   
### Disadvantages:
1. **Internal Fragmentation**: Fixed-size partitions often lead to internal fragmentation because processes rarely use the exact amount of memory in a partition. Any unused memory in a partition is wasted.
2. **Limited Flexibility**: The fixed number of partitions limits how many processes can run simultaneously. If all partitions are occupied, new processes must wait, even if there’s enough free memory in the system overall.
3. **Poor Utilization of Memory**: If a large process arrives and no partition is large enough to hold it, it cannot run, even though the system might have enough total free memory spread across multiple partitions.
4. **No Dynamic Adjustment**: Once partitions are defined, they cannot be resized or rearranged during runtime to better match the needs of processes.

# Dynamic Partitioning
**Dynamic Partitioning** is a memory management technique in operating systems where memory is allocated to processes in variable-sized blocks based on their needs, rather than fixed-sized partitions. This allows for more flexible use of memory, as the size of the partition is dynamically adjusted according to the process's requirements.

### Key Characteristics:
1. **Variable-Sized Partitions**: Unlike fixed partitioning (where memory is divided into fixed-size blocks), dynamic partitioning creates partitions that can grow or shrink as processes are loaded or removed from memory. This reduces internal fragmentation (wasted space within a partition).

2. **No Fixed Boundaries**: Partitions are created and destroyed as needed, so there are no pre-set boundaries in memory. When a process needs memory, it’s allocated exactly what it requests, leaving the remaining memory available for other processes.

3. **Efficient Memory Utilization**: Since the partition sizes are determined by the process’s memory demand, dynamic partitioning generally leads to better memory utilization compared to static methods.

### Steps of Dynamic Partitioning:
1. **Request for Memory**: When a process requests memory, the operating system checks for a sufficient amount of free space to accommodate the process.
   
2. **Allocation**: If free space is available, the operating system creates a partition that is exactly the size needed for the process.

3. **Deallocation**: When a process finishes, the partition it occupied is freed, and the memory becomes available again. The freed memory is often merged with adjacent free partitions (if any) to form a larger block of available memory.

### Challenges in Dynamic Partitioning:
1. **External Fragmentation**: Over time, as processes are loaded and removed from memory, free space can become scattered in small non-contiguous blocks. Even though there may be enough total free memory for a new process, it may be fragmented into small chunks that are too small to meet the request. This issue is called **external fragmentation**.

2. **Compaction**: To reduce external fragmentation, the operating system may periodically move processes around in memory to create larger contiguous blocks of free memory. This process is known as **compaction**, but it is resource-intensive and can cause performance overhead.

### Example:
Consider a system with 100 MB of memory, and three processes request memory as follows:
- Process 1 requests 20 MB.
- Process 2 requests 30 MB.
- Process 3 requests 40 MB.

The operating system creates dynamic partitions for each process:
- Process 1 gets 20 MB.
- Process 2 gets 30 MB.
- Process 3 gets 40 MB.

Now, if Process 2 finishes and releases its 30 MB, the free space will be fragmented:
- 20 MB used by Process 1.
- 30 MB free (from Process 2).
- 40 MB used by Process 3.

If another process (Process 4) requests 50 MB, the system won’t be able to allocate it even though there’s 30 MB of free memory, because it’s split and not contiguous. The operating system may need to compact the memory, moving processes around to consolidate the free space into a contiguous block large enough for Process 4.

### Advantages of Dynamic Partitioning:
- **Flexibility**: Memory is allocated in variable sizes, meaning less wasted space and better accommodation of process memory requirements.
- **Reduced Internal Fragmentation**: Since memory is allocated based on process size, there’s less unused space within partitions.

### Disadvantages:
- **External Fragmentation**: Free space gets scattered across memory, making it harder to allocate large blocks for new processes.
- **Need for Compaction**: To reduce external fragmentation, compaction may be required, but this can be costly in terms of system performance.
