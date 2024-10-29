# Kernel Memory
Uses buddy system
## Buddy System
Typically manages memory using blocks whose sizes are powers of two (binary moment).

initially, the free memory is represented by a single block.

**Admissible** means that a given block `B` is able to satisfy a given request `R`

Given a request `R`, a free block `B` is said to be `admissible` if:

size(`B`)/2 < size(`R`) <= size(`B`)

1. No free block -> queue the request
2. Otherwise, give it over.

### Deallocation
So we allocate blocks by dividing powers of 2. Two blocks are said to be `buddies` if they were carved out of a single parent block. We rescursively merge two buddies to form their original parent block if they are both free.
### Implmentation
Given a block of size `S`, with address `A`, the address of the buddy is given by the bitwise (S xor A). Maintain a list of free blocks bounded by log(n) where n is the size of the initial block.
The system may impose a lower bound on the smallest block size to avoid generating very small blocks.
