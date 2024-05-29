## Metrics:
---
Utopia vector - the best possible metric

Turnaround Time - (p1 time + p2 time)/n

Response Time - (p1 time + p2 time)/n 
## Scheduling Policies: (Disciplines)
---
### First In, First Out (FIFO):
Where FIFO works:
![[Pasted image 20240128090747.png]]
they all arrive at the same time (10 + 20 + 30)/3 = 20 sec

Where FIFO fails:
![[Pasted image 20240128090822.png]]
This problem is generally referred to as the ==convoy effect==, where a number of relatively-short potential consumers of a resource get queued behind a heavyweight resource consumer.

### Shortest Job First (SJF):
fixes the CONVOY EFFECT. takes the shortest job first and does them

What if jobs B and C arrive when job A is getting processed?
![[Pasted image 20240128091409.png]]

Thats where Shortest Time-To-Compleation First comes in.

### Shortest Time-to-Completion First (STCF):
also called Preemptive Shortest Job First (PSJF).

Any time a new job enters the system, the STCF scheduler determines which of the remaining jobs (including the new job) has the least time left, and schedules that one.

![[Pasted image 20240128091711.png]]

#### A New Metric: Response Time:
imagine sitting at a terminal, typing, and having to wait 10 seconds to see a response from the system just because some other job got scheduled in front of yours: not too pleasant.

![[Pasted image 20240128093313.png]]

### Round Robin (RR):
instead of running jobs to completion, RR runs a job for a ==time slice== and then switches to the next job in the run queue.
RR is sometimes called time-slicing.

>the length of the time slice presents a trade-off to a system de- signer, making it long enough to amortize the cost of switching without making it so long that the system is no longer responsive.

==RR is indeed one of the worst policies if turnaround time is our metric.==
RR is doing is **stretching out each job as long as it can**, by only running each job for a short bit before moving to the next.

### Trade offs:
Any policy that is ==fair== (round robin) will have a bad performance on ==turnaround time==.

The first type (SJF, STCF) optimizes turnaround time, but is bad for response time. 
The second type (RR) optimizes response time but is bad for turnaround

### Incorporating I/O:
when a job initiates an I/O request, the current-running job won’t be using the CPU during the I/O; it is then blocked waiting for I/O completion.

![[Pasted image 20240128094653.png]]

==Overlap== - the CPU being used by one process while waiting for the I/O of another process to complete.

![[Pasted image 20240128094800.png]]


### How Can an OS Really know how long a job will take??
Follow [[Chapter 8 - Scheduling - the Multi-level feedback queue]] to answer this question.




## Extras:
---
Interrupt service rutine:
- INT -> 1 ->F1 (function 1) -> interrupt service rutine

What happens during context switch?
![[Pasted image 20240125103910.png]]
