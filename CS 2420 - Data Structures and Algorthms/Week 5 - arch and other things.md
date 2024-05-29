## Caching:
---
==Linked Lists are terrible with Cache.
Arrays are best with cache.==

## Branching:
---
==dependably either true or false== so that the computer can predict (Speciultive prediction) what the branch will do.

sep 26: 254872


## Iterators:
---
Standarized so that iterators can walk down both vectors, arrays, and linked lists

#### Problem: Iterate through containers:
How do you walk down every value 

IDK what this is:
```cpp
#include <forward_list>
#include <list>
#include <map>
#include <vector>
#include <iostream>
#include <string>

using std::forward_list;
using std::list;
using std::map;
using std::vector;
using std::cin;
using std::cout;
using std::endl;
using std::string;

int main() {
	vector<char> myVector;
	for (char c = 'a'; c <= 'j'; c++) {
		myVector.push_back(c);
	}
	
	// with iterators, the C++98 way
	for(vector<char>::const_iterator iter = myVector.begin(); 
		iter != myVector.end(); 
		++iter) {
		cout << *iter << " ";
	}

	cout << endl;

	// C++ 11 way
	for (auto item : myVector) {
		cout << item << " ";
	}
	cout << endl;

	// Iterators in Doubly Liked Lists
	// Iterate backwars
	auto iter = myList.end(); 
	// iter is pointing to one point past 'j'
	--iter;
	cout << *iter << endl;
	--iter;
	// iter is pointing to 'i'
	
	cin.get();
	return 0;
}
```


Use `#include <algorithm>` to use iterators to shuffle or randomize items
sep 28: 713642



