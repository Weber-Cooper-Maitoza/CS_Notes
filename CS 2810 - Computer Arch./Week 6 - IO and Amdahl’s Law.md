Sections 7.1 - 7.6 
Section 7.9-7.10

## 7.1 - Intro:
---
==Disk drives== are called ==input/output devices== because data can be written to and read from them.

## 7.2 - I/O AND PERFORMANCE:
---
the root cause of why a computer acts slow is not in the processor or the memory but in how the system processes its input and output (I/O).

There are a number of tools we can use to determine the most effective way performance can be improved. ==Amdahl’s Law== is one of them.

## 7.3 - AMDAHL’S LAW:
---
In 1967, ==Gene Amdahl== recognized the ==interrelationship of all components with the overall efficiency of a computer system==. He quantified his observations in a formula, which is now known as Amdahl’s Law.

#### Amdahl’s Law states that:
>the overall speedup of a computer system depends on both the speedup in a particular component and how much that component is used by the system.

![[Pasted image 20231002105345.png]]
- S is the overall system speedup
- f is the fraction of work performed by the faster component
- k is the speedup of a new component.


CPU is used 80% of the time
new CPU we are considering is 50% faster
![[Pasted image 20231002111313.png]]

![[Pasted image 20231002111337.png]]

==Programmers can use Amdahl ’s Law to determine the overall effect on the program ’s running time.==

Suppose you have written a program and determined that 80% of the time is spent in one segment of code. You examine the code and determine that you can decrease the running time in that segment of code by half (i.e., a speedup of 2). If we apply Amdahl ’s Law, we see that the overall effect on the entire program is:
![[Pasted image 20231002111608.png]]
which means the program, as a whole, will run 1.67 times faster with the new code.

## 7.4 - I/O ARCHITECTURES:
---
We will define input/output as a subsystem of components that moves coded data between external devices and a host system, consisting of a CPU and main memory.

![[Pasted image 20231002125315.png]]

The exact form and meaning of the signals exchanged between a sender and a receiver is called a protocol. Protocols include command signals, such as “Printer reset”; status signals, such as “Tape ready”; or data- passing signals, such as “Here are the bytes you requested.”

receiver must acknowledge the commands and data sent to it or indicate that it is ready to receive data. This type of protocol exchange is called a ==handshake==.

==Buffers== allow the host system to send large quantities of data to peripheral devices in the fastest manner possible, without having to wait until slow mechanical devices have actually written the data.

### 7.4.1 I/O Control Methods:
dedicated ==I/O modules== serve as interfaces between the CPU and its peripherals

These modules perform many functions like:
- controlling device actions
- buffering data
- performing error detection
- communicating with the CPU

Computer systems employ any of five general I/O control methods:
1. programmed I/O
2. interrupt-driven I/O
3. memory-mapped I/O 
4. direct memory access
5. channel-attached I/O

#### Programmed I/O:
The ==simplest way== for a CPU to communicate with an I/O device
sometimes called polled I/O (or port I/O)

The CPU continually monitors (polls) a control register associated with each I/O port. When a byte arrives in the port, a bit in the control register is also set.
The CPU eventually polls the port and notices that the “data ready” control bit is set. The CPU resets the control bit, retrieves the byte, and processes it according to instructions programmed for that particular port. When the processing is complete, the CPU resumes polling the control registers as before.

benefit:
- we have programmatic control over the behavior of each device.
- we can adjust the number and types of devices in the system, as well as their polling priorities and intervals

problem:
- The CPU is in a continual “busy wait” loop until it starts servicing an I/O request. It doesn’t do any useful work until there is I/O to process.
- deciding how frequently to poll; some devices might need to be polled more frequently

best suited for special-purpose systems such as automated teller machines and embedded systems that control or monitor environmental events.

#### Interrupt-Driven I/O:
The ==CPU continually asking== its attached devices whether they have any input, the devices tell the CPU when they have data to send.

