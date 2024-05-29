## Using copy constructor in linked lists:
---
call:
```cpp
  myList.push_back('a');
  myList.push_back('b');
  myList.push_back('c');
  myList.push_front('y');
  myList.push_front('z');
  // z y a b c
  
  LinkedList<char> myCopy(myList); // Invokes a copy constructor
```

declaration:
```cpp
// Needs a default constructor
LinkedList() { cout << "This constuctor did nothing" << endl; }
LinkedList(const LinkedList<T>& that);
```

definition:
```cpp
template<typename T>
LinkedList<T>::LinkedList(const LinkedList<T>& that) {
	// Check if empty
	if ( !that.head ) {
		return;
	}
	
	// Check if empty
	this->count = that.count;
	auto tempForThat = that.head;
	auto tempForThis = new Node<T>;
	this->head = tempForThis;
	
	while ( tempForThat ) {
	    // copy the node's data
	    tempForThis->data = tempForThat->data;
	    this->tail = tempForThis;
	    // move that pointer forward
	    tempForThat = tempForThat->link;
	    if (tempForThat) {
	      // we're still on a node in that
	      tempForThis = new Node<T>;
	      this->tail->link = tempForThis; 
	    }
	}
}
```
sep 19: 407376

## Copy Assignment:
---
Make clear method:
```cpp
public:
	void clear();

template <typename T>
void LinkedList<T>::clear() {
	while (this->head) {
		this->pop_front();
	}
}
```

calls:
```cpp
myAssignmentCopy.push_back('x');

myAssignmentCopy = myList;
myAssignmentCopy.operator=(myList); // compiler sees this
```

Declaration:
```cpp
LikedList<T>& operator=(const LinkedList<T>& that); // copy assignment
```

Definition:
```cpp
template <typename T>
LikedList<T>& LinkedList<T>::operator=(const LinkedList<T>& that) {
	// We're cloning that into this
	// Vertually all operator='s should check for 
	// 1) Is te this and the that the same object
	// 2) The this object already had stuff in it and needs to be cleared out first
	
	// Check if were copying ourself
	if ( this == &that ) {
		return *this; // Derefercing so we can chain up
	}

	// Check if this is full
	if ( this->head ) {
		this->clear();	
	}

	// Check if empty
	if ( !that.head ) {
		return;
	}
	
	// Check if empty
	this->count = that.count;
	auto tempForThat = that.head;
	auto tempForThis = new Node<T>;
	this->head = tempForThis;
	
	while ( tempForThat ) {
	    // copy the node's data
	    tempForThis->data = tempForThat->data;
	    this->tail = tempForThis;
	    // move that pointer forward
	    tempForThat = tempForThat->link;
	    if (tempForThat) {
	      // we're still on a node in that
	      tempForThis = new Node<T>;
	      this->tail->link = tempForThis; 
	    }
	}

	return *this;
}
```


## Movement concepts:
---
- L-value: have names
- R-Values: don't have names
```cpp
int x = 42
// x = L-value
// 42 = R-value
```
You only move R-values into L-values

Use:
```cpp
std::move();
```

## Move Constructor:
---
Call:
```cpp
LinkedList<char> myMoveObj(std::move(myList)); // Invokes a move constructor
```

Declaration:
```cpp
// LinkedList(const LinkedList<T>& that); // Copy Constructor (accepts L-Values)
LikedList(LinkedList<T>&& that); // Move Constructor (accepts R-values)
```

Deffinition:
```cpp
template <typename T>
LinkedList<T>::LinkedList(LinkedList<T>&& that) {
	this->count = that.count;
	that.count = 0;
	this->head = that.head;
	that.head = nullptr;
	this->tail = that.tail;
	that.tail = nullptr;
}
```

## Move assignment:
---
call:
```cpp
LinkedList<> myAssignemntMove;
myAssignmentMove.push_back('w');
myAssignmentMove = std::move(myMoveObj);
```

Declaration:
```cpp
LikedList<T>& operator=(LinkedList<T>&& that); // copy assignment
```

Definition:
```cpp
template <typename T>
LikedList<T>& LinkedList<T>::operator=(LinkedList<T>&& that) {
	// Check if were copying ourself
	if ( this == &that ) {
		return *this; // Derefercing so we can chain up
	}

	// Check if this is full
	if ( this->head ) {
		this->clear();	
	}

	this->count = that.count;
	that.count = 0;
	this->head = that.head;
	that.head = nullptr;
	this->tail = that.tail;
	that.tail = nullptr;

	return *this;
}
```

## Doubly Linked Lists
---
pointer going back and forwards
![[Pasted image 20230921185824.png]]
Definition:
```cpp
template <typename T>
struct Node {
  T data{};
  Node<T>* next{nullptr};
  Node<T>* prev{nullptr};
};

template <typename T>
class LinkedList {
public:
  LinkedList() {}
  ~LinkedList();

  LinkedList(const LinkedList<T>& that); // Copy constructor (accepts L-values)
  LinkedList(LinkedList<T>&& that); // Move constructor (accepts R-values)
  LinkedList<T>& operator=(const LinkedList<T>& that); // Copy assignment (accepts L-values)
  LinkedList<T>& operator=(LinkedList<T>&& that); // Move assignment (accepts R-values)

  void clear();

  void push_back(const T& data); // O(1)
  void push_front(const T& data); // O(1)
  void pop_front(); // O(1)
  void pop_back(); // O(1)

private:
  Node<T>* head{ nullptr };
  Node<T>* tail{ nullptr };
};
```

Methods:
```cpp
template <typename T>
void LinkedList<T>::push_back(const T& data) {
  // Error scenarios

  // Specific scenarios
  if (!this->head) {
    // The list is empty
    auto temp = new Node<T>;
    temp->data = data;
    this->head = temp;
    this->tail = temp;
    this->count++;
    return;
  }

  // General scenario
  auto temp = new Node<T>;
  temp->data = data;
  this->tail->next = temp;
  temp->prev = this->tail;
  this->tail = temp;
}


template <typename T>
void LinkedList<T>::push_front(const T& data) {
  // Error scenarios

  // Specific scenarios
  if (!this->head) {
    // The list is empty
    auto temp = new Node<T>;
    temp->data = data;
    this->head = temp;
    this->tail = temp;
    this->count++;
    return;
  }

  // General scenario
  auto temp = new Node<T>;
  temp->data = data;
  temp->next = this->head;
  this->head->prev = temp;
  this->head = temp;
}

template <typename T>
void LinkedList<T>::pop_front() {
  // Error sceanrios
  if ( !this->head ) {
    cout << "The list is already empty" << endl;
    return;
  }
  
  // Specific scenarios
  if ( head == tail ) {
    // One node scenario
    delete this->head;
    this->head = nullptr;
    this->tail = nullptr;
    return;
  }
  
  // General scenario
  Node<T>* temp{nullptr};
  temp = this->head;
  this->head = this->head->next;
  this->head->prev = nullptr;
  delete temp;
}


template <typename T>
void LinkedList<T>::pop_back() {
  // Error scenarios
  if (!this->head) {
    cout << "The list is already empty" << endl;
    return;
  }

  // Specific scenarios
  if (head == tail) {
    // One node scenario
    delete this->head;
    this->head = nullptr;
    this->tail = nullptr;
    this->count--;
    return;
  }

  // General scenario
  // Get a pointer to the second to last node
  Node<T>* temp {nullptr};
  temp = this->tail;
  this->tail = this->tail->prev;
  this->tail->next = nullptr;
  delete temp;
}
```
sep 21: 796b6f

