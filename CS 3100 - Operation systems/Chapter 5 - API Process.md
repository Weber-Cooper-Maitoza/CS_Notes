## Process API:
---
operating system routine that interface with your program and the operating system.
API functions that the user can use

- `fork()` - keep running copies of the same program
- `exec()` - runs a different program
- `kill()` - destroy a process
- `wait()` - Its useful to wait

process control block - stores the process data when OS switches processes (Time Sharing)

#### How it works:
1. You type a command into the shell (Simply just a program)
2. the shell then figures out where in the file system the executable resides 
3. calls `fork()` to create a new child process to run the command
4. calls some variant of `exec()` to run the command
5. waits for the command to complete by calling `wait()`. 
6. When the child completes, the shell returns from wait() and prints out a prompt again, ready for your next command
### Process states:
- `Running` a process is running on a processor
- `Blocked` waiting for a process
==The CPU scheduler== determines which process runs at a given moment in time
==Adding a wait() call== makes the output deterministic

### Types of jobs running on your computer:
CPU bound: computation intensive
I/O bound: I/O intensive
