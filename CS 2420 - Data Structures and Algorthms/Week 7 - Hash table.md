Array-based (closed hashing, open addressing)
Quadratic probing
Liked list-based (open hashing, closed addressing)

Goal: ==finding data quickly, in O(1) time==
- usually meant for key/value pairs
- Fair, one item shouldn't be much longer to find
- We take keys of any type

#### Array-based Hash Table:
![[Pasted image 20231010180346.png]]
steps:
1. hash key 
2. mod by 10 (or whatever length of array)
3. go to index
4. if status in use
	1. ==Linear Probing== move down until you find the first open slot
5. else
	1. put key and value in index

Get data steps:
1. hash key
2. mod hashed key
3. locate the int in the array 
4. if key matches
	1. return value
5. else
	1. (Linear Probing) keep moving down index to find key 

==Avg lookup: O\(1)
Avg insertion: O\(1)
Avg Deletion: O\(1)==

Worst Case: O\(n)
- the adversary/jerk choses worst possible keys
- the hash table fills up
- bad luck
- frequent insertions and deletion 

#### Linked List-Based Hash Table:
![[Pasted image 20231010183131.png]]
![[Pasted image 20231010183915.png]]
## Array based hash table:
---
```cpp
#include <iostream>
#include <string>
#include <utility>
#include <finctional>

using std::cin;
using std::cout;
using std::endl;
using std::string;
using std::pair;

int main() {

	HashTable<string, string> myHashTable(10);

	myHashTable.create("Snufkin", "She-Hulk");
	myHashTable.create("Rock", "Qucksilver");
	myHashTable.create("Brad", "Black Widow");
	myHashTable.create("Burning Building", "Captain America");
	myHashTable.create("Castadon", "Black Bolt");
	myHashTable.create("Maze38", "Daredevil");

	cout << myHashTable.retrieve("Burning Building") << endl;
	myHashTable.destroy("Burning Building");
	if (myHashTable.exists("Burning Building")) {
		cout << myHashTable.retrieve("Burning Building") << endl;
	}
	cout << myHashTable.retrieve("Brad") << endl;
	cout << myHashTable.retrieve("Snufkin") << endl;

	cin.git();
	return 0;
}

```

Class:
```cpp
template <typename T, typename U>
class HashTable {
public:
	HashTable(const int capacity);
	~HashTable();
	void create(const T& key, const U& value);
	U retrieve(const T& key) const;
	void distroy(const T& key);
	bool exists(const T& key) const;
private:
	int* statusArray{ nullptr };
	pair<T, U>* kvArray{ nullptr };	
	int capacity{ 10 };
};
```

#### Constructor:
```cpp
template <typename T, typename U>
HashTable<T, U>::HashTable(const int capacity) {
	this->capacity = capacity;
	this->statusArray = new int[capacity];
	for (int i = 0; i < capacity; i++) {
		statusArray[i] = 0;
	}
	this->kvArray = new pair<T, U>[capacity];
}
```

#### Destructor:
```cpp
template <typename T, typename U>
HashTable<T, U>::~HashTable() {
	delete[] this->statusArray;
	delete[] this->kvArray;
}
```

## Create Method:
---
declairation:
```cpp
void create(const T& key, const U& value);
```

definition:
```cpp
template <typename T, typename U>
void HashTable<T, U>::create(const T& key, const U& value) {
	// Step 1, Hash the key, mod by capacity. Obtain an index
	// While loop as long as you haven't iterated capacity times
		// Step 2, Go to the status array at that index.
		// if the status array is 0 or -1, write the pair at this index
		// Else if the status array is 1, linear probe to the next index
	auto hashedIndex = std::hash<T>{}(key) % capacity;
	int counter{ 0 };
	while (counter < capacity) {
	// Assume the while loop was coded...
		if (satusArray[hashedIndex] == -1 || statusArray[hashedIndex] == 0){
			// Use this slot
			kvArray[hashedIndex] = pair<T, U>(key, value);
			statusArray[hashedIndex] = 1;
			return;
		} 
		else {
			counter++;
			hashedIndex = (hashedIndex + 1) % capacity; // wrap around
		}
	}
}
```
oct 10: 744193

## Retrieve Method:
---
declaration:
```cpp
U retrieve(const T& key) const;
```

Definition:
```cpp
template <typename T, typename U>
U HashTable<T, U>::retrieve(const T& key) const {
	auto hashedIndex = std::hash<T>{}(key) % capacity;
	int counter{ 0 };
	while (counter < capacity) {
		if (statusArray[hashedIndex] == 1) {
			if (kvArray[hashedIndex].first == key) {
				return kvArray[hashedIndex].second;
			} else {
				counter++;
				hashedIndex = (hashedIndex + 1) % capacity;
			}
		} else if (statusArray[hashedIndex] == -1) {
			counter++;
			hashedIndex = (hashedIndex + 1) % capacity;
		} else {
			throw 1;
		}
	}
	throw 1;
}
```
Step 1, Hash the key, mod by capacity
while counter isn't capacity
Go to that slot in status array,
If status is 1, 
If the pair's key for a mach with parameter's key
return pair's value
Else
increment both counter and hashedIndex (wrap around)
If status is -1,
Linear probe
If status is 0
Stop looking, this key isn't in the hash table
throw error

## Overloaded \[] :
---
Declaration:
```cpp
U operator[](const T& key) const;
```

Definition:
```cpp
template <typename T, typename U>
U& HashTable<T, U>::operator[](const T& key) const {
	auto hashedIndex = std::hash<T>{}(key) % capacity;
	int counter{ 0 };
	while (counter < capacity) {
		if (statusArray[hashedIndex] == 1) {
			if (kvArray[hashedIndex].first == key) {
				return kvArray[hashedIndex].second;
			} else {
				counter++;
				hashedIndex = (hashedIndex + 1) % capacity;
			}
		} else if (statusArray[hashedIndex] == -1) {
			counter++;
			hashedIndex = (hashedIndex + 1) % capacity;
		} else {
			throw 1;
		}
	}
	throw 1;
}
```

## Automatically resizing hash table:
---
For example, a 5th element into a hash table with capacity 10.

- If inserting an item would make it at least 50% full, then resize the hash table bigger
- Creating room for twice as many elements
- Then go through the existing hash table arrays, one by one, finding anything with a status array of 1 (you should find 4 in this example)
- Put that key/value pair into the larger arrays. This means you have to rehash every key/value pair. So a key would be hashed and modded by 20. Then insert into that hash table following hash table rules
- When you are done copying those 4 elements over, add the 5th element (the one you were originally going to add in)
- Delete your old arrays
- Set the your arrays to point to the new arrays

## Move assignment:
---
Oct 12: 206435

```cpp
if (&obj != this ) {
	// Continue with the move
	if ( this->keyValueArray ) {
		// delete the two arrays
	}
	// Do the 8 lines of moving logic
}
return *this;

```

## Resize :
---
check to see if count is half way to capacity:
```cpp
if ((count + 1.0) / capacity >= 0.5) {
	HashTable(capacity*2);
	while this->status
		*this.create(
}
```

```cpp

```