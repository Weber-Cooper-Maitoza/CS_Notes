![[Pasted image 20231019180033.png]]
Quadratic Probing:
==Better performance at high loads than linear probing==
- capacity is always a prime number
- is must be congruent with ==3 mod   4 (19/4 gives remainder of 3)==
- alternate negative and positive to go forward and backwards.

Double Hashing:

Robin Hood Hashing:

Cuckoo Hashing:


## Linked List Hash Tables:
---
![[Pasted image 20231019184408.png]]
C.R.U.D.
- C-reate
- R-etrive
- U-pdate
- D-elete

```cpp
#include <forward_list>
#include <memory>
using std::forward_list;
using std::unique_ptr;

```

Class:
```cpp
template <typename K, typename V>
class HashTable {
public:
	HashTable(const int capacity);
	~HashTable();
	void create(const K& key, const V& value);
	U retrieve(const K& key) const;
	U& operator[](const K& key) const;
	void distroy(const K& key);
	bool exists(const K& key) const;
private:
	unique_ptr<forwars_list<pair<K, V>>[]> keyValueArray;
	int capacity{ 10 };
	int count{ 0 };
};
```

Unique Constructor:
```cpp
template <typename K, typename V>
HashTable<K, V>::HashTable(const int capacity) {
	this->capacity = capacity;
	this->keyValueArray = make_unique<forwars_list<pair<K, V>>[]>(capacity);
}
```

==DOSENT NEED DISTRUCTOR==

Create Method:
```cpp
template <typename K, typename V>
void HashTable<K, V>::create(const K& key, const V& value){
	auto hashedIndex = std::hash{}(key) % capacity;
	// keyValueArray[hashedIndex].push_front(pair<K, V>(key, value));
	keyValueArray[hashedIndex].emplace_font(key, std::move(value));
}
```

Retrieve method:
```cpp
template <typename K, typename V>
V HashTable<K, V>::retrieve(cosnt K& key) const {
	auto hashedIndex = std::hash{}(key) % capacity;
	for(auto& keyValue : keyValueArray[hashedIndex]){
		if (keyValue.first == key) {
			return keyValue.second;
		}
	}
}
```

Move Constructor:
```cpp
template <typename K, typename V>
HashTable<K, V>::HashTable(HashTable<K, V>&& objToMove) {
	this->capacity = objToMove.capacity;
	objToMove.capacity = 0;
	this->count = objToMove.count;
	objToMove.count = 0;
	this->keyValArray = std::move(objToMove.keyValArray);
}
```
Oct 19: 342769