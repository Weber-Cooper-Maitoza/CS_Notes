## What is a running program?
- CPU / processor fetches instruction form memory
- Decodes the instruction
- Executes it
	- After completing goes to the next one
- Does all the above till the program concludes
- Above is Von Neumann Model
## Role of an operating system (OS):
- Virtualizes resources (such as processor and memory)
- Facilitates the smooth execution of programs
- Allows multiple programs to run at the same time
- Allows programs to share memory
- Enables programs to interact with I/O
- Makes the system easier to use and much more...
how many processes can Linux handle?
- The default kernel limit is 32,768 processes.

# Virtualization:
---
- pretends that there is unlimited memory and unlimited processors
- Efficiently managing
	- CPU, Memory, and Disk Resources
- With the goal of 
	- Fair
	- Efficient (performance)
	- easy-to-use
	- reliable
### The Process
- A Process is a program that the operating system is running.
- When a program is running is called a running process
- ==machine state==: what a program can read or update when it is running.

### Time Sharing:
- Allows users to run as many concurrent processes as they would like
	- the potential cost is performance, as each will run more slowly if the CPU(s) must be shared.

### Policy:
(decides which program to run next )
- if two programs want to run at a particular time, which should run? 
	- This question is answered by a ==policy== of the OS

### How to implement virtualization of the CPU?
Two Things Needed:
1. low-level machinery
	- ==mechanisms== are low-level methods or protocols that implement a needed piece of functionality.
	- Examples: Time Sharing, Context Switching
1. high- level intelligence


## 2.3 Concurrency:
Running processes at the same time (Sharing the cpu at the same time)
multithreading

## 2.4 Persistence:
A way to store data from memory to storage ==persistently==