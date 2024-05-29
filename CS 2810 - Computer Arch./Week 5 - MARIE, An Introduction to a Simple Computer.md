## 4.2 CPU BASICS AND ORGANIZATION:
---
The ==central processing unit (CPU)== is responsible for:
- fetching program instructions
- decoding each instruction that is fetched
- performing the indicated sequence of operations on the correct data.

CPU that can be divided into two pieces:
- the datapath, which is a network of storage units (registers) and arithmetic and logic units (for performing various operations on data) connected by buses
- The second CPU component is the control unit, a module responsible for sequencing operations and making sure the correct data are where they need to be at the correct time.

#### 4.2.1 The Registers:
storage for: 
- data
- addresses, 
- program counters
- data necessary for program execution

Registers are located on the processor so information can be accessed very quickly.
One D flip-flop is equivalent to a 1-bit register

In modern computer systems, there are many types of specialized registers: 
- registers to store information
- registers to shift values
- registers to compare values
- registers that count 
- “scratchpad” registers that store temporary values
- index registers to control program looping
- stack pointer registers to manage stacks of information for processes
- status (or flag) registers to hold the status or mode of operation (such as overflow, carry, or zero conditions)
- general-purpose registers that are the registers available to the programmer

#### 4.2.2 The ALU:
The ==arithmetic logic unit (ALU)== carries out the logic operations (such as comparisons) and arithmetic operations (such as add or multiply) required during the program execution

an ALU has two data inputs and one data output. Operations performed in the ALU often affect bits in the status register (bits are set to indicate actions such as whether an overflow has occurred)

#### 4.2.3 The Control Unit:
The control unit is the “policeman” or “traffic manager” of the CPU. It monitors the execution of all instructions and the transfer of all information

The control unit:
- extracts instructions from memory
- decodes these instructions (making sure data are in the right place at the right time)
- tells the ALU which registers to use
- services interrupts
- turns on the correct circuitry in the ALU for the execution of the desired operation.

## 4.3 THE BUS:
---
A bus is a set of wires that acts as a shared but common datapath to connect multiple subsystems within the system.

At any one time, only one device (be it a register, the ALU, memory, or some other component) may use the bus.

devices are divided into master and slave categories:
- a master device is one that initiates actions
- a slave is one that responds to requests by a master

A bus can be:
1. ==point-to-point==, connecting two specific components
2. ==Common pathway== that connects a number of devices, requiring these devices to share the bus

Point-to-point
![[Pasted image 20230925150711.png]]

Common Pathway
![[Pasted image 20230925150757.png]]

the lines of a bus dedicated to moving data are called the ==data bus==, duh!

==Control lines== indicate which device has permission to use the bus and for what purpose (reading or writing from memory or from an input/output \[I/O] device, for example)
Control lines also transfer acknowledgments for ==bus requests==, ==interrupts==, and ==clock synchronization signals==.

Typical bus transactions include sending an address (for a read or write), transferring data from memory to a register (a memory read), and transferring data to the memory from a register (a memory write)

![[Pasted image 20230925151048.png]]

buses themselves have been divided into different types. 
- Processor-memory buses are short, high-speed buses that are closely matched to the memory system on the machine to maximize the bandwidth (transfer of data) and are usually design specific. 
- I/O buses are typically longer than processor-memory buses and allow for many types of devices with varying bandwidths.

Personal Computers have an internal bus (called the system bus) that connects the CPU, memory, and all other internal components. External buses (sometimes referred to as expansion buses) connect external devices, peripherals, expansion slots, and I/O ports to the rest of the computer.

#### types of busses:
==Synchronous buses== are clocked, and things happen only at the clock ticks. The length of the bus, therefore, imposes restrictions on both the bus clock rate and the bus cycle time.

With ==asynchronous buses==, control lines coordinate the operations, and a complex handshaking protocol must be used to enforce timing. To read a word of data from memory, for example, the protocol would require steps similar to the following:
1. ReqREAD: This bus control line is activated and the data memory address is put on the appropriate bus lines at the same time.
2. ReadyDATA: This control line is asserted when the memory system has put the required data on the data lines for the bus.
3. ACK: This control line is used to indicate that the ReqREAD or the ReadyDATA has been acknowledged.
Using a protocol instead of the clock to coordinate transactions means that asynchronous buses scale better with technology and can support a wider variety of devices.


==Bus arbitration schemes must provide priority to certain master devices and, at the same time, make sure lower priority devices are not starved out.==

## 4.4 CLOCKS:
---
The CPU uses this clock to regulate its progress, checking the otherwise unpredictable speed of the digital logic gates.

The CPU requires a fixed number of clock ticks to execute each instruction. Therefore, instruction performance is often measured in clock cycles—the time between clock ticks—instead of seconds.

Most machines are synchronous: 
\- There is a master clock signal, which ticks (changing from 0 to 1 to 0 and so on) at regular intervals.

If the clock cycle is too short, we could end up with some values not reaching the registers.

==the minimum clock cycle time must be at least as great as the maximum propagation delay of the circuit, from each set of register outputs to register inputs.==

![[Pasted image 20230925152315.png]]

## 4.5 THE INPUT/OUTPUT SUBSYSTEM:
---
I/O is the transfer of data between primary memory and various I/O peripherals.

Input devices enable us to enter data into the computer: 
- keyboards
- mice
- card readers
- scanners
- voice recognition systems
- touch screens

Output devices allow us to get information from the computer:
- monitors
- printers
- plotters
- speakers 

The CPU communicates to these external devices via I/O registers.

In ==memory-mapped I/O==, the registers in the interface appear in the computer’s memory map, and there is no real difference between accessing memory and accessing an I/O device. ==Better Speed But Requires More Memory==

==instruction-based I/O==, the CPU has specialized instructions that perform the input and output. ==Requires specific I/O instructions==

## 4.6 MEMORY ORGANIZATION AND ADDRESSING:
---
You can envision memory as a matrix of bits. Each row, implemented by a register, has a length typically equivalent to the addressable unit size of the machine. Each register (more commonly referred to as a memory location) has a unique address; memory addresses usually start at zero and progress upward.
![[Pasted image 20230925192433.png]]

Memory is similar to a street full of apartment buildings. Each building (word) has multiple apartments (bytes), and each apartment has its own address. All of the apartments are numbered sequentially (addressed), from 0 to the total number of apartments in the complex minus one. The buildings themselves serve to group the apartments. In computers, words do the same thing. Words are the basic unit of size used in various instructions. For example, you may read a word from or write a word to memory, even on a byte- addressable machine.

Memory is built from random access memory (RAM) chips.

==If an architecture is byte addressable, and the instruction set architecture word size is larger than 1 byte we must address the issue of byte \_\_\_\_.==
- alignment

## 4.7 INTERRUPTS:
---
components interact with the processor through the use of interrupts. 
Interrupts are events that alter (or interrupt) the normal flow of execution in the system.

An interrupt can be triggered for a variety of reasons, including:
- I/O requests  
- Arithmetic errors (e.g., division by 0)  
- Arithmetic underflow or overflow  
- Hardware malfunction (e.g., memory parity error) User-defined break points (such as when debugging a program) 
- Page faults (this is covered in detail in Chapter 6)  
- Invalid instructions (usually resulting from pointer issues) Miscellaneous

==Interrupt Handling== is how the CPU handles the interrupts.

Interrupts can be ==maskable== (disabled or ignored) or ==non-maskable== (a high-priority interrupt that cannot be disabled and must be acknowledged)

If an architecture is byte addressable, and the instruction set architecture word size is larger than 1 byte we must address the issue of byte ________.

alignment

size