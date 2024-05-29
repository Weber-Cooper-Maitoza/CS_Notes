Next Topic: [[09 - Start of OOP (Single Program Class)]]

### Array Info:

'*Arrays: collection of data*'

Some things about arrays in C++
- **NEED TO** define how many items will be in the array
- Once the array is defined, the size cannot change
- All elements must be of the same data type

Python:
- Python does not have native support for arrays
- Lists in python allow for mixed data types

### Array Examples:
---
Array Format:
```cpp
int a1[4] = {1, 2, 3, 4}; // C++ Array
int a2[] = {1, 2, 3, 4};  // Okay in C++
```

Array data types:
```cpp
int iq[5] = {150, 115, 85, 90, 95};
double costs[3] = {7.2, 1.1, 3.9};
string words[5] = {"Hello", "World", "This", "Is", "Array"};
```

Struct Types For Arrays:
```cpp
struct Employee {
  string name;
  int id;
  
int main() {
  Employee employeesStuct[2] = {{"Rhodes", 937203}, {"Cooper", 273384}};
  cout << endl << employeesStuct[0].name << endl;
}
```

Initialization Examples:
```cpp
int test1[3] = {1, 2, 3};
int test2[] = {1, 2, 3}; // prefered
int test3[3] = {123, 234, 558};
```


### Array Sizes:

```cpp
const int SIZE = 10; // Delcare const size for array 
int data1[SIZE];

for (int i; i < SIZE; i++)
	data1[i] = i;
```

### Partially Filled Arrays: ==What do you do if you don't know the size==

```cpp
const int size = 1000; // Build it to be massive
int index = 0;

int data1[size];
data1[index++] = 6;
data1[index++] = 7;
data1[index++] = 8;
data1[index++] = 9;

for (int i = 0; i < index; i++)
	cout << data1[i] << endl;
```
- Can take a lot of *memory* and can *break* if you go over 

### Declaring and Initializing partially filled arrays:

```cpp
int data[10] = { 32, 33, 34, 35, 36 };

for (int i = 0; i < 10; i++)
	cout << data1[i] << endl; 
	
// output:
// 32, 33, 34, 35, 36, 0, 0, 0, 0, 0
```

### Zeroing Array Elements:

```cpp
int test[10] = {};

for (int i = 0; i < 10; i++)
	cout << data1[i] << endl; 

// output:
// 0, 0, 0, 0, 0, 0, 0, 0, 0

// if 'int test[10];'
// output would be garbage
```

### Computing Size Of Array:

```cpp
string fruit[] = { "apples", "bananas", "oranges", "Grapes", "limes" };
int size = sizeof(fruit) / sizeof(string);
// sizeof(fruit) = 200 byte
// sizeof(string) = 40 byte
// 200 / 40 = 5 

for (int i = 0; i < size; i++)
	cout << data1[i] << endl; 
```
==WILL NOT WORK WHEN ARRAYS ARE PASSED TO A FUNCTION==

### Two-dimensional Array

==C++ is a ROW MAJOR language (row is always specified first)==

```cpp
int data[4][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}, {10, 11, 12}};

cout << data[1][2] << endl;
```

iterating rough a 2D array:
```cpp
char alpha[3][4] = { 'a', 'b', 'c', 'd', 
					'e', 'f', 'g' 'h', 
					'i', 'j', 'k', 'l' }; // just format it like this 
										// or something better

for (int row = 0; row < 3; row ++){
	for (int col = 0; col < 4; col++)
		cout << "[" << alpha[row][col] << "]";
	cout << endl;
}
```

### Copying Arrays:

NOT A COPY:
```cpp
//char alpha[3] = { 'e', 'f', 'g' };
char alpha1[4] = { 'a', 'b', 'c', 'd' };

char* alpha2 = alpha1; // assigns alpha2's memory address is the same as alpha1

alpha2[0] = 'f';
// changes both 'alpha1' and 'alpha2' index 0 to 'f'
```

COPY:
```cpp
char alpha1[4] = { 'a', 'b', 'c', 'd' };
char alpha2[4];

for (int i = 0; i < 4; i++){
	alpha2[i] = alpha1[i];
}

alpha2[0] = 'f';

for (int i = 0; i < 4; i++){
	cout << alpha1[i] << endl;
}
for (int i = 0; i < 4; i++){
	cout << alpha2[i] << endl;
}

// output:
// abcd
// fbcd
```

