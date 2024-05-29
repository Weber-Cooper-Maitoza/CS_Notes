## Shared Pointers:
Reduce performance but you wont mess up.

- cleans up 
- checks references 

Needs to include `#include <memory>`
You can use `std::shared_ptr` and `std::make_shared`

```cpp
shared_ptr<int[]> myArray = make_shared<int[]>(10);

```

this counts how many references are sharing that memory address.

```cpp
shared_ptr<int[]> anotherRefToMyArray = myArray; // shares myArray address
myArray.reset(); // looses all references to the original pointer.
```

Old Way:
```cpp
int* myArray = new int[10];
delete[] myArray;
myArray = nullptr;
```

## Copy Assignment:

```cpp
SafeArray {
public:
	SafeArray& operator=(const SafeArray<T>& objToClone);
}
```

```cpp
template <typename T>
SafeArray<T>& SafeArray<T>::operator=(const SafeArray<T>& objToClone) {
	// Make sure i'm not my self
	if (this == &objToClone) { // makes sure they arent the same address
		// DO Nothing
		return *this; // Dereference object
	}

	// What if I have an Array already?
	if ( this->arr ) { // if non 0 == true
		delete[] this->arr;
		this->arr = nullptr;
	}
	
	this->capacity = objToClone.capacity; // Assigns the new object's capacity the clones capacity.
	this->arr = new T[this->capacity];
	for (int i = 0; i < this->capacity; i++) {
		this->arr[i] = objToClone.arr[i];
	}

	return *this; // returns the object itself
}
```
`if ( this->arr ) ` means if `this->arr` != 0 then `true`

The decoration has to have a pass-by-reference for object: `SafeArray<T>&`.

```cpp
SafeArray<int> myContainer(10);

SafeArray<int> cloneObj = myContainer;
```
## Copy Constructor:

Declaration:
```cpp
class SafeArray {
public:
	SafeArray(const SafeArray<T>& objToClone); // copy Constructor
	//SafeArray(const SafeArray<T>& objToClone) = delete; disables
}
```

Definition:
```cpp
template <typename T>
SafeArray<T>::SafeArray(const SafeArray<T>& objToClone) {

	// The left side, the new object, is the "this"
	// The right side, the object to clone, is the "objToClone"
	this->capacity = objToClone.capacity;
	this->arr = new T[this->capacity];
	for (int i = 0; i < this->capacity; i++) {
		this->arr[i] = objToClone.arr[i];
	}
 // ### MYBE MISSING SOMETHING ###
}
```

Call:
```cpp
SafeArray<int> myCopy( myContainter );
```

## Queues:
---
Stacks: Last In First Out (LIFO)

Queues: First In First Out (FIFO) 
like a line of people
`[] [] [] [] []`

usually has these methods:
- int .size()
- int .capacity()
- void .push_back()
- void .pop_font()
- T .back()
- T .front()

"Loop" line when line if full

numItems: number of items used
frontIndex: front of the line
backIndex: back of the line
capacity: size of the line

back
if empty, throw error
if backIndex = 0 and isnt empty, return -1
else ????

push back:
check =  am I full
if backIndex == 0 and isnt empty, get value at -1 (the back of line)
arr\[backIndex\] = value;
backIndex++;
numItems++;

pop front:
check = am I empty
frontIndex++;
numItems--;

Sep 7: 8675309


