# Inversion
A schedule is said to have an inversion if there are an increasing job times and there is some smaller job that exists in the wrong place. You want to be having the smaller jobs first.
## Example
The numbers are waiting times
```bash
1, 3, 4, 9, 2
->->->->->->->
```
2 is in the wrong place, so we need to keep swapping it with adjacent jobs to put it between 1 and 3
# Exercise
| Process  | CPU Time | Priority |
| -------- | -------- | -------- |
| A | 5 ms    | 15 |
| B | 10 ms   | 5 |
| C | 3 ms    | 4 |
| D | 6 ms | 12 |
| E | 8 ms | 7 |
Five Processes will be processed on a single CPU/core. All processes are at time point 0 in state `ready`. High priorities are characterized by high values. **Draw the execution order of the processes with a Gantt chart (timeline) for Round Robin (time slice/quantum is q = 1 ms), FCFS and priority-driven scheduling.** The Priority column in the table is only relevant for the priority scheduling and not for Round Robin or FCFS. **Calculate the average runtimes and average waiting times of the processes.**

## Solution [INACCURATE]
### Round Robin
<details>
  <summary>Spoiler warning</summary>
  Time slice is 1 ms, so we go around with the smallest runtime first
  > 
</details>

### FCFS (First Come First Serve)
<details>
  <summary>Spoiler warning</summary>
  
  > A, B, C, D, E
</details>

### Priority-Driven Scheduling
<details>
  <summary>Spoiler warning</summary>
  
> A, D, E, B, C
</details>

# Sharing Resources
* Concurrent processes generally need to share some nonzero amount of resources, which is often data.
* Race conditions can happen
## Process Synchronization
* Opposite goal than IPC
* Needed to guarantee correct and stable outcome
* It looks simple, but is not!
## Problems
### Race Conditions
Correct outcome is only guaranteed in certain situations
### Deadlocks
A deadlock in an operating system occurs when a group of processes is stuck in a state where each process is waiting for a resource that another process in the group holds. As a result, none of the processes can proceed, causing the entire group to be blocked indefinitely.
### Livelocks
A livelock in an operating system occurs when two or more processes or threads are constantly changing their state in response to each other, but none of them make progress toward completing their tasks. This situation is similar to a deadlock, but in a livelock, the processes or threads are actively "doing something," whereas in a deadlock, they are completely blocked.
### Dining Philosopher Problem
* Five philosophers dine together at the same table. Each philosopher has their own plate at the table. There is a fork between each plate. The dish served is a kind of spaghetti which has to be eaten with two forks. Each philosopher can only alternately think and eat. Moreover, a philosopher can only eat their spaghetti when they have both a left and right fork. Thus two forks will only be available when their two nearest neighbors are thinking, not eating. After an individual philosopher finishes eating, they will put down both forks. The problem is how to design a regimen (a concurrent algorithm) such that any philosopher will not starve; i.e., each can forever continue to alternate between eating and thinking, assuming that no philosopher can know when others may want to eat or think (an issue of incomplete information).
* The problem was designed to illustrate the challenges of avoiding deadlock, a system state in which no progress is possible. To see that a proper solution to this problem is not obvious, consider a proposal in which each philosopher is instructed to behave as follows:

* think unless the left fork is available; when it is, pick it up;
* think unless the right fork is available; when it is, pick it up;
* when both forks are held, eat for a fixed amount of time;
* put the left fork down;
* put the right fork down;
* repeat from the beginning.
* With these instructions, the situation may arise where each philosopher holds the fork to their left; in that situation, they will all be stuck forever, waiting for the other fork to be available: it is a deadlock.

# Exercise
```C
int main() {
  for (int i = 0; i < 3; i++) {
    pid_t = fork();
    if (p == 0) {
      i++; // extra increment on i
    }
    printf("%d", i);
    fflush(); // flush buffer, it just means "actually send this thing to console"
  }
}
```
> What's a possible output?

> lmao it's a trick question we have no fucking idea

# Mutual Exclusion
A `mutex` (mutual exclusion) in C++ is used to prevent multiple threads from accessing shared resources simultaneously, ensuring that only one thread can execute a critical section of code at a time. This helps prevent race conditions—where two or more threads access shared data concurrently, potentially leading to inconsistent or unpredictable results.

## Key Concepts
* _**Mutual Exclusion**_: Only one **thread** can own the **mutex** at any given time, meaning only that thread can execute the protected critical section of code.
* _**Locking**_: A **thread** must **acquire** (or **lock**) the **mutex** before entering the critical section. Once it finishes its task, it releases (or unlocks) the **mutex** so that other **threads** can acquire it.
  * A acquires a lock and B acquires a lock and they accidentally lock each other out (dining philosophers problem, nobody wants to put their singular fork down)
* _**Blocking**_: If a **thread** tries to acquire a **mutex** that is already locked by another **thread**, it will be **blocked** until the **mutex** is released.

```C
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;  // Declare a mutex

void printNumbers(int id) {
    mtx.lock();  // Lock the mutex before entering critical section
    for (int i = 0; i < 5; ++i) {
        std::cout << "Thread " << id << " is printing " << i << std::endl;
    }
    mtx.unlock();  // Unlock the mutex after leaving the critical section
}

int main() {
    std::thread t1(printNumbers, 1);
    std::thread t2(printNumbers, 2);

    t1.join();
    t2.join();

    return 0;
}
```

