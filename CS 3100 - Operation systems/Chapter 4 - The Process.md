## Process States: At any given point  
---
- **Running**: a process is running on a processor. This means it is executing instructions  
- **Ready**: a process is ready to run but for some reason the OS has chosen not to run it at this given moment.  
- **Blocked:** a process has performed some kind of operation that makes it not ready to run until some other event takes place 
	- when a process initiates an I/O request to a disk, it becomes blocked and thus some other process can use the processor
 ![[Pasted image 20240121215253.png]]

The OS runs in privileged mode (or ==kernel mode==), where it has access to the entire machine; applications run in ==user mode==, where they are limited in what they can do.