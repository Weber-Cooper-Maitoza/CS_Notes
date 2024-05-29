Search algorithms:
- unsorted
- sorted 
- hash

What does ==Stable== mean? (nothing to do with crashing programs)
- ==Doesn't allow items to jump out of position==
- phone book sorting 
	- first sort by first names
	- then by last name
	
Big-O upper bound
Big-(omega) lower bound

Big-(Theta) is when both the Big-O and Big-(omega) are the same
![[Pasted image 20231024183332.png]]
Sort algorithms we will do:
- Bubble
- Selection
- Insertion
- Quick 
- Merge
- Heap
- Tim
- Bucket sort
- Bogo sort
#### code:
```cpp
#include <iostream>
#include <random>
#include <chrono>

using std::cout;
using std::cin;
using std::endl;
using std::string;

template <typename T>
class BaseSort {
public:
  BaseSort(const string& name, const unsigned int capacity);
  ~BaseSort();
  string getName() const { return name; }
  void loadRandomValues();
  void printValues() const;
  bool verifySort() const;
  
  virtual void runSort() = 0;  // A pure virtual function
                               // C++'s crazy way to say this class is abstract
                               // meaning this class can be inherited, but not instantiated

protected:
  string name;
  T* arr{ nullptr };
  unsigned int capacity{ 0 };
};

template <typename T>
BaseSort<T>::BaseSort(const string& name, const unsigned int capacity) {
  this->name = name;
  this->capacity = capacity;
  this->arr = new T[capacity];
}

template <typename T>
BaseSort<T>::~BaseSort() {
  delete[] arr;
}

template <typename T>
void BaseSort<T>::loadRandomValues() {
  std::random_device rd;  //Will be used to obtain a seed for the random number engine
  std::mt19937 gen(rd()); //Standard mersenne_twister_engine seeded with rd()
  std::uniform_int_distribution<unsigned int> distrib(0, 0xffffffffui32);

  for (unsigned int i = 0; i < capacity; ++i) {
    this->arr[i] = distrib(gen);
  }
}

template <typename T>
void BaseSort<T>::printValues() const {
  if (capacity < 50) {
    for (unsigned int i = 0; i < capacity; i++) {
      cout << arr[i] << " ";
    }
    cout << endl;
  }
}

template <typename T>
bool BaseSort<T>::verifySort() const {
  for (unsigned int i = 0; i < capacity - 1; i++) {
    if (arr[i + 1] < arr[i]) {
      cout << "Not sorted at index: " << (i + 1) << endl;
      return false;
    }
  }
  cout << "Sorted!" << endl;
  return true;
}

template <typename T>
class Bubble : public BaseSort<T> {
public:
  Bubble(const unsigned int capacity) : BaseSort<T>("Bubble", capacity) {}
  void runSort();
private:

};

template <typename T>
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

template <typename T>
void runMySort(BaseSort<T>&& sortObj) {
  cout << "Running sort: " << sortObj.getName() << endl;
  sortObj.loadRandomValues();
  sortObj.printValues();
  auto t1 = std::chrono::high_resolution_clock::now();
  sortObj.runSort();
  auto t2 = std::chrono::high_resolution_clock::now();

  sortObj.printValues();
  sortObj.verifySort();
  std::chrono::duration<double, std::milli> fp_ms = t2 - t1;
  std::cout << "Sort completed in " << fp_ms.count() << " milliseconds" << endl;
}

int main() {
  //BaseSort<int> forbidden(666);

  runMySort(Bubble<unsigned int>(20000));
  runMySort(Bubble<unsigned int>(40000));
  runMySort(Bubble<unsigned int>(80000));
  runMySort(Bubble<unsigned int>(160000));

  //runMySort(Selection<unsigned int>(20000));
  //runMySort(Insertion<unsigned int>(20000));

  cin.get();
  return 0;
  
}
```


Virtual:
```cpp
	virtual void runSort() = 0; 
```
- a pure virtual function
- meaning this class can be inherited, but not instantiated
Oct 24: ABCDEF

#### Bubble Sort:
- Compare pairs of values then swap the larger to the right. Repeat for each pair. Repeat for all pairs until the largest value has "bubbled" to the right.
- ﻿﻿Repeat prior algorithm to find the second largest number, then third largest number, etc.
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

```cpp
(unsigned int round = 0; round < this->capacity - 1; round++) 
```
`this->capacity - 1` means that the left most number doesn't need to be sorted 

performance = ==O(n^2)==
memory = ==O(1)==
==STABLE==
Optimize Repeats = ==no (optimized = yes)==
Cache friendly = ==better than others==
Speculative Execution Friendly = ==no==
Optimize ordered runs = ==no==
Parallel = ==some options (Odd-Even)==

#### Insertion Sort:
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

performance = ==O(n^2)==
memory = ==O(1)==
==STABLE==
Optimize Repeats = ==no==
Cache friendly = ==some==
Speculative Execution Friendly = ==fantastic yes==
Optimize ordered runs = ==no==
Parallel = ==maybe some method==

#### Selection Sort:
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

