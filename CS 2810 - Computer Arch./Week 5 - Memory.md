## 6.2 TYPES OF MEMORY:
---
### RAM:
two basic types of memory: 
- RAM (random-access memory) "read-write memory"
- ROM (read-only memory).

==RAM is  the “main memory”== Often called primary memory. RAM is used to store programs and data that the computer needs when executing programs, but RAM is volatile and loses this information once the power is turned off.

Two Types of Chips for RAM:
- SRAM (Static RAM)
- DRAM (Dynamic RAM)

==Dynamic RAM== is constructed of ==tiny capacitors that leak electricity==. DRAM requires a recharge every few milliseconds to maintain its data. (much denser (can store many bits per chip), uses less power, and generates less heat)

==Static RAM technology==, in contrast, holds its contents as long as power is available. SRAM consists of circuits similar to the ==D flip-flops== 

Often used in combination: ==DRAM for main memory== and ==SRAM for cache==.

### ROM:
==ROM== that stores critical information necessary to operate the system, such as the program necessary to boot the computer.

There are five basic types of ROM: 
- ROM
- PROM
- EPROM
- EEPROM
- flash memory

## 6.3 THE MEMORY HIERARCHY:
---
today’s computer systems use a combination of memory types to provide the best performance at the best cost. This approach is called ==hierarchical memory.==

As a rule, the faster memory is, the more expensive it is per bit of storage

==Cache memory== is a very-high-speed memory where data from frequently used memory locations may be temporarily stored.

==larger main memory==, which is typically medium-speed memory.

This memory is complemented by a very large ==secondary memory==, typically composed of hard disk drives containing data not directly accessible by the CPU

![[Pasted image 20230926105242.png]]

==virtual memory== (nonsystem memory that acts as an extension to main memory—this is discussed in detail later in this chapter)
Virtual memory is typically implemented using a hard drive; it gives the impression that a program may have a large, contiguous working main memory, when in fact the program may exist, in fragments, in main memory, and on disk.

## 6.4 CACHE MEMORY:
---
1. Purpose of caching 
- To make the computer faster

QUIZ QUESTIONS:
==For caching to be effective, we are dependent upon the idea of locality==

==In associative memory, such as cache, information is accessed by its content==

Cache memory is small, temporary, but fast memory that the processor uses for information it is likely to need again in the very near future.

the data must be accessible (locatable)

The cache location for a new block depends on two things: 
- the cache mapping policy (discussed in the next section)
- the cache size (which affects whether there is room for the new block)

==Level 1 (L1)== cache is smaller, typically 8K to 64K (on processor)
==level 2 (L2)== cache is 256K or 512K. (between CPU and Main memory)

==The purpose of cache is to speed up memory accesses by storing recently used data closer to the CPU, instead of storing it in main memory.==

Cache is not accessed by address; it is accessed by content.

#### 6.4.1 Cache Mapping Schemes:
When accessing data or instructions, the CPU first generates a main memory address.

==The mapping scheme== determines where the data is placed ==when it is originally copied into cache== and also provides a method for the CPU to ==find previously copied data== when searching cache.

Mapping schemes include:
- direct mapping
- fully associative mapping
- set-associative mapping

Steps:
1. check to see if data is already cached in the cache

#### principle of locality:
if an address was just referenced, there is a good chance that addresses in the same general vicinity will soon be referenced as well.
Therefore, one missed address often results in several found addresses.

==cache hit==: One field of the main memory address points us to a location in cache in which the data resides if it is resident in cache

==cache miss==: where it is to be placed if it is not resident

The cache block referenced is then ==checked to see if it is valid==. This is done by associating a ==valid bit== with each cache block. (0 means invalid, 1 means valid)

If valid then cache hit, if not then cache miss

==Tag== in the cache block is compared to the ==tag field of the address==.
	The tag is a special group of bits derived from the main memory address that is stored with its corresponding block in cache

If the tags are the same, then the desired cache block has been found (CACHE HIT)

we need to locate the desired data in the block; this can be done using a different portion of the main memory address called the ==offset field==. ==All cache mapping schemes require an offset field==;


Some computers are ==byte addressable==; others are ==word addressable==
	If a machine is ==byte addressable==, we are concerned with the number of bytes; 
	if it is ==word addressable==, we are concerned with the number of words, regardless of the size of the word.

## Cache Mapping Schemes:
---
2. Advantages and disadvantages of the various cache mapping schemes.
 - **Direct Mapping:**
    - _Advantages:_ Simple to implement, requires less hardware, and provides deterministic cache placement.
    - _Disadvantages:_ Limited flexibility, potential for cache conflicts (where multiple items map to the same cache location), which can lead to cache thrashing.
    
- **Set-Associative Mapping:**
    - _Advantages:_ Offers more flexibility than direct mapping by allowing multiple cache lines (a set) for each index, reducing the likelihood of cache conflicts.
    - _Disadvantages:_ More complex to implement than direct mapping, requires additional hardware, and may still suffer from cache conflicts, albeit less frequently.
    
- **Fully Associative Mapping:**
    - _Advantages:_ Maximum flexibility as any cache line can store data from any location in the main memory, which minimizes cache conflicts.
    - _Disadvantages:_ Most complex to implement, requires more hardware, and can be slower due to the need to search the entire cache for a match.

## Virtual Memory:
---
Virtual memory is a memory management technique that provides an abstraction of the computer's physical memory. It allows the operating system to use a combination of physical RAM and disk storage to simulate a larger amount of RAM than is physically available. 

The primary reasons for using virtual memory are:
- **Memory Isolation:** Virtual memory allows each process to have its own private address space, preventing one process from accessing or affecting the memory of another. This enhances system stability and security.
    
- **Resource Multiplexing:** Multiple processes can run concurrently, and virtual memory allows the operating system to efficiently allocate and manage physical memory resources among them.
    
- **Ease of Memory Management:** Virtual memory simplifies memory management for both the operating system and programmers by providing a uniform address space.

#### Memory Paging and Its Advantages/Disadvantages:
Memory paging is a virtual memory management technique that divides both physical and virtual memory into fixed-size blocks called pages. The main advantages and disadvantages of paging are:

- _Advantages:_
    - Efficient use of physical memory: Pages can be easily moved in and out of physical RAM, enabling efficient use of available memory.
    - Simplified memory allocation: Allocating and deallocating memory becomes simpler, as pages can be managed independently.
    - No external fragmentation: Paging eliminates external fragmentation, as it allocates memory in fixed-size blocks.

- _Disadvantages:_
    - Internal fragmentation: Paging can suffer from internal fragmentation when the last page allocated to a process is not fully used, wasting some memory.
    - Page table overhead: Maintaining page tables can consume additional memory and may introduce some performance overhead.
    - Potential for thrashing: If too many pages are swapped in and out of RAM frequently, it can lead to thrashing, a situation where the system spends more time managing pages than executing processes.

#### Paging vs. Segmentation:
Paging and segmentation are both memory management techniques used in virtual memory systems, but they differ in how they divide and manage memory:

- **Paging:** Divides memory into fixed-size blocks (pages) and manages memory allocation in terms of these pages. Offers more efficient memory utilization but may lead to internal fragmentation.
    
- **Segmentation:** Divides memory into variable-sized segments based on the logical structure of the program. Offers flexibility in memory allocation but can result in external fragmentation.