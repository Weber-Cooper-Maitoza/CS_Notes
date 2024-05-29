Card Class:
```cpp
// Cards
// int value, string suit
// getValue()
// addCard(Card card)

// Card cardA(9)
// Card cardB(3)

// How Would You Add Both Numbers

// int sumCard = cardA.getValue() 
// Card cardC = cardA.add(cardB);

// Card cardC = cardA + cardB; #############

```

#### Rules for Overloaded Operators:
---
Rules:
1. Should NOT change the meaning of a prebuilt operator 
	1. EX. a + b (result = a - b)
	2. IN PYTHON. string * 5 = stringstringstringstringstring
2. Cannot change the precedence of the operator or associativity
	1. Natural Precedence: PEMDAS
3. Cannot change number of operands
	1. EX. 5 + 4 (only 2 operands)
4. Cannot create a new operator (can only overload existing)
5. Cannot overload an operator without using some class (modified from text)

"*Should Be Intuitive*" 

## Commonly Overloaded Operators:
---
- +
- - 
- * 
- / 
- +=
- -=
- \*= 
- /= 
- <<
- >>  
- type conversions
- ()
- []

Cannot Overload (not exhaustive)
- ::
- .
- new
- etc.

## Example:
---
```cpp
#include <iostream>
using namespace std;

class Time {
private:
	int hours = 0;
	int minutes = 0;
	int seconds = 0;

public:
	// Default constructor
	Time() {}

	// Parameterized constructor
	Time(int h, int m, int s) : hours(h), minutes(m), seconds(s) {}

	// Conversions constuctor
	Time(int seconds) {
		hours = seconds / 3600;
		seconds %= 36000;
		minutes = seconds / 60;
		this->seconds = seconds % 60;
	}

	// Overlaoded operator to add two Time Objects
	Time operator+(Time time) {
		// can add `this->` or not
		int seconds1 = this->hours * 3600 + minutes * 60 + seconds;
		int seconds2 = time.hours * 3600 + time.minutes * 60 + time.seconds;
		return Time(seconds1 + seconds2);
	}

	// only for integer on the left and 
	/*friend Time operator+(int seconds, Time time) {
		int seconds1 = time.hours * 3600 + time.minutes * 60 + time.seconds;
		return Time(0, 0, seconds1 + seconds);
	}*/

	// Temporary print function
	void print() {
		cout << hours << ":";
		if (minutes < 10)
			cout << "0";
		cout << minutes << ":";
		if (seconds < 10)
			cout << "0";
		cout << seconds << endl;
	}
};

int main ()
{
	Time time1(5, 4, 39);
	time1.print();	
  
	Time time2(2, 57, 55);

	Time time3 = time1 + time2;
	time3.print();
}
```

#### Integer Constructor conversion:
---
```cpp
Time(int seconds) {
	hours = seconds / 3600;
	seconds %= 36000;
	minutes = seconds / 60;
	this->seconds = seconds % 60;
}
```

This is used to with:
```cpp
Time time3 = time2 + 55;
```

converts `55` to a Time object.

#### Friend type:
---
Friend version of overloaded `+` operator:
```cpp
friend Time operator+(Time time1, Time time2) {
	int seconds1 = time1.hours * 3600 + time1.minutes * 60 + time1.seconds;
	int seconds2 = time2.hours * 3600 + time2.minutes * 60 + time2.seconds;
	return Time(seconds1 + seconds2);
}
```

"`friend`" can ==access private variables== in their associated class

#### Insertion:
---
Declaration of overloaded insertion/extraction
```cpp
friend ostream& operator<<(ostream& out, const Time& time);
```
- `ostream& out` is the ==left== operand next to "<<"
- `ostream&` is a value
- const is used so you don't change time

```cpp
ostream& operator<<(ostream& out, const Time& time) {
  out << time.hours << ":";
  if (time.minutes < 10)
    out << "0";
  out << time.minutes << ":";
  if (time.seconds < 10)
    out << "0";
  out << time.seconds;
  return out;
}
```

usage:
```cpp
Time time1(5, 4, 39);
cout << time1 << endl;
```

#### Extractor:
---
declaration:
```cpp
istream& operator>>(istream& in, Time& time);
```
- DON'T USE CONST
- `instrea&` is used to declare
- USE `>>` operator

```cpp
istream& operator>>(istream& in, Time& time) {
  char c;
  cout << "Please enter a time in the format (hh:mm:ss): ";
  in >> time.hours >> c >> time.minutes >> c >> time.seconds;
  return in;
}
```

usage:
```cpp
Time time4;
cin >> time4;
cout << time4 << endl;
```

#### Type Conversion:
---
converts one time into another. 
"*int to double*"
##### Integer conversion:
```cpp
// Converts to seconds
operator int() {
	return hours * 3600 + minutes * 60 + seconds;
}
```

usage:
```cpp
Time time1(5, 4, 39);
cout << time1 << endl;
cout << int(time1) << endl;
```

###### Double conversion:
```cpp
// Convert to hours
operator double() {
	return double(int(*this)) / 3600;
}
```

==`*this`== is a way to dereference the `instansiation` 
Example:
```cpp
Time* time1 = new Time(1, 50, 0);
cout << *time1 << endl;
```

Usage:
```cpp
Time time1(5, 4, 39);
cout << time1 << endl;
cout << double(time1) << endl;
```

##### Compound Assignment:
Examples: +=, -=, \*=, /= 

Need THIS:
```cpp
// Overlaoded operator to add two Time Objects
Time operator+(Time time) {
	// can add `this->` or not
	int seconds1 = hours * 3600 + minutes * 60 + seconds;
	int seconds2 = time.hours * 3600 + time.minutes * 60 + time.seconds;
	return Time(seconds1 + seconds2);
}
```

```cpp
// Compound assignment: += 
Time& operator+=(Time time) {
	*this = *this + time;
	return *this;
}
```

usage:
```cpp
Time time1(5, 4, 39);
Time time2(2, 57, 55);
time1 += time2;
```

##### Increment/Decrement:
Examples: ++, --

Prefix notation: `++time1`
```cpp
// Prefix notation
Time& operator++() {
	this->hours += 1;
	return *this;
}
```

usage:
```cpp
Time time1(1, 30, 0);
cout << time1 << endl;
cout << ++time1 << endl;
cout << time1 << endl;
```

Postfix Notation: `time++`
```cpp
// Postfix notation
Time operator++(int) {
	Time copy(int(*this));
	this->hours += 1;
	return copy;
}
```

usage:
```cpp
Time time1(1, 30, 0);
cout << time1 << endl;
cout << time1++ << endl;
cout << time1 << endl;
```

#### testing relational operators:
---
```cpp

// compairs integers
if (time1 > time2) {
	blah
}

// int(time1) > int(time2)
bool operators>(Time time) {
	if (int(*time) > int(*time))
}
```