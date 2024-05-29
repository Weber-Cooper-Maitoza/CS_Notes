graphs are made up of:
- Nodes
- Edges

How to store a graph:

Matrix:
![[Pasted image 20231128181424.png]]

Sparse - many nodes few neighbors
Dense  - many neighbors few nodes

### Adjacency List:
![[Pasted image 20231128182748.png]]

![[Pasted image 20231128184029.png]]

### Flat File:

### CSR:
Source, Weight, Destination
![[Pasted image 20231128185543.png]]
Weights: \[] number of nodes \* 2  (the edge weight)
Colums: \[] number of nodes \* 2 (to what node represented as a number)
Row: \[] number of nodes + 1 (how many edges there are and where)
![[Pasted image 20231130185847.png]]
Nov 28: 724308

![[Pasted image 20231130174242.png]]

## Shortest Path Algorithm: (Dijkstra's):
- Global Knowledge
- Cant Change (recompute otherwise)
- cant have negative weights

![[Pasted image 20231130175012.png]]

3 Arrays:
- visited: \[f, f, f, f, f, f, f]
- weight: \[99, 99, 99, 99, 99, 99]
- CameFrom: \[, , , , E , , ,]
![[Pasted image 20231207183724.png]]

nov 30: 975823

### Bellman-Ford (The Distance Vector) Algorithm:

 
 