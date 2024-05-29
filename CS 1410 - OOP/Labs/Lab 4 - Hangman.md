```cpp
#include <iostream>
using namespace std;

struct Employee {
  string name;
  int id;
};

int main() {
  // Arrays: collection of data

  // Some things about arrays in C++
  // NEED TO define how many items will be in the array
  // Once the array is defined, the size cannot change
  // All elements must be of the same data type

  // Python
  // Python does not have native support for arrays
  // Lists in python allow for mixed data types

  // Arrays in C++:
  int a1[4] = {1, 2, 3, 4}; // C++ Array
  int a2[] = {1, 2, 3, 4};  // Okay in C++

  int iq[5] = {150, 115, 85, 90, 95};
  double costs[3] = {7.2, 1.1, 3.9};
  string words[5] = {"Hello", "World", "This", "Is", "Array"};

  // Accessing array data
  cout << words[1] << endl;

  // cout << iq[-1] << endl;     // Doesn't WORK!!

  // Initialization Examples
  int test1[3] = {1, 2, 3};
  int test2[] = {1, 2, 3}; // prefered
  int test3[3] = {123, 234, 558};

  int test4[3];
  test4[0] = 1;
  test4[1] = 2;
  test4[2] = 3;

  // int* test6 = new int[3] { 1, 2, 3 }; TODO: WHYYYYYY

  int *test5 = new int[3];
  test5[0] = 65;
  test5[1] = 75;
  test5[2] = 85;
  delete [] test5;

  Employee employeesStuct[2] = {{"Rhodes", 937203}, {"Cooper", 273384}};
  cout << endl << employeesStuct[0].name << endl;

  // one-deminsional, two-dimensional, three-dimensional arrays
  // Two-dimensional Array:

  // C++ is a ROW MAJOR language (row is always specified first)

  int data[4][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}, {10, 11, 12}};

  cout << data[1][2] << endl;

  // memmory allocation:
  int array1[10];           // Allocated on the stack

  int* a9 = new int[10];    // Allocated on the heap #### MEMORY LEAK ####
  delete[] a9;              // #### DELETES MEMORY LEAK #####


  
  int size;
  cout << "Number of data points needed: ";
  cin >> size;

  // double dataset[size];
  double* dataset = new double[size];

  for (int i = 0; i < 1; i++)
    dataset[i] = i * 2;

  delete[] dataset; 

  // Partially filled arrays...

  // And so on...


}
```