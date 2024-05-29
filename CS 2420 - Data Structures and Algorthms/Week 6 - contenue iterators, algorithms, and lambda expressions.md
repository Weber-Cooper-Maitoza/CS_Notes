## Iterators for ==SafeArray==:
---
the goal of iterators is a consistent design pattern for containers.
Iterators mimic pointer arithmetic on arrays.

```cpp
for (auto iter = container.begin(); iter != container.end(); ++iter) {
	cout << *iter << endl;
}
```

`container.begain()` returns an iterator object.

```cpp
#include <iostream>
#include <string>

using std::cout;
using std::cin;
using std::endl;

template <typename T>
class SafeArray {
public:
  SafeArray(const int capacity);
  SafeArray& operator=(const SafeArray<T>& objToClone);
  ~SafeArray();
  void assign(const int index, const T& data);
  T get(const int index) const;
private:
  int capacity{ 0 };
  T* arr{ nullptr };
};

template <typename T>
SafeArray<T>::SafeArray(const int capacity) {
  this->arr = new T[capacity];
  this->capacity = capacity;
}

template <typename T>
SafeArray<T>& SafeArray<T>::operator=(const SafeArray<T>& objToClone) {

  // Make sure I'm not myself
  if (this == &objToClone) {
    // Do nothing
    return *this;

  }

  // TODO: What if "this" already had an array...

 
  // The left side, the new object, is the "this"
  // The right side, the object to clone, is objToClone
  this->capacity = objToClone.capacity;

  this->arr = new T[this->capacity];

  for (int i = 0; i < this->capacity; i++) {
    this->arr[i] = objToClone.arr[i];
  }
 
  
  return *this;


}

template <typename T>
SafeArray<T>::~SafeArray() {
  delete[] this->arr;
}

template <typename T>
void SafeArray<T>::assign(const int index, const T& data) {
  if (index >= capacity || index < 0) {
    cout << "You are looking nice today, but the index was out of bounds" << endl;
    return;
  }
  this->arr[index] = data;
}

template <typename T>
T SafeArray<T>::get(const int index) const {
  if (index >= capacity || index < 0) {
    cout << "Your index was bad, but you aren't" << endl;
    throw 1;
  }
  return this->arr[index];
}


int main() {
  cin.get();
  return 0;
}
```

### Class iterator: for safe array
```cpp
template <typename T> class SafeArray; 
// Forward declaration

template <typename T>
class Iterator {
// I want the safe array to see my private stuff
friend class SafeArray<T>;
public:
	T& operator*();
private:
	T* arr{ nullptr };
	int capacity{ 0 };
	int currIndex{ 0 };
};

template <typename T>
class SafeArray {
	
};
```

#### Begin method:
```cpp
Iterator<T> begain() const;
```

```cpp
template <typename t>
Iterator<T> SafeArray<T>::begain() const {
	Iterator<T> retVal; // Return Value Object
	retVal.arr = this->arr;
	retVal.capacity = this->capacity;
}
```

#### \* overload method:
```cpp
T& operator*();
```

```cpp
template<typename T> 
T& Iterator<T>::operator*() {
	return this->arr[currIndex];
}
```

#### != overload method:
```cpp
bool operator!=(const Iterator<T>& rightHandSide) const;
```

```cpp
template<typename T>
bool Iterator<T>::operator!=(const Iterator<T>& rightHandSide) const {
	if (this->arr != rightHandSide.arr || 
		this->currIndex != rightHandSide.currIndex) {
		return true;
	}
	return false;
}
```

#### ++ operator overload method:
```cpp
Iterator<T> operator++();
```

```cpp
template <typename T>
Iterator<T> Iterator<T>::operator++() {
	if (this->currIndex < this->capacity) {
		this->currIndex++;
	}
	return *this;
}
```

#### end() method:
```cpp
Iterator<T> end() const;
```

```cpp
template <typename t>
Iterator<T> SafeArray<T>::end() const {
	Iterator<T> retVal; // Return Value Object
	retVal.arr = this->arr;
	retVal.capacity = this->capacity;
### missed something
}
```
oct 3: 573910

### Iterators Cans and Cants:
Iterators Can:
- read data
- modify data

Iterators Can't:
- add values
- remove values

## Lambda:
---
define function on the fly

```cpp
[](){} // lambda exptression
```
`[]` - the capture
`()` - the parameter (passed into the lambda expression every time) (const string& wordToCheck)
`{}` - body of code (function)

## Hash Algorithm:
---
Need, good distribution

Encoding: can go back and forth


encrypting / decrypting: input and secret get encrypted output
![[Pasted image 20231005185039.png]]
Hashing: data only gets hashed one way, cant go back
![[Pasted image 20231005184828.png]]

#### Good hashing algorithms:
- fast
- reasonably well distributed
- takes a long time to compute

### SHA-256:
a hash algorithm 

Hash Collisions:
hash(A) -> output <- hash(B)

### The array approach:
3 arrays of the same size

==closed hashing==
open addressing
- fast
- annoying design issues

Example:
![[Pasted image 20231005191134.png]]

### Linked list approach:
one array of multiple linked lists
==Open hashing==
open hashing
- shower 
- clean design

Example:
oct 5: 543281