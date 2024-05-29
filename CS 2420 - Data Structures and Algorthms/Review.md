## Writing outside the blah
---
```cpp
#include <iostream>

using std::cout;
using std::cin;
using std::endl;

int main() {

  SafeArray<int> myContainter(10);

  myContainter.assign(2, 4);
  myContainter.assign(3, 9);
  myContainter.assign(4, 16);
  cout << "The containter at 4 has the value: " << myContainter.get(4) << endl;

  myContainter.assign(10, 666);

  cout << "The containter at index -1 has the value: " << myContainter.get(-1) << endl;
  
  cout << "Hello world" << endl;

  return 0;
}

```

BIGGEST PROBLEM IN THIS CLASS
```cpp
int* myArray = new int[1000000];
```
`new` is used to allocate space on the heap.
`int[1000000]` is the space and type that needs to be allocated on the heap.
stores the address in `myArray`.

CHANGE DATA ON THE HEAP:
```cpp
*myArray = 28
myArray[0] = 28;

*(myArray + 1) = 42;
myArray[1] = 42;
```

participation code: 46c79f
## C++ Review:
---
Pointers
arrays
dynamic allocation
classes and objects
error handling

```cpp
  int capacity{ 0 };
```
initializes the value of zero

```cpp
delete[] // = many things
```
#### Safe Array Code:
---
```cpp
#include <iostream>

using std::cout;
using std::cin;
using std::endl;

template <typename T>
class SafeArray {
public:
  SafeArray(const int capacity);
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
 
  //int* myArray = new int[1000000];
  //
  //myArray[0] = 28;
  //cout << myArray << endl;
  //cout << *myArray << endl;
  //cout << myArray[0] << endl;

 // SafeArray<string> myBooks(5);
  //myBooks.assign(0, "It was the best of times, it was the worst of times...");

  SafeArray<int> myContainer(10);
  
  myContainer.assign(2, 4);
  myContainer.assign(3, 9);
  myContainer.assign(4, 16);
 
  cout << "The container at 4 has the value: " << myContainer.get(4) << endl;

  myContainer.assign(10, 666);

  try {
    cout << "The container at index -1 has the value: " << myContainer.get(-1) << endl;
  }
  catch (int whateverError) {
    cout << "Someone used the ejection seat of throw, and the error code was " << whateverError << endl;
  }

  cin.get();
  return 0;
}
```

#### Stack Homework Assignment:
Last In First Out (LIFO)
top()
pop()
push()
size()

## push:

==write to array the value then increment index.==

```cpp
obj.push(a);


push {
	
}

```

## Day 3:
---
how to Dynamically allocate memory in C:
```c
int arrSize{ 0 };
int* myArray{ nullptr };

myArray = (int*)malloc(arraySize * sizeof(int));

// how to deallocate in C
free(myArray);
```

