Next Topic: [[05 - Functions]]

## For Loops:
---

## While Loops:
---

## Do While Loops:
---


### Import: 
---
```cpp
#include <iomanip>
#include <iostream>
using namespace std;

int main() {
  // Loops

  // while - it is an indeterminate loop (iterations unknown) and loop may not
  // execute

  int number = 1;
  while (number <= 3) {
    cout << "Elmo says: " << number++ << "!" << endl;
    // number++;
  }

  // do while - same as standard while loop (indeterminate) but loop ALWAYS
  // execute once
  cout << endl << endl;

  number = 1;
  do {
    cout << "Elmo says: " << number++ << "!" << endl;
  } while (number <= 3);

  // for - you or the program know how many iterations known (Determinate)
  cout << endl << endl;

  // init (variable)
  // condition
  // update

  for (int number = 0; number < 10; number++) {
    cout << "Elmo says " << (number + 1) << "!" << endl;
  }

  int value;
  cout << "Enter a number: ";
  cin >> value;

  for (int i = 1; i <= value; i++)
    if (value % i == 0)
      cout << i << ", " << value / i << endl;

  // NOT COMMON
  cout << endl << endl;
  // Example: Fibonacci sequence
  // 0, 1, 1, 2, 3, 5, 8, 13, etc.

  /*
      for (long fn = 0, f1 = 1, swap = 0; f1 < 100000; swap = f1, f1 = fn + f1,
     fn = swap) cout << f1 << endl;
  */

  // Nested loops:
  // use "#include <iomanip>"
  for (int i = 1; i <= 12; i++) {
    for (int j = 1; j <= 12; j++)
      cout << setw(5) << i * j;
    cout << endl;
  }

  // for range - iterate through an existing collection
  string s = "Hello world!";
  for (char c : s)
    cout << c << ", " << endl;

  // Fence Post Problem

  string student[] = {"Thomas", "Austin", "Olga", "Phil", "Hunter"};
  for (string studentName : student)
    cout << "Hello " << studentName << endl;

  for (int i = 0; i < student->size() - 2; i++) {
    cout << student[i] << ", ";
  }
  cout << student[student->size() - 2];

  cout << endl << endl;

  // break

  for (int i = 0; i < 10; i++) {
    if (i == 6)
      continue;
    cout << i << ", ";
  }

  // complete example: search the alphabet
  char letter;
  cout << "Which letter? ";
  cin >> letter;

  for (int i = 1; i <= 26; i++) {
    cout << "Searching position " << i << "..." << endl;
    if (char(i + 64) == letter || char(i + 96) == letter) {
      cout << letter << " is in postion " << i << "." << endl;
      break;
    } else if (i < 26)
      continue;
    cout << letter << " not found." << endl;
  }

  // Null Statements (and why they are tricky:

  // for (int i = 0; i < 10; i++);
  // cout << i << endl;

  // Tricky scope

  cout << "You are standing at a cabin." << endl;

  char response;

  do {
    cout << "To the left is a lake, to the right is a mountian." << endl;
    cout << "\nWhich way? (L/M): ";
    cin >> response;

    if (toupper(response) == 'L') {
      cout << "You travel to the lake..." << endl;
      cout << "After a while, you find yourself back at the cabin." << endl;
    }

    else {
      cout << "You travel to the mountian..." << endl;
    }

  } while (toupper(response) == 'L');
}

```