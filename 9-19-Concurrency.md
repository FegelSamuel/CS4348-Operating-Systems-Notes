# Mutual Exclusion Problem
Cooperating processes often share resources. 
## Sharing Discipline
Policy that defines how a resource that should be shared. The most common is **mutual exclusion**.

## Infinite while loop until it's false
```C
while (state[j] == inside); 
```

## Bad Algorithm
```C
  /* i is this process, j is the other process (from the perspective of the process that's running the code) */
  while (true) 
  {
    state[i] = interested;
    while (state[j] == interested); // while the other process is interested, stay in this while loop
    state[i] = notinterested;
  }
```

## Good Algorithm (Peterson's)
```C
while (true)
{
  state[i] = interested; // declare interest
  turn = j; // be nice to other guy
  while (state[j] == interested && turn == j);
  // critical section code
  // critical section code
  state[i] = notinterested;
  // code outside critical section
  // outside critical section
}
```

# Producer-Consumer Problem
**Producers**: Responsible for creating new items
**Consumers**: Responsible for using said items
* Messaging services
* Print spooling (send job to printer, then printer prints what's on the job)
* Copying data from a disk to a DVD/CD
* Speeds of the processes are different, they can be either faster or slower than the other. 
## Buffer-Based Solution
* Buffers can be implemented with linked lists or circular lists (array)
* Circular Wait
* Waiting is outside the critical section
* You must modify the buffer inside the critical section, however.
* Shortcomings involve a relatively large overhead regarding reserving locks.


# Semaphores

Semaphores are a synchronization tool used in computer science to manage access to shared resources, especially in multi-threaded or multi-process environments. They help ensure that multiple processes or threads don't interfere with each other when accessing the same resource, like a file or a block of memory.

## Basic Idea:
Imagine you have a limited number of toys (resources) and several kids (threads or processes) want to play with them. You want to make sure that only a certain number of kids can play with the toys at the same time. Once all the toys are taken, the other kids must wait until a toy is available again.

## Types of Semaphores:
1. **Binary Semaphore**: Think of this as a simple "lock." It has two states:
   - **0 (locked)**: Resource is in use.
   - **1 (unlocked)**: Resource is free to use.

   Only one process or thread can access the resource at a time.

2. **Counting Semaphore**: This allows multiple threads to access a set of resources. The semaphore maintains a counter to track how many resources are available. For example, if you have 5 toys (resources), the counter starts at 5. Each time a kid (thread) takes a toy, the counter decreases by 1. When the counter hits 0, no more toys are available, and any further kids must wait until someone returns a toy.

## How Semaphores Work:
- **Wait (P operation)**: This is when a thread/process wants to access the resource. It decreases the semaphore's count. If the count is 0 (no resources left), the process has to wait.
- **Signal (V operation)**: This happens when a thread/process is done using the resource and increases the semaphore's count, signaling that the resource is now available.

## Example:
Let's say you have a semaphore with a count of 2, representing two printers in a shared office:
- Thread A prints something, and the semaphore count goes from 2 to 1.
- Thread B prints something, and the semaphore count goes from 1 to 0.
- Thread C tries to print, but since the semaphore is 0, it waits until one of the printers is free again (i.e., Thread A or B finishes printing).

This ensures that no two threads are trying to use the same printer at the same time!