==Reversed Program-Driven I/O==

The ==CPU proceeds with other tasks== until a device requesting service sends an interrupt to the CPU. These interrupts are typically generated for every word of information that is transferred.

most interrupt-driven I/O uses an ==interrupt controller==.

![[Pasted image 20231002210748.png]]

he case with serial mice and modems, which often do try to share the same interrupt, causing bizarre behavior in both.

![[Pasted image 20231002211002.png]]

#### Memory-Mapped I/O:
A simpler and more elegant approach is memory- mapped I/O, in which I/O devices and main memory share the same address space.
==each I/O device has its own reserved block of memory==

#### Direct Memory Access (DMA):
![[Pasted image 20231003091801.png]]
Clearly, these instructions are simple enough to be programmed in a dedicated chip. This is the idea behind direct memory access (DMA).

![[Pasted image 20231003091844.png]]
Once the proper values are placed in memory, the CPU signals the DMA subsystem and proceeds with its next task, while the DMA takes care of the details of the I/O. After the I/O is complete (or ends in error), the DMA subsystem signals the CPU by sending it another interrupt.

#### Channel I/O:
==Most large computer systems \[mainframe]== use an intelligent type of DMA interface known as an I/O channel.

Channel I/O is becoming ==common on file servers== and ==storage networks==

one or more I/O processors control various I/O pathways called channel paths
On IBM mainframes, ==a multiplexed channel path is called a multiplexor channel==. Channels for disk drives and other “fast” devices are called ==selector channels==.
![[Pasted image 20231003092529.png]]
I/O channels are driven by ==small CPUs called I/O processors (IOPs)==, which are optimized for I/O

### 7.4.3 I/O Bus Operation:

One good reason for ==having memory on its own bus== is that memory transfers can be ==synchronous==, using some multiple of the CPU’s clock cycles to retrieve data from main memory

==I/O buses==, on the other hand, ==cannot operate synchronously==. They must take into account the fact that I/O devices cannot always be ready to process an I/O transfer.

Because these ==handshakes== take place every time the bus is accessed, I/O buses are called ==asynchronous==.

synchronous v.s. asynchronous:
- ==synchronous== transfer requires both the sender and the receiver to share a common clock for timing
- ==asynchronous== bus protocols also require a clock for bit timing and to delineate signal transitions

## 7.6 DISK TECHNOLOGY:
---
==Disk drives== are called random (sometimes direct) access devices because each unit of storage on a disk, the sector, has a unique address that can be accessed independently of the sectors around it.
![[Pasted image 20231003103753.png]]

They sometimes “==skip around==” to allow time for the drive circuitry to process the contents of a sector prior to reading the next sector. This is called ==interleaving==.
Most of today’s fixed disk drives read disks one track at a time, not one sector at a time, so interleaving is becoming less common.

### 7.6.1 Rigid Disk Drives:
Rigid (“hard” or fixed) disks contain control circuitry and one or more metal or glass disks called platters to which a thin film of magnetizable material is bonded.
![[Pasted image 20231003104353.png]]

==Seek time== is the time it takes for a disk arm to position itself over the required track.

==Rotational delay== is the time it takes for the required sector to position itself under a read/write head.

The ==sum of the rotational delay and seek time== is known as the ==access time==.

## 7.9 RAID:
---
==redundant array of independent disks (RAID)==
Using multiple disks to increase speed and efficiency of data storage

### Overview:
1. RAID 0 (Striping):
	- **Pros:**
		- Improved performance: Data is split across multiple drives, leading to faster read/write speeds.
		- Utilizes 100% of available storage space.
	- **Cons:**
		- No data redundancy: If one drive fails, all data is lost.
		- Not suitable for critical data where data loss is unacceptable.

