Deciding ==which page (or pages) to evict== is encapsulated within the ==replacement policy== of the OS.

## Cache Management:
Knowing the number of cache hits and misses let us calculate the ==average memory access time (AMAT)== for a program.
![[Pasted image 20240223111043.png]]

## The Optimal Replacement Policy:
==The optimal replacement policy leads to the fewest number of misses overall.==
replaces the page that will be accessed *==furthest in the future==* is the optimal policy, resulting in the fewest-possible cache misses.
![[Pasted image 20240223111554.png]]
==cold-start== miss (or compulsory miss) - The first page accesses miss.

![[Pasted image 20240223111656.png]]

## A Simple Policy: FIFO:
Many early systems avoided the complexity of trying to approach optimal and employed very simple replacement policies.

FIFO (first-in, first-out) replacement, where pages were simply placed in a queue when they enter the system; when a replacement occurs, the page on the ==tail of the queue (the “first-in” page) is evicted==. FIFO has one great strength: it is quite ==simple to implement==.

![[Pasted image 20240223111835.png]]

## Another Simple Policy: Random:
![[Pasted image 20240223111904.png]]
picks a random page to replace under memory pressure.

## Using History: LRU:
This family of policies is ==based on the principle of locality==.

==The Least-Frequently-Used (LFU)== policy replaces the least-frequently- used page when an eviction must take place.
==the Least-Recently- Used (LRU)== policy replaces the least-recently-used page.

Most- Frequently-Used (MFU) and Most-Recently-Used (MRU) dont work very well.

### Locality:
- ==spatial locality==, which states that if a page P is accessed, it is likely the pages around it (say P − 1 or P + 1) will also likely be accessed.
- ==temporal locality==, which states that pages that have been accessed in the near past are likely to be accessed again in the near future.

