Next Topic: [[11 - Pointers]]

#### Review of OOP:
---
Class designers; class implementers

Public interface: 
- ==What the class user needs to know how to use the class==

*stable interface* : 
- once part of the interface is public, that public access should not change

> *if cpp programmer changed `sqrt()` to `squareroot()` would cause problems*

```cpp
sqrt(2.6);
```

Data hiding: 
- Member data should only be manipulated through public interface

Encapsulation:
- ==bundle all data and functions within the class==

#### Unified Modeling Language (UML)
---
Broken up into Three parts:
- Top: Class name
- Middle: Attributes
- Bottom: Operations

`+` means public access
`-` means private access
`#` means protected access

Underlined means `Static` - meaning doesn't change.

constructor function doesn't return a type.

converting UML `person`:
```cpp
class Person {
private:
	string name;
	double height;
	int weight;
	static int instances;

	public Address get_address() {};

public:
	Person(string a_name, double a_height, int a_weight) {}

	bool pay_taxes() {}
	void catch_bus() {}

	static int getInstances() {
		return instances;
	}
}
```

converting UML `Time`:
```cpp
class Time {
private:
	int hours;
	int minutes;
	int seconds;

public:
	Time() {}
	Time(int h, int m, int s) : hours(h), minutes(m), seconds(s) {}
	Time(int s) {}
	
	Time add(Time ts) {}
	Time* add(Time* t2) {}

	void print() {}
	void read() {}
}
```