## Big-O Notation:
---
A way of describing algorithms.
Big-O describes asymptotic bounding when its input gets large.

Big-O = upper bound
Big-Ω = Lower Bound
Big-Ø = both upper and lower are the same

Order of algorithm class:
1. O(1) - constant time, not dependent on size of input
2. O(log n) - Divide and conquer 
3. O(n) - loop n iterations 
4. O(n log n) - outer loop with a divide and conquer 
5. O(n^2) - outer loop with inner loop `for (int i = 0;...){ for (int i = 0:...) {single line of code}}`
6. O(n^3) - outer, middle, and inner loop on `n`.
7. O(2^n) - brute force 
8. O(n\*n!) - just a joke 

Stack:
- array based 
- push - O(1)
- pop - O(1)
- top - O(1)

Queue:
- array based 
- push_back - O(1)
- pop_front - O(1)
- back - O(1)
- front - O(1)
- copy constructor - O(n) : ==because it loops `n` times==

## Linked Lists:
---
a single container with data and a pointer is called a ==node==

Arrays:
- Good:
	- everything Linked Lists are bad at
- Bad
	- everything Linked Lists are good at

Linked lists:
- Good:
	- Remove Items
	- Add items on ends
	- Add items in the middle
	- Circular
	- Reorder
	- no fixed limit
	- good with memory fragmentation
	- cant goes out of bounds
	- Know their own size
- Bad:
	- Not random Access 
	- Can't easily iterate backwards
	- Much slower than arrays; bad caching and locality
	- Always have memory overhead for pointers
	- struggles in safe memory languages

Skeleton:
```cpp
#include <iostream>

template <typename T>
struct Node {
  T data{};
  Node<T>* link{nullptr};
};

template <typename T>
class LinkedList {
public:
	//~LinkedList();
private:
  Node<T>* front{ nullptr };
  Node<T>* back{nullptr};
  int count{ 0 };
};
```
sep 12: 314159

Two containers:
- Node Struct: for the actual node
- LinkedList Class: to control how the nodes interact

Node Struct:
```cpp
template <typename T>
struct Node {
  T data{};
  Node<T>* link{nullptr};
};
```

Linked List Class:
```cpp
template <typename T>
class LinkedList {
public:
private:
  Node<T>* head{ nullptr };
  Node<T>* tail{ nullptr };
  int count{ 0 };
};
```

User should ==only interact with the linked list class== and not the Node Struct.

#### Calls:
---
```cpp
int main() {
	LinkedList<char> myList;
	myList.push_back('a');	
	myList.push_back('b');	
	myList.push_back('c');	
	myList.push_back('y');	
	myList.push_back('z');	
	cout << "Front: " << myList.front() << endl;
	cout << "Back: " << myList.back() << endl;
	cout << "This list has this many items: " << myList.size() << endl;
	myList.pop_front();
	myList.pop_front();
	myList.pop_back();
	myList.pop_back();
	myList.pop_back();
	myList.pop_back();
	myList.pop_back();
	myList.pop_back();

	cin.get();

	return 0;
}
```

#### Methods:
---
Three step process:
1. error scenarios 
2. specific scenarios
3. General scenarios

##### push_back():
```cpp
public:
	void push_back(const T& data);

template <typename T>
void LinkedList<t>::push_back(const T& data) {
	// 1. error scenarios
		// None
	// 2. specific scenarios
	if ( !head ) { 
		// The list is empty
		Node<T>* temp = new Node<T>;
		temp->data = data;
		this->head = temp;
		this->tail = temp;
		this->cout++;
		return;
	}
	
	// 3. General scenarios
	auto temp = new Node<T>;
	temp->data = data;
	this->tail->link = temp; // the node in front points to next node
	this->tail = temp;
	count++;
}
```

##### Push_Front()
---
```cpp
public:
	void push_front(const T& data);

template <typename T>
void LinkedList<t>::push_front(const T& data) {
	// 1. error scenarios
		
	// 2. specific scenarios
	if ( !head ) { 
		// The list is empty
		Node<T>* temp = new Node<T>;
		temp->data = data;
		this->head = temp;
		this->tail = temp;
		this->cout++;
		return;
	}
	
	// 3. General scenarios
	Auto temp = new Node<T>;
	temp->data = data;
	temp->link = this->head; 
	this->head = temp;
	this->count++;
}
```

#### Pop_Front():
---
```cpp
public:
	void pop_front();


template <typename T>
void LinkedList<t>::pop_front() {
	// 1. error scenarios
	if ( !this->head ) {
		cout << "This list is empty." << endl;
		return;
	}

	// 2. specific scenarios
	if ( head == tail ) {
		// One node scenario
		delete this->head;
		this->head = nullptr;
		this->tail = nullptr;
		this->count--;
		return;
	}

	// 3. General scenarios
	// Node<T> temp{ nullptr };
	//temp = this->head;
	auto temp = this->head;
	this->head = this->head->link;
	delete temp;
	count--;
	
```

#### pop_Back():
---
```cpp
public:
	void pop_back();


template <typename T>
void LinkedList<t>::pop_back() {
	// 1. error scenarios
	if ( !this->head ) {
		cout << "This list is empty." << endl;
		return;
	}

	// 2. specific scenarios
	if ( head == tail ) {
		// One node scenario
		delete this->head;
		this->head = nullptr;
		this->tail = nullptr;
		this->count--;
		return;
	}

	// 3. General scenarios
	// Get pointer to second to last node
	auto temp = this->head;
	while (temp->link != this->tail) {
		temp = temp->link;
	}	
	// temp is at the second to last node
	delete this->tail;
	this->tail = temp;
	this->tail->link = nullptr;
	this->count--;
}
```
sep 14: 452839