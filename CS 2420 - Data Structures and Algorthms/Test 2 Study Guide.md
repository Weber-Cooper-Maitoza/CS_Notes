## Big O:
---
- Order Big O notation and understand common scenarios.
	1. O(1) - Independent of n (constant time)
	2. O(log n) - divide and conquer 
	3. O(n) - Loop down every item
	4. O(n log n) - Loop and divid and conquer
	5. O(n^2) - Loop within a loop
	6. O(n^3) - 3 nested loops
	7. O(2^n) - brute force
	8. O(n\*n!) - a joke

## Hash Tables:
---
- ==Open hashing: linked lists==
- ==Closed hashing: arrays==
- ==Open addressing: allow elements to overflow out of their target bucket and into other spaces.==
- ==Closed addressing: store colliding elements in an auxiliary data structure like a linked list or a binary search tree.==
- What is hashing:
	- Hashing is a way to get an even distribution of values by feeding the value into a hashing function which returns a unique key, but you cannot reverse the order and give a function the key and then return the value.
- What is a collision:
	- a collision is when one value returns the same key as another value. 
- Overall goal of a hash table:
	- To make looking up data in a table be Big O(1) time instead of O(n) (looking down every item)
- Big O notation for all operations, on average:
	- Insertion = O(1)
	- retrieve = O(1)
	- deletion = O(1)
- Worst case Big O for hash tables:
	- Worst case = O(n) - looping down every item
- A good rule of thumb to avoid collision issues and keep O(1):
	- have enough space to not have collisions (2:1 ratio 2 open slots per 1 peice of data)
- What to do if a hash table's slots get too full?
	- Resize table when table gets to be 50% full
#### Open Hashing (Linked Lists)
- Why use this approach?
	- No secondary clustering problem
	- No capacity problems
	- Don't have to "make deleted" 
	- less wasted space
- Why avoid this approach?
	- Slow
	- Doesn't work without dynamic memory
- What is the Step-by-step process to insert, retrieve, and delete items?
	- Insert:
		1. Hash key mod by capacity -> index
		2. go to list\[index] 
		3. emplace front key and value pair 
	- Retrieve:
		1. Hash key mod by capacity -> index
		2. go to list\[index]
		3. iterate through list to find key
		4. if key in list
			1. return value
		5. else throw error
	- Delete:
		1. Hash key mod by capacity -> index
		2. go to list\[index]
		3. remove if key is in list
- Be prepared to write code to insert an item or retrieve an item given a key:
	- Insert:
	 ```cpp
	void HashTable<K, V>::create(const K& key, const V& value) {
	  int hashedIndex = std::hash<K>{}(key) % capacity;
	  this->arrayOfLists[hashedIndex].emplace_front(key, value);
	  this->count++;
	}
	```
	- Retrieve:
	```cpp
	V HashTable<K, V>::retrieve(const K& key) const {
	  int hashedIndex = std::hash<K>{}(key) % capacity;
	  for (auto& keyValue : this->arrayOfLists[hashedIndex]) {
	    if (keyValue.first == key) {
	      return keyValue.second;
		    }
		  }
	  throw std::out_of_range("Key/Value not in hash table");
	}
	```

#### Closed Hashing (arrays):
---
- Why use this approach?
	- Fast 
	- Does work without dynamic memory
- Why avoid this approach?
	- secondary clustering problem
	- capacity problems
	- has to make "deleted" 
	- more wasted space
- Step-by-step process for:
	- Inserting:
		1. check if adding a value will full capacity to 50%
		2. if it will
			1. make a new hash table 2x the size of original
			2. iterate through every element in original hash table
			3. if status array == 1
				1. copy over key and value pair and place at "counter" index
			4. else 
				1. increment counter
			5. when done, `*this = std::move(newHashTable);`
		3. hash key and mod by capacity -> index
		4. loop through table capacity times
			1. if status array = -1 or 0
				1. place keyvalue pair at that spot in keyvalue array
				2. set that spot in status array to 1
				3. increment count 
			2. else loop around by `hashedIndex = (hashedIndex + 1) % this->capacity`
	- Retrieving:
		1. hash key and mod by capacity
		2. loop through table capacity times
			1. if status array = 1
				1. if keyvalue array = key
					1. return value
				2. else, increment count and wrap around if needed
			2. else if, status array = -1
				1. increment count and wrap around if needed
			3. else
				1. throw error
		3. else
			1. throw error
	- Deleting:
		- do retrieving steps except instead of returning value, set status array to -1.
- What is a status array? why does it need one?
	- A status array is used to find a location that is empty to fill with key and value, to check to see what has been filled, and to determine what can be over written (deleted). A closed hash table needs this to manage the table.
- What is clustering?
	- Clustering is when groups of data that has been inputed into the hash table "cluster together". this is a problem because if the cluster gets to big, the table ends up having to walk O(n) times down the array. The goal is an even distribution of data in the table.
- What is linear probing and quadratic probing?
	- Linear Probing: `(hash value + i) mod capacity`
		- This happens when the algorithm looks for the next available slot in the hash table to insert data into. Linear probing probes consecutively to the next slot then inserts data.
	- Quadratic Probing:
		- For quadratic probing, the capacity has to always be a prime number. Quadratic probing uses `(hash value + i^2) mod capacity`
