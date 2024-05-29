Next Topic: [[12 - Multi Class Programs]]

What is a pointer?
- A variable that stores a memory address

*"think of a shortcut on windows"*

Whats the *"point"* of pointers?

1. Allocate objects on the *Heap*
2. Pass functions to other functions
3. Iterate over elements in arrays and other data structures
4. Memory management (pass-by-value (&), pass-by-pointer(*))

Variables:
1. Name (defined by programmers)
2. Content (may vary)
3. Address in memory (RAM)

*"Pointers point to a memory address"*

#### Stack v.s. Heap:
---
- Static Allocation (Compile time): Stack
```cpp
int dataset[100];
int index = 0;
```

- Dynamic Allocation (runtime): Heap
```cpp
int count;
count << "How many items on dataset?";
cin >> count;

int* dataset = new int[count]; // heap
```

#### Six Operators of Pointers:
---
1. `new` - Defines on heap
2. `delete` - Reallocate heap space
3. `->` - Member access operator
4. `&` - Address of operator
5. `*` - pointer definition
6. `*` - dereference operator *"GETS the contents"*

```cpp
int i; // Variable used to store an integer
int* p; // pointer to store an address of an integer

i = 9; // Stores integer i
p = &i; // stores address of i

*p = 15; // DEREFERENCING // Reassignes 'i' to 15 

// cout << i << endl; // OUTPUT: 9
// cout << &i << endl; // OUTPUT: 0000003FC39 'THE EXACT SAME'
// cout << p << endl; // OUTPUT: 0000003FC39

// cout << *p << endl; // DEREFERENCE // OUTPUT: 9  //GETS THE CONTENTS
```

#### `new` and `delete`:
```cpp
class Person {
	
};

int main () {
	Person person; // Defined on stack
	Person* personPointer = new Person; // Defined on heap

	delete personPointer; // DEALOCATED 
}
```

Stack:
- Memory allocated on top 
- LIFO (Last in , first out)
- Automatic variables (known at compile time)

Heap:
- Memory allocation anywhere
- Heap can have "holes"
- Slower than stack


Common delete errors:
```cpp
	Person* p1; // not initilized (and p1 is on stack)
	// Person* p1 = new Person; // will work
	delete p1; // doesn't have anything to delete 
```

```cpp
Person p2 = Person(); // on stack
Person* pointer2 = &p2; // references on stack
delete pointer2; // WONT DELETE ON STACK (ONLY ON STACK)
```


```cpp
struct Person {
	string name = "jonny";
}

int main() {
	Person sPerson = { "Jimmy" }; // on stack
	cout << sPerson.name << endl;

	Person* sPointer = new Person { "Jacob" }; // on heap
	cout << (*sPointer).name << endl; // dereferences address and pulls content
	cout << sPointer->name << endl; // -> Member access operators
	delete sPointer;
}
```

`->` is a member access operator same as `Person.name` 

#### Relational Operators:
---
```cpp
int i1 = 64; // diffrent address location
int i2 = 64; // diffrent address location

int* ip1 = &i1;
int* ip2 = &i2;

if (ip1 == ip2)
	cout << "i1 and i2 are same location" << endl;
else
	cout << "i1 and i2 are NOT the same location" << endl;

// OUTPUT: i1 and i2 are NOT the same location
```

#### Arrays and Pointers:
---
```cpp
int n[] = { 2, 4, 6, 8, 10, 12 }; // 4 bytes (32-bits)
cout << n << endl; // OUTPUT: memory address

cout << n + 0 << endl; // memory address
cout << n + 1 << endl; // memory address
cout << n + 2 << endl; // memory address
// counts by 4 bytes in hex

string names[] = {"John", "Jacob", "Jingle", "Hymer", "Smith"}; // 28 bytes
cout << *(names + 0) << endl; // counts by 28 bytes
cout << *(names + 1) << endl;
cout << *(names + 2) << endl;
// should deallocate addresses and return contents

for (int i = 0; i < 5; i++) {
	cout << *(names + i) << endl;
}
// returns list of names
```

#### Null Pointer: *can set nullptr in the event data is not known*
---
```cpp
// define a pointer now and initilize it later
Person* person = nullptr; 

if (person != nullptr)
	cout << person->name << endl;

```

#### Pass-by-pointer function calls:
---
Doesnt work;
```cpp
void addFive(int n) {
	n += 5;
}

int main () {
	int n = 10;
	addFive(n); // want to add 5 to 10
	cout << n << endl; // OUTPUT: 10 "DOESN'T WORK"
}
```

Pass-by-reference:
```cpp
void addFive(int &n) { // Pass-By-Refference
	n += 5;
}

int main () {
	int n = 10;
	addFive(n); 
	cout << n << endl; 
}
```