performance = ==O(n^2)==
memory = ==O(1)==
==STABLE==
Optimize Repeats = ==no==
Cache friendly = ==no==
Speculative Execution Friendly = ==often for most data==
Optimize ordered runs = ==no==
Parallel = ==some==
Oct 26: DEADBEEF

#### Quick Sort:
divide and conquer : uses a pivot 
```cpp
```

average performance = ==O(n log (n))==
worst performance = ==O(n^2)==
memory = ==O(log (n))==
==NOT STABLE==
Optimize Repeats = ==no==
Cache friendly = ==yes==
Speculative Execution Friendly = ==no==
Optimize ordered runs = ==no==
Parallel = ==some==

#### Merge Sort:
```cpp

```

average performance = ==O(n log (n))==
memory = ==O(n)==
==STABLE==
Optimize Repeats = ==no==
Cache friendly = ==yes==
Speculative Execution Friendly = ==some==
Optimize ordered runs = ==no==
Parallel = ==YES!==

#### Heap Sort:
![[Screenshot 2023-11-02 at 2.39.15 PM.png]]
```cpp

```
Max Heap: All parents are bigger than their children
nothing to do with memory heap

average performance = ==O(n log (n))==
memory = ==O(1)==
==NOT STABLE==
Optimize Repeats = ==no==
Cache friendly = ==no==
Speculative Execution Friendly = ==no==
Optimize ordered runs = ==no==
Parallel = ==some==

#### Tim Sort:
Hybrid sort: Insertion sort and Merge sort
Put's together ==runs of data==

average performance = ==O(n log (n))==
memory = ==O(n)==
==STABLE==
Optimize Repeats = ==yes==
Cache friendly = ==some==
Speculative Execution Friendly = ==some==
Optimize ordered runs = ==YES!==
Parallel = ==some==

## Threading Programing:
---
"fork-join"
![[Pasted image 20231102183224.png]]
parent thread will fork and create four child threads, then they will join the main parent thread.

```cpp
thread* arrayOfTrackers = new thread{numThreads};
```

Race Condition:
![[Pasted image 20231102183648.png]]

Mutex: allows an individual thread do something.

```cpp
countMutex.lock(); // locks bathroom stall
count = count + localCount; // uses the bathroomj
countMutex.unlock(); // unlocks bathroom stall
```

### Multi-Tread Counting Sixes:
```cpp
#include <iostream>
#include <random>
#include <chrono>
#include <cstdio> // For printf
#include <thread> // To create and track threads
#include <mutex>  // We'll see in a moment

using std::cin;
using std::cout;
using std::endl;
using std::thread;
using std::mutex;

unsigned int numThreads{ 4 };
unsigned int N{ 0 };
unsigned int count{ 0 };
uint8_t* arr{ nullptr };
mutex theOneAndOnlyMutex;

void allocateArray() {
  arr = new uint8_t[N];
}

void deleteArray() {
  delete[] arr;
}

void loadRandomNumbers() {
  std::random_device rd;
  std::mt19937 gen(rd());
  std::uniform_int_distribution<unsigned int> distrib(0, 9);
  for (unsigned int i = 0; i < N; ++i) {
    arr[i] = distrib(gen);
  }
}

void countSixes() {
  for (unsigned int i = 0; i < N; ++i) {
    if (arr[i] == 6) {
      ++count;
    }
  }
}

void parallelCountSixes(unsigned int threadID) {
  
  unsigned int startIndex{ N / numThreads * threadID };
  unsigned int endIndex{ N / numThreads * (threadID + 1) };
  unsigned int localCount{ 0 };
  printf("I'm thread %u, starting my work before I die\n", threadID);
  for (unsigned int i = startIndex; i < endIndex; ++i) {
    if (arr[i] == 6) {
      ++localCount;
    }
  }
  printf("I'm thread %u, before I die, I want my last words to be: count is %u\n", threadID, localCount);

  // Only one thread at a time can run this line of code
  theOneAndOnlyMutex.lock();
  count = count + localCount;
  theOneAndOnlyMutex.unlock();

}


int main() {

  N = 1'000'000'000;
  allocateArray();
  cout << "Loading random numbers" << endl;
  loadRandomNumbers();
  cout << "Counting sixes" << endl;
  auto t1 = std::chrono::high_resolution_clock::now();
  //countSixes();
  // Create thread tracking objects
  thread* arrayOfTrackers = new thread[numThreads];
  // Fork, create 4 child threads who are born starting at 
  // the function parallelCountingSixes() and die at the end of it
  for (unsigned int i = 0; i < numThreads; i++) {
    arrayOfTrackers[i] = thread(parallelCountSixes, i);
  }

  // Join, the parent thread waits until all child threads are done
  for (unsigned int i = 0; i < numThreads; i++) {
    arrayOfTrackers[i].join();
  }
  
  delete[] arrayOfTrackers;
  auto t2 = std::chrono::high_resolution_clock::now();
  std::chrono::duration<double, std::milli> fp_ms = t2 - t1;
  cout << "Count completed in " << fp_ms.count() << " milliseconds" << endl;
  cout << "Counted " << count << " sixes" << endl;
  deleteArray();
  cin.get();
  return 0;
}
```

nov 2: 999999

