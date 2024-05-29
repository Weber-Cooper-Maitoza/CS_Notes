- Swap Space
	- Space on secondary storage
	- present bit P
- Page fault
	- Page is not present in Swap Space
	- Page fault handler
- Memory Full 
	- ==Page Replacement Policy==
- Types of Localities
	- Spatial and temporal

## Swap Space:
![[Pasted image 20240223083432.png]]
Notice Proc 3 isn't in physical memory. this means that program isnt running.

## P bit and Page Faulting:
 Paging steps:
1. check if in ==TBL==
2. check if Page is ==present==(P bit)
3. check if page is in ==swap space== (HDisk)
4. if nothing, ==Page fault==
In either type of system, if a page is not present, the OS is put in charge to handle the page fault. The appropriately-named OS ==page-fault handler== runs to determine what to do.

## What If Memory Is Full?
the OS might like to first page out one or more pages to make room for the new page(s) the OS is about to bring in. **The process of picking a page to kick out**, or replace is ==known as the page-replacement policy.==