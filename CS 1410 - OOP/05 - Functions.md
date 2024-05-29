Next Topic: [[06 - Enum and Struct]]

**Functions**: ==reusable piece of code==

"Machine" can have a variety of inputs (or no inputs at all)
Does some work behind the scenes
Then kicks back some kind of output

- **Bottom-up programming**: getting the "pieces" to work, before the larger project 
- **Top-down programming**: Focusing on the larger project, and using "fillers" as needed to get it to work


int                                  - return type       (specify ahead of time what it will return)                                                          (can be any type: double, char, string, void)
randInt                              - identifier        (Programmer-defined name of function)
int low, int high                    - parameters        (data necessary to apply this function)
{}                                   - function body
return random                        - return statement  (one piece of data that gets)
returned to the caller) (13, 19)     - arguments         (actual data sent to the function)

#### Decimal to Hex conversion Function:
```cpp
string decToHexDigit(int n); // declaration

string decToHexDigit(int n) {
    if (n >= 0 && n < 16) {
        switch (n) {
            case 15:
                return "F";
            case 14:
                return "E";
            case 13:
                return "D";
            case 12:
                return "C";
            case 11:
                return "B";
            case 10:
                return "A";
            default:
                return to_string(n);
        }
    }
    else
        return "Only Single Numbers";
}
```

## Pass-by-xx:
---
#### Pass-by-pointer (C++)
---
Variable where the value is an address

#### Pass-by-reference (reference to the memory address)
---
Advantages:
- Efficient for large amounts of data
- More efficient because no data is contained

Disadvantages:
- Only works with variables (i.e. not with expressions)
- Function call and definition must exist in same address space
- Might mess up your original data (but this can be fixed)

```cpp
double interimCompute(const double &bigData){
    double computation = bigData * 1.50;
    return computation;
}
```

#### Pass-By-Value (copy of the data)
---
Advantages:
- No concert about "accidentally" modifying the original data
- May pass expressions (rather than just values)

Disadvantages:
- Cannot update value directly
- It can be costly (i.e. time/memory) to make copies of larger data

```cpp
// Pass-By-Value, returns value
int addFiveToReturn(int a) {
    a += 5;
    cout << "in function: " << a << endl;
    return a;
}
```

### Import:
---
```cpp
#include <cstdlib>
#include <iostream>
using namespace std;

int randInt(int low, int high);             // Prototype (Function Declaration)
void showRandomDicePair();
void showRandomDice(int n);
void showExactDicePair(int d1, int d2);
int getNRandomDice(int n);

int main() {
  // Functions: resuable peice of code

  // "Machine" can have a variety of inputs (or no inputs at all)
  // Does some work behind the scenes
  // Then kicks back some kind of output

  srand(time(0));
  showRandomDicePair();
  showRandomDice(7);
  showExactDicePair(6, 6);

  // Bottom-up programming: getting the "pieces" to work, before the larger
  // project Top-down programming: Focusing on the larger project, and using
  // "fillers" as needed to get it to work
  //
}

int getNRandomDice(int n) {
  int sum = 0;
  for (int i = 0; i < n; i++) {
    int d = randInt(1, 6);
    cout << "[" << d << "]";
    sum += d;
  }
  cout << endl;
  return sum;
}

void showRandomDicePair() {
  int d1 = randInt(1, 6);
  int d2 = randInt(1, 6);
  cout << "[" << d1 << "][" << d2 << "]" << endl;
}

void showRandomDice(int n) {
  for (int i = 0; i < n; i++) {
    int d = randInt(1, 6);
    cout << "[" << d << "]";
  }
  cout << endl;
}

// two parameters, no return
void showExactDicePair(int d1, int d2) {
  cout << "[" << d1 << "][" << d2 << "]" << endl;
}

int randInt(int low, int high) { // Function Definition
  int random = rand() % (high - low + 1) + low;
  return random;
}

// int                                  - return type       (specify ahead of time what it will return)
//                                                          (can be any type: double, char, string, void)
// randInt                              - identifier        (Programmer-defined name of function)
// int low, int high                    - parameters        (data necessary to apply this function)
// {}                                   - function body
// return random                        - return statement  (one piece of data that gets)
// returned to the caller) (13, 19)     - arguments         (actual data sent to the function)

```

```cpp
#include <iostream>
#include <string>
using namespace std;

double distance(double x1, double y1, double x2, double y2);

string decToHexDigit(int n);

int main ()
{
//    double x = distance(2, 5, 3, 9);
//    cout << x;
    int number;
    cout << "what number: " << endl;
    cin >> number;
    cout << decToHexDigit(number) << endl;

}

// if you specify a return type (other than void): MUST return value
// you can: return a variable
// The caller can ignore the return value

double distance(double x1, double y1, double x2, double y2) {
    return sqrt((pow(x2 - x1, 2)) + (pow(y2 - y1, 2)));
}

string decToHexDigit(int n) {
    if (n >= 0 && n < 16) {
        switch (n) {
            case 15:
                return "F";
            case 14:
                return "E";
            case 13:
                return "D";
            case 12:
                return "C";
            case 11:
                return "B";
            case 10:
                return "A";
            default:
                return to_string(n);
        }
    }
    else
        return "Only Single Numbers";
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

void addFiveTo(int a);
int addFiveToReturn(int a);

int main ()
{
    int n = 5;
    // addFiveTo(n);
    n = addFiveToReturn(n); // updates itself
    cout << "n in main: " << n << endl;
}
// Pass-by-value #####################################################################
void addFiveTo(int a) {
    a += 5;
    cout << "in function: " << a << endl;
 }
// Pass-By-Value, returns value
int addFiveToReturn(int a) {
    a += 5;
    cout << "in function: " << a << endl;
    return a;
}
```