2. RAID 1 (Mirroring):
    - **Pros:**
        - Data redundancy: Data is duplicated on multiple drives, providing fault tolerance.
        - Read performance is often improved.
    - **Cons:**
        - Limited storage efficiency: Only 50% of available storage is usable, as data is mirrored.
        - Write performance can be slower due to data duplication.

3. RAID 5 (Striping with Parity):
    - **Pros:**
        - Good balance of performance and data redundancy.
        - Efficient use of storage space (typically 75% usable).
        - Can tolerate the failure of one drive without data loss.
    - **Cons:**
        - Slower write speeds compared to RAID 0.
        - Rebuilding a failed drive can be time-consuming.
        
1. RAID 6 (Striping with Dual Parity):
    - **Pros:**
        - Enhanced data redundancy: Can withstand the failure of two drives without data loss.
        - Good read performance.
    - **Cons:**
        - Lower write performance compared to RAID 5.
        - Less storage efficiency due to dual parity (typically 50-60% usable).

### 7.9.1 RAID Level 0:
RAID Level 0, or RAID-0, places ==data blocks in stripes across several disk surfaces== so that one record occupies sectors on several disk surfaces.
This method is also called ==drive spanning==, block interleave data striping, or disk striping.
![[Pasted image 20231003110138.png]]
RAID-0 offers the ==best performance==
RAID-0 is also very ==inexpensive==
As the number of disks increases, the ==probability of failure increases== to the point where it approaches certainty
RAID-0 offers ==no-fault tolerance== because there is no redundancy
the only ==advantage== offered by RAID-0 is in ==performance==

### 7.9.2 RAID Level 1:
RAID Level 1, or RAID-1 (also known as ==disk mirroring==), gives t==he best failure protection of all RAID schemes.==
Each time data is written, it is ==duplicated onto a second set of drives== called a ==mirror set or shadow set==
![[Pasted image 20231003113939.png]]

### 7.9.3 RAID Level 2 (theoretical):
one or more disks to storing information about the data on the other disks.
RAID-2 takes the idea of data striping to the extreme. Instead of writing data in blocks of arbitrary size, RAID- 2 writes one bit per strip
Additional drives are used for error-correction information generated using a ==Hamming code==
![[Pasted image 20231003114345.png]]
==RAID-2 is too slow for most commercial implementations==
RAID-2, however, forms the theoretical bridge between RAID-1 and RAID-3, both of which are used in the real world.

### 7.9.4 RAID Level 3:
Like RAID-2, RAID-3 stripes (interleaves) data one bit at a time across all of the data drives. Unlike RAID-2, however, RAID-3 uses only one drive to hold a simple parity bit
![[Pasted image 20231003120352.png]]

it is more economical than either RAID-1 or RAID-2 because it uses only one drive for data protection.
RAID-3 has been ==used in some commercial systems== over the years, but it is not well suited for transaction-oriented applications.

### 7.9.5 RAID Level 4 (theoretical):
RAID-4 is another “==theoretical==” RAID level (like RAID- 2)
RAID-4 writes data in ==strips of uniform size==, creating a stripe across all of the drives, as described in RAID-0
![[Pasted image 20231003120643.png]]

### 7.9.6 RAID Level 5 (commercial success):
RAID-5 is RAID-4 with the parity disks spread throughout the entire array
![[Pasted image 20231003120808.png]]

Compared with other RAID systems, ==RAID-5 offers the best protection for the least cost==. As such, it has been a ==commercial success==, having the largest installed base of any of the RAID systems.

Recommended applications include file and application servers, email and news servers, database servers, and web servers.

### 7.9.7 RAID Level 6:
==Most of the RAID systems== just discussed ==can tolerate at most one disk failure at a time.==
RAID-6 provides an economical answer to the problem of multiple disk failures.
It does this by using ==two sets of error-correction strips for every rank (or horizontal row) of drives.==
![[Pasted image 20231003121827.png]]
Because of the two-dimensional parity, ==RAID-6 offers very poor write performance==.

Until recently, there were no commercial deployments of RAID-6
