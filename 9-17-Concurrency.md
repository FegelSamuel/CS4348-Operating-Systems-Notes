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