```cpp
#include <iostream>
#include <string>
using namespace std;

void addFiveTo(int a);
void addFiveToRef(int &a);

int main() {
  int a = 32; // Local variable ##############################################
  addFiveTo(32 + 45);
  cout << "call in main: " << a << endl;
}
// Pass-by-pointer (C++)
// Variable where the value is an address

// Pass-by-reference (reference to the memory address)
// advantages:
//      - Efficient for large amounts of data
//      - More efficient because no data is contained
// Disadvantages:
//      - Only works with variables (i.e. not with expressions)
//      - Function call and definition must exist in same address space
//      - Might mess up your original data (but this can be fixed)

// Pass-By-Value (copy of the data)
// Advantages:
//    - No concert about "accidently" modifying the original data
//    - May pass expressions (rather than just values)
//
// Disadvantages:
//    - Cannot update value directly
//    - It can be costly (i.e. time/memory) to make copies of larger data

// Pass-by-value
void addFiveTo(int a) {
  a += 5;
  addFiveToRef(a);
  cout << "in function: " << a << endl;
}

void addFiveToRef(int &a) {
  a += 5;
  cout << "a in function: " << a << endl;
}

```

```cpp
#include <iostream>
#include <string>
using namespace std;

void makeNewPart();

int main()
{
    makeNewPart();
    makeNewPart();
    makeNewPart();
    makeNewPart();
    makeNewPart();

}

void makeNewPart() {
    static int part = 0;       // Static variable #############################################
    cout << "Generating part #" << ++part << endl;
}

// Overloaded functions
// Default arguments
// Const
// Inline functions?
// Recursion
// Interpreting library functions

```

Day Two: functions contenued
```cpp
#include <iostream>
using namespace std;

int findMax(int, int);
double findMax(double, double);

int main ()
{
    // Overloaded functions: two or more functions w/ the same name
    // a - different number of parameters
    // b - different types of parameters
    // CANNOT DO: same number/type of params (i.e. no ambiguity)

    int n = findMax(7, 2);
    double r = findMax(7.9, 2.3);
    cout << n << endl <<  r ;
}

int findMax(int a, int b) {
    return (a > b) ? a : b; // ternary operator
//    if (a > b)
//        return a;
//    else
//        return b;
}

double findMax(double a, double b) {
    return (a > b) ? a : b;
}
```
default argument
```cpp
#include <iostream>
using namespace std;

//void decorativeBorder(int = 75, char = '-');
void decorativeBorder(int = 75, char = '-');

int main ()
{
    // default arguments
    // required + default, then default always to the right
    // provide some but not others, can only skip to the right
    // defaults specified in prototype (if done separately)
    // overloaded functions w/ defaults cannot be ambiguous

    decorativeBorder(50, '*');
    decorativeBorder(20, '#');
    decorativeBorder();

}

void decorativeBorder(int length, char character) {
    for (int i=0; i < length; i++)
        cout << character;
    cout << endl;
}
```
const
```cpp
#include <iostream>
using namespace std;

double interimCompute(const double& bigData);

int main ()
{
    // const
    double data = 3;
    cout << interimCompute(data);

}

double interimCompute(const double& bigData){
    double computation = bigData * 1.50;
    return computation;
}
```
inline functions
```cpp
#include <iostream>
using namespace std;

// inline function: quick-and-dirty that replaces funciton calls in project (speed)
inline int findMin(int x, int y) {return (x < y) ? x : y; };

int main ()
{
    int min = findMin(5, 6);
    cout << min;
}
```
recursion
```cpp
#include <iostream>
#include <string>
using namespace std;

void notRecursion();
void song(int n = 99);
long factorial(int);
double sine(int x, int n = 0);
string greaterIgnoreCase(string, string, int = 0);


int main ()
{
    // apple > banana


    // Recursion: to understand recursion, one must first understand recursion

    // Recursion is when a function calls its self

    // Must have:
        // function calls itself path
        // argument that changes from call to call
        // base case: the path where no recursion occurs

    // song(5);

    //cout << factorial(10);

//    cout << sin(1) << endl;
//    cout << sine(1);

    string greaterWord = greaterIgnoreCase("applean", "apple");
    cout << greaterWord << endl;
}

string greaterIgnoreCase(string a, string b, int index){
    // TODO: Remove non-alphabetical characters
    if (index < a.size() && index < b.size()) {
        // word 'a' letter is greater
        if (tolower(a.at(index)) > tolower(b.at(index)))
            return a;
            // word 'a' letter is lesser (b is greater)
        else if (tolower(a.at(index)) < tolower(b.at(index)))
            return b;
            // letters are the same (repeat algorithm with next letter)
        else
            return greaterIgnoreCase(a, b, index + 1);
    }
    else if (a.size() != b.size())
        return a.size() > b.size() ? a : b;
    else
        return a; // not really the same but whatever
}


double sine(int x, int n){
    if (n < 10)
        return sine(x, n + 1) + pow((-1), n) * ((pow(x, 2 * n +1) / factorial(2 * n + 1)));
    else
        return 0;
}

long factorial(int n){
    if (n >= 1)
        return n * factorial(n-1);
    else
        return 1;
}

void song(int n) {
    cout << n << " bottle of coke on the wall..." << endl;
    if (n > 1)
        song(n - 1);
    else
        cout << "...no more bottles of coke on the wall!";
}

void notRecursion() {
    // notRecursion();
}
```