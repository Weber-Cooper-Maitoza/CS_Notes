*Variables are just `containers` for data.*
Next Topic: [[02 - Arithmetic]]

### Types of Variables in CPP
---
- `void` - (not really a data type; used later for returns)
- `short` - 16-bit whole number
- `int`* - 32-bit whole number
- `long` - 32 (or 64) bit whole number
- `float` - 32-bit floating point number
- `double`* - 64-bit floating point number
- `bool`* - true or false
- `char`* - single character
\*This is what you will use in most cases

### Constants:
---
`const` cannot change!
`const` variable name must be CAPATILIZED.

```cpp
const PEOPLE = 10;
```

### Rules for Variables in CPP:
---
Rules:
1. no length limit
2. are case sensitive (Apple != apple)
3. must begin with letter, or _
4. should be all letters, numbers, or underscores
5. cannot be a reserved word/should not be library names
6. may only be defined once in scope
7. must be declared before use
8. VARIABLE NAME SHOULD REPRESENT ITS CONTENT

#### Terminology:
- ==declare==: introduces a "symbol" (such as a variable) to the compiler
- ==define==: allocate memory to hold the variable (or function, etc.)
- ==initialize==: give the variable the initial value

### Scope:
---
- Variable scope: where variables can be seen/accessed
- Global: can be accessed within the file
- Local: delimited by those curly braces
- Function parameters: part of the function

### Variable stuff
---
`::` = **scope resolution operator**
Type promotions:
```cpp
std::cout << (7.0 / 5) << std::endl;
```

Type casting:
```cpp
double x = 67.56;
std::cout << (int)x << std::endl;
std::cout << ((double) 9 / 5) << std::endl;
```

String parsing:
```cpp
std::string coord = "96";
std::cout << std::stoi(coord) + 10 << std::endl;
```


Use:  `#include <iomanip>`
`setw()` = set the width of text output. 
	EX: `cout << setw(10) << "cooper" ` 
	OUTPUT: `          cooper` = setw(10)
`setprecision()` = sets the precision of decimals
`fixed` = uses fixed about of decimal places

### Import
---
```cpp
#include <iostream>
#include <string>
#include <iomanip>

int globalVar = 16;

int main () {
    std::cout << "Hello World!" /*this is a inline comment*/ << std::endl;

    double p = 355.0/ 67;
	std::cout << std::fixed << std::setprecision(3) << p << std::endl;
    std::string id = "Cooper";
    std::cout << std::setw(15) << id << std::endl;
}
```
