## **Introduction to Memory Allocation Interface**:
- `malloc()` allocates memory of a specified size and `free()` deallocates memory, with the library needing to figure out the size of the memory chunk to be freed.

## **Heap Management and Free Lists**: 
- The memory space managed by the library is referred to as the heap, and free space within the heap is managed using a data structure known as a free list. This free list contains references to all the free chunks of space in the heap.

## Types of fragmentation:
1. external fragmentation, which occurs due to scattered free spaces within the heap.
2. internal fragmentation, where allocated memory contains unused space.

## **Low-level Mechanisms**:
splitting and coalescing. 
- Splitting involves dividing a larger free chunk to satisfy smaller allocation requests.
- coalescing merges adjacent free chunks to combat fragmentation.

## **Tracking Allocated Regions**: 
- Memory allocators often use headers to track information about allocated regions, such as size and integrity checks.

## **Growing the Heap**: 
- When the heap runs out of space, allocators may request more memory from the operating system, typically via system calls like `sbrk()`.
