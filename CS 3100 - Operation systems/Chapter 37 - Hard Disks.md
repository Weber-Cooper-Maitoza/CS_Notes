==Seek time== is the time it takes for a disk arm to position itself over the required track.
==Rotational delay== is the time it takes for the required sector to position itself under a read/write head.
==Transfer Time==

![[Pasted image 20231003103753.png]]

## I/O Time: Doing The Math:
![[Pasted image 20240326103222.png]]
SEEK and ROTATION Take more time than TRANSFER

![[Pasted image 20240401122704.png]]

## Random and Sequential Workloads:
- Random: 
- Sequential: 
## 37.5 Disk Scheduling:

Disk Scheduling algorithms
### SSTF: Shortest Seek Time First:
SSTF orders the queue of I/O requests by track, picking requests on the nearest track to complete first
Some Problems:
1. starvation
2. OS doesn't see geometry 

### Elevator (a.k.a. SCAN or C-SCAN):
Simply moves back and forth across the disk servicing re- quests in order across the tracks.
a single pass across the disk is a ==sweep==.

==SCAN==, simply moves back and forth across the disk servicing re- quests in order across the tracks.
==F-SCAN==, which freezes the queue to be serviced when it is doing a sweep
==C-SCAN==, Instead of sweeping in both directions across the disk, the algorithm only sweeps from outer-to-inner, and then resets at the outer track to begin again.
### SPTF: Shortest Positioning Time First:
Prioritizes staying on the same track.
There is still a problem of starvation