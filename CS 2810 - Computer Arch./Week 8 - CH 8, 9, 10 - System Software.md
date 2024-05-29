#### Things to focus on in chapter 8:
- you should understand the following terms:  
	- multiprogramming   
	- multiprocessing  
	- multitasking  
	- multiuser  

- should also study to gain an understanding of the following:  
	- What are the operating system services?
	- What is a kernel and how does it relate to an operating system?  
	- How process management works in an operating system.  
	- What a virtual machine is and how it benefits the operation of a system.  
	- The purpose of link editors.  
	- The differences between link editors and Dynamic Link Libraries.  
	- The relationship between compilers and linkers.  
	- The difference between a compiler and interpreter.
#### Things to focus on in chapter 9:
- should understand the differences, strengths and weaknesses of ==RISC== and ==CISC machines== (Table 9.1). 
- You should have a general understanding of ==Flynns’s Taxonomy== and how it is used to define computer architectures.  
- Know what kinds of applications could benefit from ==parallel architectures==.  
- know what they do and what kinds of applications benefit from them:
	- Pipelining  
	- Superscalar  
	- VLIW  
	- Vector Processors  
	- Interconnection Networks  
	- Shared Memory Multiprocessors  
	- Distributed Computing  
	- Dataflow computing  
	- Neural Networks  
	- Systolic Arrays
#### Things to focus on in chapter 10:
- become familiar with the concept of an embedded system.


## Chapter 8 - System Software:
---
#### Questions to Answer:
 **Multiprocessing**:
    - Multiprocessing is a computer architecture that involves the use of multiple central processing units (CPUs) within a single computer system. It allows multiple tasks or processes to run concurrently, improving the system's performance and responsiveness.

 **Multitasking**:
    - Multitasking is an operating system feature that allows multiple tasks or processes to run concurrently on a single CPU. The CPU rapidly switches between tasks, giving the illusion of parallel execution. This allows a user to work with multiple applications simultaneously.
	
 **Multiuser**:
    - Multiuser systems are operating systems that allow multiple users to interact with the system simultaneously. Each user has their own account, files, and resources, and the operating system manages access and security for each user.
	
**Operating System Services**:
	- **Human Interface**: Provides user interfaces and input/output services.
	- **Process Management**: Manages running processes and allocates resources.
	- **Resource Management**: Controls hardware resources like CPU, memory, and devices.
	- **Security and Protection**: Ensures data and system security through access controls.
**Kernel**:
    - The kernel is the core component of an operating system. It manages hardware resources, provides essential services, and serves as an intermediary between applications and hardware. It controls the execution of processes and enforces security and protection mechanisms.
	
**Process Management in an Operating System**:
    - Process management in an operating system involves creating, scheduling, and terminating processes. It manages process states, communication, and resource allocation to ensure efficient execution of tasks.
	
**Virtual Machine**:
    - A virtual machine (VM) is a software-based emulation of a physical computer. It allows multiple operating systems to run on the same physical hardware, providing isolation, flexibility, and resource management benefits.
	
**Link Editors**:
    - Link editors, or linkers, are tools that combine object code files and resolve symbolic references to create executable programs. They play a crucial role in the compilation and linking process.
	
**Differences between Link Editors and Dynamic Link Libraries (DLLs)**:
    - Link editors create standalone executable files, while DLLs are shared libraries that can be loaded at runtime. DLLs allow code to be shared among multiple programs, conserving memory.
	
**Relationship between Compilers and Linkers**:
    - Compilers translate source code into object code, and linkers combine object code files to create an executable program. They work together to convert high-level code into a runnable application.
	
**Difference between a Compiler and Interpreter**:
    - A compiler translates the entire source code into machine code or intermediate code before execution, while an interpreter translates and executes code line by line. Compilers tend to produce faster code, while interpreters provide easier debugging and portability.
#### 8.2.3 Operating System Services:
==The operating system oversees all critical system management tasks, including memory management, process management, protection, and interaction with I/O devices.==
##### The Human Interface:
Command Line Interface - terminal, CMD
Graphical User Interface (GUI) - windows 

##### Process Management:
The operating system keeps track of each process, its status, the resources it is using, and those that it requires. The operating system’s ==main task in process scheduling== is to ==determine which process should be next in line for the CPU==.

==Multitasking== (allowing multiple processes to run concurrently)
==multithreading== (allowing a process to be subdivided into different threads of control)

##### Resource Management:
multiple processes can share one processor, multiple programs can share physical memory, and multiple users and files can share one disk.

There are ==three resources that are of major concern to the operating system==: 
- the CPU
- memory
- I/O

The scheduler controls access to the CPU

The operating system ==translates virtual addresses to physical addresses==, ==transfers pages to and from disk==, and ==maintains memory page tables==.

The operating system also determines main ==memory allocation== 
==“garbage collection”== is the process of coalescing small portions of free memory into larger, more usable chunks.

##### Security and Protection:

