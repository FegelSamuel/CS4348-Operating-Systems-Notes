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

Priority and the idea of "Shortest job first" can be combined as well.
