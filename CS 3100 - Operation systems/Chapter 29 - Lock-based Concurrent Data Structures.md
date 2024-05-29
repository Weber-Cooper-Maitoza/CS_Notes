## Concurrent Counters:
![[Pasted image 20240317121539.png]]
![[Pasted image 20240317121521.png]]
the threads complete just as quickly on multiple processors as the single thread does on one. Achieving this end is called ==perfect scaling==

## Concurrent Linked Lists:
![[Pasted image 20240317122301.png]]

### Scaling Linked Lists
![[Pasted image 20240317122332.png]]
==hand-over-hand== locking (a.k.a. ==lock coupling==) - instead of having a single lock for the entire list, you instead add a lock per node of the list

## Concurrent Queues:
![[Pasted image 20240317122500.png]]

## Concurrent Hash Table:
![[Pasted image 20240317122532.png]]