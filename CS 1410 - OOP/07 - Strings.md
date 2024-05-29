Next Topic: [[08 - Arrays]]





### Import:
---
```cpp
#include <cstdio>
#include <string>
#include <iostream>
using namespace std;

int main()
{
    // Aggregate data
    // enumeration (interger constants)
    // structures (structs)
    // strings

    // string - any sequence of characters
    // constructors(s) - how you create an instance of an object
    // functions

    string s1; // default
    string s2("Hello"); // conversion 
    string s3(s2); // copy
    string s4 = "This is a really long string that i have made."; // assignment

    // cout << s4.capacity() << endl;

    // Operators for strings
    // =            assignment
    // <, >         relational
    // ==           equality
    // !=           not equals
    // +            concatenation 

    cout << s2 + " World\n";


    // string input
    string name;
    cout << "Type your full name: ";
    getline(cin, name);
    cout << "Welcome, " + name + " to class\n";

    // find a substring
    size_t index = name.find("Maitoza"); 

    if (index != string::npos)
        cout << "Maitoza found at " << index << endl;
    else
        cout << "Not Found" << endl;

    // String iteration
    // .at()
    // []
    // range
    
    for (size_t i = 0; i < name.length(); i++) {
        if (name[i] == ' ')
            cout << "Space is found at " << i << endl;
    }
    
    // toString()
    int number = 75;
    cout << "This is a number: " << to_string(number) << endl;

    // number conversions
    string number1 = "139";
    // double result = stoi(number1) / 2; // STOI = string to int
    // double result = stod(number1) / 2; // STOD = string to double 
    cout << stoi(number1);

    // arrays
}
```