#### Kernel:
The ==kernel== is the core of the operating system. It is used by the process manager, the scheduler, the resource manager, and the I/O manager.
The kernel is ==responsible for scheduling, synchronization, protection/security, memory management, and dealing with interrupts.==
#### 8.3 PROTECTED ENVIRONMENTS:

##### Virtual Machines:
The real hardware of the real computer is under the exclusive command of a controlling program (or kernel).

he controlling program creates an arbitrary number of virtual machines that execute under the kernel as if they were ordinary user processes, subject to the same restrictions as any program that runs in user space.
![[Pasted image 20231016141716.png]]

#### 8.4.2 Link Editors:
On most systems, program compiler output must pass through a ==link editor (or linker)== before it can be executed on the target system.
The principal job of a link editor is to ==combine related program files into a unified loadable module.==
![[Pasted image 20231016152034.png]]
#### 8.4.3 Dynamic Link Libraries (DLL):
With proper syntax in the source program, certain external modules can be linked at run time called ==dynamic link libraries (DLLs)==
![[Pasted image 20231016152052.png]]

##### ==Advantages==
- if an external module is used repeatedly by several programs, static linking would require that each of these programs include a copy of the module’s binary code.
- if the code in one of the external modules changes, then each module that has been linked with it does not need to be relinked to preserve the integrity of the program.



## Chapter 9 - Alternative Architectures:
---
#### Questions to answer:
1. **RISC vs. CISC Machines:**
   - **RISC (Reduced Instruction Set Computer):** RISC architectures have a simplified instruction set with a small number of basic instructions, which are executed in a single clock cycle. RISC architectures aim to optimize the execution of instructions to increase overall throughput.
     - **Strengths:** RISC architectures tend to be more power-efficient and have a straightforward instruction pipeline, which makes them suitable for applications requiring high performance and low power consumption, like mobile devices.
     - **Weaknesses:** They may require more instructions to perform certain complex operations, which can lead to larger program sizes. Additionally, RISC architectures often lack complex addressing modes, which can make some programming tasks less efficient.

   - **CISC (Complex Instruction Set Computer):** CISC architectures have a more extensive and complex instruction set, with instructions capable of performing multiple operations in one instruction. CISC architectures focus on providing rich instructions for complex operations.
     - **Strengths:** CISC architectures can execute complex operations with a single instruction, potentially reducing the number of instructions needed for certain tasks. This can lead to smaller program sizes and potentially better code density.
     - **Weaknesses:** The complexity of CISC instructions can make pipelining and instruction scheduling more challenging, which can affect overall performance and power efficiency. CISC processors are often less power-efficient compared to RISC processors.

2. **Flynn's Taxonomy:**
   Flynn's Taxonomy categorizes computer architectures based on the number of instruction streams and data streams being processed simultaneously. It defines four main categories:
   - **SISD (Single Instruction, Single Data):** This represents traditional single-core, single-threaded machines. These systems execute a single instruction stream and process a single data stream, making them the simplest category.
   - **SIMD (Single Instruction, Multiple Data):** SIMD architectures process a single instruction stream but operate on multiple data streams simultaneously. This is commonly seen in vector processors and GPUs.
   - **MISD (Multiple Instruction, Single Data):** MISD architectures are relatively rare and involve multiple instruction streams operating on a single data stream. They have limited practical applications.
   - **MIMD (Multiple Instruction, Multiple Data):** MIMD architectures execute multiple instruction streams on multiple data streams. This category includes multiprocessors and distributed computing systems.

   Flynn's Taxonomy is used to categorize and understand the parallelism and concurrency aspects of computer architectures, which is crucial for designing and optimizing systems for specific applications.

3. **Applications Benefiting from Parallel Architectures:**
   Applications that can benefit from parallel architectures are those that require significant computational power and can be broken down into smaller, independent tasks. Examples include:
   - Scientific simulations and calculations
   - Weather forecasting and climate modeling
   - Video and image processing
   - Financial modeling and simulations
   - Data analysis and big data processing
   - High-performance gaming and graphics rendering
   - Cryptography and encryption/decryption
   - Artificial intelligence and machine learning

4. **Parallel Architectures and Their Applications:**
   - **Pipelining:** Pipelining is used to improve instruction throughput in processors. It's beneficial for most general-purpose computing tasks, including data processing, web browsing, and office applications.
   - **Superscalar:** Superscalar architectures can execute multiple instructions per clock cycle. They are beneficial for applications with a mix of independent instructions, like multimedia and scientific simulations.
   - **VLIW (Very Long Instruction Word):** VLIW processors use multiple functional units to execute multiple instructions in parallel. They are suitable for applications where instruction scheduling can be done at compile time, like embedded systems and signal processing.
   - **Vector Processors:** Vector processors are optimized for parallel processing of arrays or vectors of data. They excel in scientific simulations, image processing, and high-performance computing.
   - **Interconnection Networks:** These are essential for connecting multiple processors in parallel computing clusters or data centers, enabling parallel processing for a wide range of applications.
   - **Shared Memory Multiprocessors:** These are used for applications that require shared data access, like database management systems and some scientific simulations.
   - **Distributed Computing:** Distributed computing architectures are suitable for applications that can be split into tasks that run on different nodes, such as web services, distributed databases, and cloud computing.
   - **Dataflow Computing:** Dataflow architectures are used in scenarios where the order of execution depends on data availability. This is seen in some real-time systems and specific signal processing applications.
   - **Neural Networks:** Specialized hardware for neural networks and deep learning applications can greatly accelerate training and inference tasks for machine learning applications.
   - **Systolic Arrays:** Systolic arrays are well-suited for tasks involving regular data patterns and matrix operations, often found in scientific computing and signal processing.

