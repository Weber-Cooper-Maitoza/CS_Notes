## Sets
---
U - universe
∈ - element of 
⊆ - subset of
\{\} or ∅ - empty set

`A = {1, 2, 3}` &  `A = {2, 1, 3}` are the same!
`A = {1, 2, 3}` &  `A = {1, 1, 2, 2, 3, 3}` are *not* the same!

`B = {4, 5, 6}`

`{1, 2}` ⊆ A = T
`{1, 2}` ⊆ B = F
`{1, 2}` ∈ A = F
1, 2 ∈ A = T
1, 2, 4 ∈ A = F

`C = {1, {2, 3}, 4}`

`{1, 4}` ⊆ C = T
`{2, 3}` ⊆ C = F
`{2, 3}` ∈ C = T
`{{2, 3}}` ⊆ C = T
∅ ∈ B = F
∅ ⊆ B = T

list the elements of "set C":
- 1
- `{2, 3}`
- 4

A = `{1, 2, 3}`
list all possible subsets: 8 elements
- `{}`
- `{1}`
- `{2}`
- `{3}`
- `{1, 2}`
- `{2, 3}`
- `{1, 3}`
- `{1, 2, 3}`
or 2^3 -> 8 elements

A ⊆ A = T

`16. A = {x|x is an integer and x^2 < 16}`
`|` = is where 

## Operations
---
U - union
∩ - intersection

`A = {1, 2, 3}`
`B = {2, 4, 6}`
`A U B = {1, 2, 3, 4 ,6}` NO REPEATES
`A ∩ B = {2}`

⊕ - symmetric difference

A ⊕ B = (AUB) - (A∩B) = `{1, 3, 4, 6}`
or (A - B) U (B - A)

`||` - cardinality - how many are in the set
`|A|`= 3  - 3 elements in set A
`|AU(B∩C)|` = 3

A-Bar - Complement

`A-Bar = not A therefore = {4, 5, 6, 7, 8, 9, 10}`
`C-Bar = not nothing therefore everything = {1, 2, 3, 4, 5, 6, 7, 8, 9,10} = U - Universe`
`U-Bar = ∅` - U = universe

![[Pasted image 20240111203919.png]]

The addition principle:
need to read

![[Pasted image 20240111205448.png]]

y ∈ A ∪ B ∪ C = TRUE (sum of A B C has y in it)
