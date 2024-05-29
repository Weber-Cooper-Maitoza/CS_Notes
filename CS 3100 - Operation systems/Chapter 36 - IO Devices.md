Location of I/O devices and their Bus's
![[Pasted image 20240326170407.png]]

## A Canonical Device:

Device to interact with I/O 
![[Pasted image 20240326170556.png]]

## The Canonical Protocol:

3 Registers:
1. Data - pass data to the device, or get data from the device
2. Status - can be read to see the current status of the device
3. Command - tell the device to perform a certain task

==polling== - waits until the device is ready to receive a command by repeatedly reading the status register

Problem with polling is that it is super ==slow== and it wastes a great deal of CPU time just waiting for the (potentially slow) device to complete its activity, instead of switching to another ready process and thus better utilizing the CPU.

## Lowering CPU Overhead With Interrupts:

When the device is finally finished with the operation, it will raise a hardware interrupt, causing the CPU to jump into the OS at a pre-determined ==interrupt service routine (ISR==) or more simply an ==interrupt handler==.
![[Pasted image 20240326171458.png]]

If the speed of the device is not known, or sometimes ==fast== and sometimes ==slow==, it may be best to use a ==hybrid== that polls for a little while and then, if the device is not yet finished, uses interrupts. This ==two-phased approach== may achieve the best of both worlds

## More Efficient Data Movement With DMA:
when using programmed I/O (==PIO==) to ==transfer a large chunk of data to a device==, the CPU is once again overburdened with a rather trivial task, and thus wastes a lot of time and effort that could better be spent running other processes.
![[Pasted image 20240326171756.png]]

==Direct Memory Access (DMA)== - is essentially a very specific device within a system that can orchestrate transfers between devices and main memory without much CPU intervention
![[Pasted image 20240326171923.png]]

## Methods Of Device Interaction:
1. Oldest method is to have explicit ==I/O instructions==.
	- This way specify a way for the OS to send data to specific device registers and thus allow the construction of the protocols described above.
	- For example, to send data to a device, the caller specifies a register with the data in it, and a specific port which names the device. Executing the instruction leads to the desired behavior.
1. Second way is to interact with devices is known as ==memory- mapped I/O==.
	- the hardware makes device registers available as if they were memory locations. To access a particular register, the OS issues a load (to read) or store (to write) the address; the hardware then routes the load/store to the device instead of main memory.

## Fitting Into The OS: The Device Driver:
PROBLEM: How can we keep most of the OS device-neutral, thus hiding the details of device interactions from major OS subsystems?
- The problem is solved through the age-old technique of ==abstraction==. At the lowest level, a piece of software in the OS must know in detail how a device works. We call this piece of software a ==device driver==, and any specifics of device interaction are ==encapsulated== within.