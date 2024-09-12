In operating systems, preemptive and non-preemptive scheduling are two methods used to manage how processes are allocated CPU time. Here’s a breakdown:

1. Preemptive Scheduling:
In preemptive scheduling, the operating system can interrupt a running process and switch the CPU to another process.
It is used to ensure that important, high-priority tasks get CPU time even if lower-priority tasks are already running.
This type of scheduling is time-sliced or based on priority levels.
Examples: Round Robin, Priority Scheduling, and Shortest Remaining Time First (SRTF).
Advantages:
Better responsiveness for interactive tasks.
Higher-priority processes get quick access to the CPU.
Disadvantages:
More context switching, which may lead to overhead.
2. Non-Preemptive Scheduling:
In non-preemptive scheduling, a process runs until it finishes or voluntarily yields control, like waiting for I/O.
The CPU cannot be taken away from a running process, and other processes must wait.
Examples: First-Come, First-Served (FCFS) and Shortest Job First (SJF) (non-preemptive version).
Advantages:
Less overhead due to fewer context switches.
Simpler implementation.
Disadvantages:
Poor responsiveness to urgent tasks.
Lower-priority processes may cause starvation for higher-priority processes.
In essence, preemptive scheduling allows for more control and flexibility at the cost of complexity, while non-preemptive scheduling is simpler but less adaptive to system needs.

As a summary, preemptive scheduling allows the SCHEDULER (NOT OS) to interrupt a running process and Context Switch the CPU to some other process where as non preemptive scheduling does NOT allow the Scheduler to make interrupts.

Priority and the idea of "Shortest job first" can be combined as well, although shortest job first only comes in when multiple processes have the same priority. 

# Infinite Problems
* An infinite arrival scenario occurs in systems dealing with queues or job scheduling, where tasks or requests keep arriving endlessly without any pause. This is often theoretical but used to study how systems behave under constant load or to simulate worst-case performance.
## Process Aging
As a process exists in the queue for longer, its priority grows larger. This basically will ensure very old processes don't just get shifted off forever.

# Round Robin
* A process is allowed to run for a *certain amount of time* after which it is pre-empted (interrupted) and another process is selected for execution.
* Time for which a process can run before it's preempted is called **time quantum** or **time slice**
  * How long a time slice is can be determined by how long context switching is and how seamless the machine gets for the user.
  * If a time slice is too short, we are walking into a massive amount of context switching, which sucks.
  * If a time slice is too long, the user experience is not so seamless.
As a reminder, processes are scheduled in priority queues, which are often heaps or red-black trees.


# Starvation
Starvation in the context of operating systems occurs when a process or thread is unable to get the resources (like CPU time, memory, or I/O) it needs to execute, often because other processes are continuously favored.

## Causes of Starvation:
**Priority Scheduling**: In systems where processes are prioritized, lower-priority processes can be "starved" if higher-priority ones keep getting selected by the CPU scheduler. For example, if new high-priority processes keep arriving, a lower-priority process may never get a chance to run.
**Resource Allocation**: Starvation can also happen in scenarios involving limited resources (e.g., disk access or memory). If a resource is always allocated to other processes before a particular process can get it, that process will be starved of the resource.
**Mutual Exclusion**: In cases where a resource is always held by one process (like in a deadlock or lock), other processes that need it could be indefinitely postponed, leading to starvation.

# Multi-Level Queue

Multilevel Queue Scheduling is a scheduling algorithm used in operating systems to manage processes by dividing them into multiple queues, each with its own scheduling strategy. This method is particularly useful when processes can be categorized into distinct types, each with different needs or priorities.

## Multiple Queues:
The system is divided into different queues, each designed for specific types of processes. For example:
* Foreground (interactive) processes: Typically require more responsive scheduling, so they might use algorithms like Round Robin.
* Background (batch) processes: These might be less time-sensitive, so they can be managed with First-Come, First-Served (FCFS).
## Process Classification:
Processes are assigned to different queues based on characteristics like priority, type (e.g., system or user processes), or expected execution time.
Once a process is assigned to a queue, it stays in that queue and is scheduled according to the queue’s specific algorithm.
## Scheduling Between Queues:
There’s also a need to schedule between the different queues. This can be done in several ways:
* Fixed priority scheduling: Queues have a strict hierarchy (e.g., the foreground queue always gets CPU time before the background queue).
* Time-slicing between queues: Each queue gets a fixed share of CPU time (e.g., the system divides CPU time between interactive and batch processes in a fair proportion).





