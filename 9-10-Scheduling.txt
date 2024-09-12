CPU Scheduling
	CPU scheduling in operating systems is the process of determining which process or task will use the CPU at any given time. Since the CPU is a limited resource, scheduling ensures that all tasks get a fair share of the CPU and that the system operates efficiently.

Key concepts:

Process states: Processes can be in different states—ready, running, or waiting. The scheduler decides when a process moves from the ready state to the running state.

Scheduling criteria: Different algorithms optimize for various criteria:

CPU utilization: Keep the CPU as busy as possible.

Throughput: Maximize the number of processes completed per unit time.

Turnaround time: Minimize the total time taken to execute a process.

Waiting time: Reduce the time a process spends in the ready queue.

Response time: Minimize the time from when a request is made until the first response is produced.

Types of CPU scheduling algorithms:

First-Come, First-Served (FCFS): Processes are scheduled in the order they arrive.

Shortest Job Next (SJN): The process with the shortest expected execution time is selected next.

Round-Robin (RR): Each process gets a small time slice (quantum) in turn.

Priority Scheduling: Processes are assigned priorities, and the CPU is allocated to the highest-priority process.

Multilevel Queue: Processes are divided into different priority levels, each with its own scheduling algorithm.

Multilevel Feedback Queue: Processes can move between different queues based on their behavior and execution time.

Preemptive vs Non-preemptive scheduling: In preemptive scheduling, the operating system can interrupt a running process to allocate the CPU to another process. In non-preemptive scheduling, once a process starts running, it keeps the CPU until it finishes or blocks.