## Cuckoo Hashing:
---
- What is the main purpose of cuckoo hashing?
	- The main purpose of cuckoo hashing is to get a worst case O(1)!
- How does it work?
	- There are two hash tables key/value pair can reside
	- if a hashed key in the first table is taken, that key/value replaces the old data, then the old data is rehashed using `(key/capacity) % capacity`and is placed in second hash table.
- What does it do better?
	- guarantees O(1) worst case lookup time
	- **Insertion** is expected O(1)
	- **Deletion** is O(1) worst-case
- What does it do worse?
	- Time complexity = O(n)
	- Space usage = O(n)
## Search Algorithms:
---
- How does a linear search work? What is it's Big O? (This is easy)
	- Linear search works by incrementing down a container trying to find a mach. This would produce a Big O of O(n) because it is looping down n times
- Suppose the container is sorted, now how can it be searched?
	1. Sequential search: ==linear search==
	2. Interval search: ==binary search - target the center of the search structure and divide the search space in half==

## Sort Algorithms:
---
- Describe all 7 sort algorithms in class:
	- Bubble: ==Compare pairs of values then swap the larger to the right. Repeat for each pair. Repeat for all pairs until the largest value has "bubbled" to the right.==
		- Average Complexity:O(n^2)
		- Worst Complexity: O(n^2)
		- Average Memory: O(1)
		- Worst Memory: O(1)
		- STABLE
	- Selection: ==selects the smallest element from the unsorted portion of the list and swaps it with the first element of the unsorted part.==
		- Average Complexity:O(n^2)
		- Worst Complexity: O(n^2)
		- Average Memory: O(1)
		- Worst Memory: O(1)
		- STABLE
	- Insertion: ==Array split into two parts, sorted and unsorted. Values from the unsorted part get inserted into the sorted part.==
		- Average Complexity: O(n^2)
		- Worst Complexity: O(n^2)
		- Average Memory: O(1)
		- Worst Memory: O(1)
		- STABLE
	- Quick: ==Recursive divide and conquer algorithm that picks pivots and partitions the given array around the picked pivot by placing the pivot in its correct position in the sorted array.==
		- Average Complexity: O(n log n)
		- Worst Complexity:O(n^2)
		- Average Memory: O(log n)
		- Worst Memory: O(n)
		- ==NOT== STABLE
	- Merge: ==Recursively merge two sorted arrays== 
		- Average Complexity: O(n log n)
		- Worst Complexity: O(n log n)
		- Average Memory: O(n)
		- Worst Memory: O(n)
		- STABLE
	- Heap: ==Uses a max heap to find largest value, which is then placed at the end of list== Left-child = 2n+1, Right-child = 2n+2, Parent = (n-1)/2
		- Average Complexity: O(n log n)
		- Worst Complexity: O(n log n)
		- Average Memory: O(1)
		- Worst Memory: O(1)
		- ==NOT== STABLE!!!
	- Tim: ==Mix of INSERTION sort and MERGE sort. Optimizes runs of data!!==
		- Average Complexity: O(n log n)
		- Worst Complexity: O(n log n)
		- Average Memory: O(n)
		- Worst Memory: O(n)
		- STABLE
- Be prepared to code:
	- Bubble:
	```cpp
	void Bubble<T>::runSort() {
	  for (unsigned int round = 0; round < this->capacity - 1; round++) {
	    for (unsigned int i = 0; i < this->capacity - 1 - round; i++) {
	      if (this->arr[i + 1] < this->arr[i]) {
	        T temp = this->arr[i];
	        this->arr[i] = this->arr[i + 1];
	        this->arr[i + 1] = temp;
	      }
	    }
	  }
	}
	```
	- Selection:
	```cpp
	void Selection<T>::runSort() {
		for (unsigned int i = 0; i < this->capacity - 1; i++) {
			for (unsigned int j = i + 1; j < this->capacity; j++) {
				if (this->arr[j] < this->arr[i]) {
					T temp = this->arr[i];
					this->arr[i] = this->arr[j];
					this->arr[j] = temp;
				}
			}
		}
	}
	```
	- Insertion:
	```cpp
	void Insertion<T>::runSort() {
		for (unsigned int i = 1; i < this->capacity; i++) {
			unsigned int j = i;
			while (j > 0 && this->arr[j] < this->arr[j - 1]) {
				T temp = this->arr[j];
				this->arr[j] = this->arr[j - 1];
				this->arr[j - 1] = temp;
				j--;
			}
		}
	}
	```
- What is bucket sort?
	- Bucket sort is a sorting technique where values in a list are separated into buckets of data which are then sorted with another algorithm. When all buckets are sorted, they are collected together in a orderly fashion. 
- What is a stable sort?
	- Like Phone book where last name is sorted first then first name.
	- ==Stable means it doesn't mix up data that have the same values==
- what is max heap? how do you find children given an index?
	- Max heap is when all parents are bigger than their children. You can find left-children by 2n+1 and right-children by 2n+2. To find parent you use (n-1)/2