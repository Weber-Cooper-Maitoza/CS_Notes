Next Topic: [[03 - Decisions]]
### Import:
---
```cpp
#include <iostream>
#include <cmath>
#include <iomanip>
using namespace std;

int main () {

    // Arithmetic ops
    // +
    // -
    // *
    // /
    // %
    // ()
    // ++ increment operator (increases ONLY by 1)
    // -- decrement operator (decreases ONLY by 1)


//     x--; // postfix notation
//     --x; // prefix notation
//     cout << x ;

    // Compound assignment

//    x += 5; // same as (x = x + 5) "Compound assignment"
//     x -= 5;
//     x *= 5;

//    cout << x;

    // Math library

    // use #include <cmath>
//    cout << sqrt(2) << endl;
//    cout << sin(3.14159 / 2);

    // EXAMPLE: Distance formula

    /*
    double x1, y1, x2, y2, d;
    char c;

    cout << "Distance Formula Calculator, by Cooper" << endl;

    cout << "Enter point 1 (x, y): ";
    cin >> x1 >> c >> y1;

    cout << "Enter point 2 (x, y): ";
    cin >> x2 >> c >> y2;

    d = sqrt(pow((x2 - x1), 2) + pow((y2 - y1), 2));

    cout << "Distance: " << fixed << setprecision(10) << d << endl;
    */

    // Psudo-random numbers
    // why do we care about random numbers?
    // Games
    // Probabilities
    // Test cases / simulations
    // Art

    srand(time(0));
    cout << rand() << endl;

    // Random number between 1 and 10
    cout << rand() % 5 + 1 << endl;

    // Random number between 13 and 19
    // rand() % (high value - low value + 1) + low value

    cout << rand() % (19 - 13) + 13 << endl;

    // system pause for mac
    system( "read -n 1 -s -p \"Press any key to continue...\"; echo" );
    //system("read \"pause\"; echo");
}
```