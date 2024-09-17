# Inversion
A schedule is said to have an inversion if there are an increasing job times and there is some smaller job that exists in the wrong place. You want to be having the smaller jobs first.
## Example
The numbers are waiting times
```bash
1, 3, 4, 9, 2
->->->->->->->
```
2 is in the wrong place, so we need to keep swapping it with adjacent jobs to put it between 1 and 3