Pass-by-pointer:
```cpp
void addFive(int* n) { // takes a memory address 
	*n += 5; // dereference memory address
}

int main () {
	int n = 10;
	addFive(&n); // address of n
	cout << n << endl; 
}
```

Pass-by-pointer object/struct:
```cpp
void print(Person* person) {
	cout << "Name: " << person->name << endl;
}

void read(Person* person) {
	cout << "Enter a name: ";
	cin >> person->name; // same as dereferencing memory address "*n"
}

int main() {
	Person person() = { "Johnny" };
	read(&person);
	print(&person); 
}
```

#### Pass Functions to Other Functions:
---
```cpp
int add(int a, int b) {
	return a + b;
}

int subtract(int a, int b) {
	return a - b;
}

int mult(int a, int b) {
	return a * b;
}

int divide(int a, int b) {
	return a / b;
}

int compute(int(*temp)(int, int), int a, int b) { // temp is funtion name
	return op(a, b);
} 

int main () 
{
	int a = 10;
	int b = 5;

	cout << compute(add, a, b); << endl;
	cout << compute(subtract, a, b); << endl;
	cout << compute(mult, a, b); << endl;
	cout << compute(divide, a, b); << endl;
}
```

#### Arrays of Objects with Pointers:
---
```cpp
class Student {
private:
	int id;
	string name = "Smithy";
	double gpa;

public:
	string getName() {
		return name;	
	}
}
```

##### #1 - Array of 10 objects:
```cpp
int main () 
{
	Student studentA[10]; // All student objects on stack
}
```

##### #2 - Pointer to array of 10 objects:
```cpp
int main () 
{
	Student* studentB; // Pointer on stack 
	student B = new Student[10]; // Student objects on heap
}
```

##### #3 - Array of 10 pointers: 
```cpp
int main () 
{
	Student* studentC[10]; // Pointers on the stack
	for (int i = 0; i < 10; i++) 
		studentC[i] = new Student; // Student on the heap
	cout << studentC[0]->getName() << endl	
	cout << (*studentC[0]).getName() << endl	
}
```

##### #4 - Pointer to an array of 10 pointer:
```cpp
int main () 
{
	Student** studentD; // Pointer on stack
	studentD = new Student*[10]; // Pointers on heap
	for (int i = 0; i < 10; i++) 
		studentD[i] = new Student; // Students no heap
}
```

#### Functional Example of Pointers:
---
Stack (Linked-list) - LIFO (last-in-first-out):
```cpp
#include <iostream>
using namespace std;

struct Node {
  string data;
  Node* nextPointer;
};

class Stack {
private:
  Node* topPointer;

public:
  Stack() {
    topPointer = nullptr;
  }

  // Destructor: Deletes all remaning data on heap once out of scope
  ~Stack() {
    while (!isEmpty()) {
      pop();
    }
  }

  // Add data to the stack
  void push(string data) {
    // create a new node
    Node* nodePointer = new Node; 
    nodePointer->data = data;
    nodePointer->nextPointer = nullptr;

    // If empty, add new node
    if (isEmpty()) {
      topPointer = nodePointer;
    }
    // Otherwise, add the new node to the top and change new node pointer
    else {
      // New node next points to "old" top
      nodePointer->nextPointer = topPointer;
      // Top pointer points to "new" top (new node)
      topPointer = nodePointer;
    }
  }

  // Look at the top item
  string peek() {
    return topPointer->data;
  }

  // Remove top item
  void pop() {
    if (!isEmpty()) {
      // Store top plate in temp
      Node* temp = topPointer;
      // Move top pointer to next "plate" down
      topPointer = topPointer->nextPointer;
      // Delete "old" top plate
      delete temp;
    }
  }

  bool isEmpty() {
    return topPointer == nullptr; // evaluates only if true
  }

  // Look at all items on stack
  void print() {
    if (!isEmpty()) {
      Node* temp = topPointer;
      while (temp != nullptr) {
        cout << "[" << temp->data << "]" << endl;
        temp = temp->nextPointer;
      }
      cout << endl;
    }
  }
};

int main () 
{
  Stack stack;

  stack.push("Star Trek");
  stack.push("Star Wars");
  stack.push("Red Dwarf");
  stack.push("Game of Thrones");
  
  stack.print();
  // cout << stack.peek();
  // stack.pop();
  // stack.print();
}
```

convert this notation:
```cpp
Node* nodePointer = new Node{ data, nullptr };
```

to This:
```cpp
Node* nodePointer = new Node; 
nodePointer->data = data;
nodePointer->nextPointer = nullptr;
```

Destructor: *destroys all nodes once out of scope*
```cpp
~Stack() {
	while (!isEmpty()) {
      pop();
    }
}
```
