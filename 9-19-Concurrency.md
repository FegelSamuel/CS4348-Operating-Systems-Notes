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
