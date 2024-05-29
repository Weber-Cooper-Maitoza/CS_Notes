MLFQ tries to:
1. optimize turnaround time
2. minimize response time

## MLFQ: Basic Rules:
---
- Rule 1: If Priority(A) > Priority(B), A runs (B doesn’t).
- Rule 2: If Priority(A) = Priority(B), A & B run in RR.

![[Pasted image 20240129093942.png]]

### How MLFQ changes priority:

- Rule 3: When a job enters the system, it is placed at the highest priority (the topmost queue).
- Rule 4a: If a job uses up an entire time slice while running, its priority is reduced (i.e., it moves down one queue).
- Rule 4b: If a job gives up the CPU before the time slice is up, it stays at the same priority level.

A single long running job.
![[Pasted image 20240129094238.png]]

When a small jobs comes into use (SJF):
![[Pasted image 20240129094621.png]]

==it first assumes it might be a short job, thus giving the job high priority. If it actually is a short job, it will run quickly and complete; if it is not a short job, it will slowly move down the queues, and thus soon prove itself to be a long-running more batch-like process.==

How I/O works with MLFQ:
![[Pasted image 20240129095120.png]]

Look at ==Rule 4b== : if a process gives up the processor before using up its time slice, we keep it at the same priority level.

## Problems with MLFQ:
==Starvation:== if there are “too many” interactive jobs in the system, they will combine to consume all CPU time, and thus long-running jobs will never receive any CPU time (they starve)

==Gaming the scheduler== means that a user can write a program that will doing something sneaky to trick the scheduler into giving you more than your fair share of the resource.

### How to fix Starvation:
==The Priority Boost== periodically boost the priority of all the jobs in system.
- Rule 5: After some time period S, move all the jobs in the system to the topmost queue.
![[Pasted image 20240129110710.png]]

voodoo constants: a constant like how long until the next priority boost

### how to prevent gaming of our scheduler:
perform better ==accounting== of CPU time at each level of the MLFQ
- Instead of forgetting how much of a time slice a process used at a given level, the scheduler should keep track; once a process has used its allotment, it is demoted to the next priority queue.

- Rule 4: Once a job uses up its time allotment at a given level (regardless of how many times it has given up the CPU), its priority is reduced (i.e., it moves down one queue).
![[Pasted image 20240129113713.png]]

## Other Issues:
---
how to ==parameterize== a scheduler:
- how many queues should there be?
- How big should the time slice be per queue? 
- How often should priority be boosted in order to avoid starvation and account for changes in behavior?

How to avoid VooDoo constants:
- The frequent result: a configuration file filled with default parameter values that a seasoned administrator can tweak when something isn’t quite working correctly.

# MLFQ Rules:
---
- ==Rule 1:== If Priority(A) > Priority(B), A runs (B doesn’t).
- ==Rule 2:== If Priority(A) = Priority(B), A & B run in RR.
- ==Rule 3==: When a job enters the system, it is placed at the highest priority (the topmost queue).
- ==Rule 4==: Once a job uses up its time allotment at a given level (regardless of how many times it has given up the CPU), its priority is reduced (i.e., it moves down one queue). 
- ==Rule 5==: After some time period S, move all the jobs in the system to the topmost queue.