The choice of architecture depends on the specific requirements of the application and the level of parallelism that can be exploited.
#### 9.2 RISC MACHINES:
==Reduced Instruction Set Computer== (RISC), Pentium and MIPS.
The original idea was to provide a set of ==minimal instructions that could carry out all essential operations: data movement, ALU operations, and branching.==

==Complex Instruction Set Computer== (CISC) require more clock cycles but uses less additional resources. (z80, intel 8080, mos 6502)

![[Pasted image 20231017110630.png]]
![[Pasted image 20231017110644.png]]

#### 9.3 FLYNN’S TAXONOMY:
two factors: 
1. the number of instructions
2. the number of data streams that flow into the processor.

Four possible combinations:
1. SISD (single instruction stream, single data stream)
2. SIMD (single instruction stream, multiple data streams)
3. MISD (multiple instruction streams, single data stream)
4. MIMD (multiple instruction streams, multiple data streams)

Flynn’s taxonomy falls short in several areas. For one, there seem to be very few (if any) applications for MISD machines. Secondly, Flynn ==assumed that parallelism was homogeneous.==

The two major parallel architectural paradigms, ==symmetric multiprocessors (SMPs)== and ==massively parallel processors (MPPs)==, are both MIMD architectures

MPP computers are harder to program because the programmer must make sure that the pieces of the program running on separate CPUs can communicate with each other. However, SMP machines suffer from a serious bottleneck when all processors attempt to access the same memory at the same time. The decision to use MPP or SMP depends on the application—if the problem is easily partitioned, MPP is a good option. Large companies frequently use MPP systems to store customer data (data warehousing) and to perform data mining on that data.

==Distributed computing==, defined as a set of networked computers that work collaboratively to solve a problem.

![[Pasted image 20231017115901.png]]

#### 9.4 Parallel Processes:

==Superpipelining== occurs when a pipeline has stages that require less than half a clock cycle to execute.
Superpipelining is one aspect of superscalar design

==Superscalar== is a design methodology that allows multiple instructions to be executed simultaneously in each cycle.

==Superscalar computers== are architectures that exhibit ==parallelism== through ==pipelining== and replication.
##### 9.4.2 Vector Processors:
Often referred to as ==supercomputers==, ==vector processors== are specialized, heavily pipelined SIMD processors that perform efficient operations on entire vectors and matrices at once.

Vector processors are often divided into two categories:
1. Register-register vector processors require that all operations use registers as source and destination operands
2. Memory-memory vector processors allow operands from memory to be routed directly to the arithmetic unit

##### 9.4.4 Shared Memory Multiprocessors (SMM):
![[Pasted image 20231017140253.png]]

##### 9.4.5 Distributed Computing:
In a sense, all multiprocessor systems are also distributed systems because the processing load is divided among a group of processors that work collectively to solve a problem.

Distributed Computing really means very loosely coupled multicomputer system.

![[Pasted image 20231017140448.png]]

#### 9.5 ALTERNATIVE PARALLEL PROCESSING APPROACHES:

##### 9.5.1 Dataflow Computing:
In ==dataflow computing==, the ==control of the program is directly tied to the data itself==. 

It is a simple approach: An instruction is executed when the data necessary for execution becomes available. Therefore, the actual order of instructions has no bearing on the order in which they are eventually executed.

##### 9.5.2 Neural Networks:
Neural networks, on the other hand, are useful in dynamic situations where we can’t formulate an exact algorithmic solution, and where ==processing is based on an accumulation of previous behavior.==

##### 9.5.3 Systolic Arrays:
Systolic array computers derive their name from drawing an analogy to how blood rhythmically flows through a biological heart.

==They are a network of processing elements that rhythmically compute data by circulating it through the system.==


## Chapter  10  - Topics in Embedded Systems:
---
Embedded systems are real computers, having a CPU, memory, and some sort of I/O capabilities. But they differ from general-purpose computers because they carry out a limited set of tasks within the domain of a larger system.
the larger system is something other than a computer.

divided into three categories, based on their power requirements: 
1. battery- operated
2. fixed power
3. high-density systems.

most difficult aspect of embedded systems is the matter of ==signal timing==.
