### Calculator 1:
```cpp
// Calculator 1: Area of a Circle

#include <iostream>
#include <iomanip>
#include<cmath>
using namespace std;

int main () {
    const double pi = 3.1415926535;
    double r;

    cout << "Radius: " ;
    cin >> r;
    cout << "Area: " << fixed << setprecision(10) << (pi * pow(r, 2)) /* 𝐴 = 𝜋𝑟2 */;
}

// Test Cases:
// Radius:              Area:
// 1.33                 5.5571632448
// 2.75                 23.7582944421
// 3.25                 33.1830724026
// 4.99                 78.2259712314
// 5.50                 95.0331777684
```
### Calculator 2:
```cpp
// Calculator 2: Fraction Addition
#include <iostream>
using namespace std;

int main () {
    int a;
    int b;
    int c;
    int d;
    char placeholder;

    cout << "First Fraction (a/b): ";
    cin >> a >> placeholder >> b;
    cout << "Second Fraction (c/d): ";
    cin >> c >> placeholder >> d;

    cout << "Sum: " << (a*d + b*c) << "/" << (b*d);
}

//  Test Cases:
//  Fraction 1      Fraction 2      Sum
//  1/3             2/5             11/15
//  1/4             2/3             11/12
//  1/2             1/2             4/4
//  7/10            9/15            195/150
//  76/80           95/100          15200/8000
```
### Calculator 3:
```cpp
// Calculator 3: Quadratic Formula
#include <iostream>
#include <cmath>
using namespace std;

int main () {
    int a;
    int b;
    int c;
    char deliminator;

    cout << "ax^2 + bx + c" << endl;
    cout << "Enter Coefficients (A,B,C): ";
    cin >> a >> deliminator >> b >> deliminator >> c;
    cout << "X-Intercept 1: " << ((-b + sqrt(pow(b, 2) - 4*a*c))/(2*a)) << endl;
    cout << "X-Intercept 2: " << ((-b - sqrt(pow(b, 2) - 4*a*c))/(2*a));

}

//  Input                       Output
//  A       B       C           x1          x2
//  3       6       -9          1           -3
//  1       -2      -24         6           -4
//  6       3       -6          0.780776    -1.28078
//  2       4       -8          1.23607     -3.23607
//  1       4       -20         2.89898     -6.89898
```