## AWL Tree:
---
Goal: Fixed the binary "stick" tree with binary trees
Avg: O(log n)
Worst: O(log n)
If a difference of 3 exists between a parent and a child, Rotate! 
```cpp
if (nodeParent - nodeChild == 3)
	rotate
```
Locate the prior three nodes, the median becomes the new sub root.
![[Pasted image 20231117170527.png]]
Rotation occurs twice: 
![[Pasted image 20231117200901.png]]
![[Pasted image 20231117200930.png]]
Updated Tree:
![[Pasted image 20231117201004.png]]

When Rotation is triggered, the previous path of the last three nodes are used:
![[Pasted image 20231117202058.png]]
![[Pasted image 20231117202134.png]]

## B-Tree:
---
- Rule #1 - Always insert into a leaf node. Not above, not below.
- Rule #2 - If a  node has 1 item, then it now has 2 items ordered or if the node has 2 items, then the node splits and the median goes up. Then repeat rule 2 on that node.
Note: 
- a B tree can have 2 or 3 children.
- Because nodes are never created below leafs, the tree is even better balanced than an AVL tree.

having a "max degree" of 5 creates nodes with Arrays which increases speed because nodes can now be stored in cache lines.
![[Pasted image 20231117205421.png]]

## B+ Tree:
---
Enterprise usage (can be used by everything)
Used in NTFS formatting 
![[Pasted image 20231117210618.png]]
all leaf nodes contain all numbers and are connected. Think of reading blocks of data.
Linked list with a tree above it