### Memory Allocation:

```cpp
int array1[10];           // Allocated on the stack

int* a9 = new int[10];    // Allocated on the heap #### MEMORY LEAK ####
delete[] a9;    // #### DELETES MEMORY LEAK #####
  
int* test5 = new int[3];
test5[0] = 65;
test5[1] = 75;
test5[2] = 85;
delete [] test5; // need to close a pointer 
```

### Functions and Arrays:

- Arrays are always passed by pointer
Review on PassByValues:
```cpp
void updateVar(char letter) { // "char &letter" change by refferance 
	letter = 'f';
}

int main() {
	char letter = 'a';
	updateVar(letter); // passby value
	cout << letter << endl; // output: a
	
	char alpha[4] = { 'a', 'b', 'c', 'd' };
}
```

ARRAYS AND FUNCTIONS:
```cpp
void updateFirst(char array[]) {

}

int main() {
	char alpha[4] = { 'a', 'b', 'c', 'd' };

	updateFirst(alpha); // ALWYS PASSED BY POINTER
	
	for (int i=0; i<4; i++)
		cout << alpha[i];
	// Output: fbcd
}
```

### Array Decay:

==Passing arrays into function parameters==
function:
```cpp
void sizeOfArray(char alpha[]) {
	int size = sizeof(alpha) / sizeof(char);
	cout << "Size of array: " << size << endl;
}

int main() {
	char alpha[4] = { 'a', 'b', 'c', 'd' };

	int size = sizeof(alpha) / sizeof(char);
	cout << "Size of array: " << size << endl; 
	// Output: 4

	sizeOfArray(alpha);
	// Output: 8 
	// DOESNT WORK IF YOU PASS AN ARRAY INTO A FUNCTION
}
```

### Returning arrays from functions:

build print array function:
```cpp
void print(int a[], int size) {
	for (int i = 0; i < size; i++)
		cout << "[" << a[i] << "]";
	cout << endl;
}

```


```cpp
int* getRandomFive() { // Type INT*
	int random[5]; // ############## LOCAL SCOPE ###########################
	// static int random[5]; SEE FOOT NOTE
	for (int i = 0; i < 5; i++) 
		random[i] = rand() % 10;
	cout << "In Fucntion: ";
	print(random, 5); // output: 1, 7, 4, 0, 9 
	return random;
}

int main()
{
	int* random = getRandomFive();
	cout << "In Main: ";
	print(random, 5); // output: GARBAGE
}
```

Solution 1:  Static (NOT A GOOD IDEA)

```cpp
int* getRandomFive() { 
	static int random[5]; SEE FOOT NOTE
	for (int i = 0; i < 5; i++) 
		random[i] = rand() % 10;
	cout << "In Fucntion: ";
	print(random, 5); // output: 1, 7, 4, 0, 9 
	return random;
}

int main()
{
	int* random = getRandomFive();
	cout << "In Main: ";
	print(random, 5); // output: GARBAGE
}
```
- `static` only works for functions to share a "global" variable.

Solution 2: pass as an argument

```cpp
int* getRandomFive(int random[]) { // Type INT*
	for (int i = 0; i < 5; i++) 
		random[i] = rand() % 10;
	cout << "In Fucntion: ";
	print(random, 5); // output: 1, 7, 4, 0, 9 
	return random;
}

int main()
{
	int a[5];
	int* random = getRandomFive(a);

	int b[5];
	int* random = getRandomFive(b);
	
	cout << "In Main: ";
	print(random, 5); // output: GARBAGE
}
```

Solution 3: allocate on the heap

```cpp
int* getRandomFive() { 
	int* random = new int[5]; // throw into heap memory
	for (int i = 0; i < 5; i++) 
		random[i] = rand() % 10;
	cout << "In Fucntion: ";
	print(random, 5); // output: 1, 7, 4, 0, 9 
	return random;
}

int main()
{
	int* random = getRandomFive();
	
	cout << "In Main: ";
	print(random, 5); // output: GARBAGE

	delete[] random; // dealocate pointer
}
```
- MEMORY LEAKK! if not **deallocated**

### Arrays and Security: some notes on arrays

1. Ensure input validation (when user input is used to access arrays).
	1. check with an if statement.
2. Test to ensure array indices in bounds "if (index >= 0 && index < SIZE)".
3. Ensure indices based on calculations are correct.
4. Ensure array size is included when passes as args to functions.