Next Topic: [[13 - Overloaded Operators]]

## Multi-class Programs:
---
*"Programmers can only solve elementary problems with a single class program; solving more complex problems require multiple classes"*

How do each of the classes (which all serve some purpose) relate to one another in a complex problem?

Six relationships for "binding" collections of objects:
1. Inheritance - class (generic case) to class (specific case)
2. Composition - class comprises parts of another class
3. Aggregation - class comprises parts of another class (parts are usually interchangeable)
4. Association - classes are of "equal" importance that interact with each other
5. Dependency - class that uses other classes
6. Realization (Won't be covering this) - class that implements some interface

- Lifetime (are the objects created/destroyed together, etc)
- Sharing (parts of the whole can be shared, etc.)
- Binding strength (tight, loose)

#### Overridden functions:
---
==Overrides inherited `work()` function in `forager` class.==

```cpp
class Worker : public Ant {
private:
  int capacity;
public:
  Worker(string designation, int capacity) : Ant(designation), capacity(capacity) {}

  void work(int value) {
    cout << designation << " works for " << value << " units." << endl;
  }
};

class Forager : public Worker {
public:
  Forager(string designation = "Forager", int capacity = 2) : Worker(designation, capacity) {}

  // Overridden function
  void work(int value) {
    cout << designation << " searches." << endl;
    Worker::work(value); // get workers work function
  }
};

class Nurse : public Worker {
//blah
}
```

#### Overloaded functions:
---
```cpp
// Overloaded functions
void work() {
cout << designation << " works." << endl;
}

void work(int value) {
cout << designation << " works for " << value << " units." << endl;
}
```

## Inheritance:
---
uses a solid Arrow shape in UML diagram
![[Pasted image 20230801160356.png]]

```cpp
class Human {
private:
	int age;
public:
	Human(int age){
		this->age = age;
	}
}
```

```cpp
class Person : public Human {
private:
	string name;
public:
	Person(int age, string name) : Human(age){
		this->name = name;
	}	
}
```

## Composition:
---
uses a solid Diamond shape in UML diagram

![[Pasted image 20230801160500.png]]


"*one class exists as an integral part of another class*"
"A whole part relationship that you can not swap parts"
Objects live and die together

Semantic:
- Has-a
- Is-a-part-of

Colony has a queen (colony has to have a queen or its ceases to be a colony)

==Unidirectional== meaning can only go one way:
binding strength: ==strong/tight==
lifetime: ==coincident (created and destroyed together)==
Sharing: ==exclusive (The whole does not share the parts)==

Consider the following example of a simple composition using a `Car` class. We'll create a `Car` class that is composed of an `Engine` and a `Wheel` class.

```cpp
// Engine class
class Engine {
public:
    void start() {
        std::cout << "Engine started.\n";
    }
};

// Wheel class
class Wheel {
public:
    void rotate() {
        std::cout << "Wheel rotating.\n";
    }
};

// Car class composed of Engine and Wheel
class Car {
private:
    Engine engine;
    Wheel wheels[4]; // Four wheels

public:
    void startCar() {
        engine.start();
        for (int i = 0; i < 4; ++i) {
            wheels[i].rotate();
        }
        std::cout << "Car started.\n";
    }
};
```

## Aggregation:
---
uses a hollow Diamond shape in UML diagram

![[Pasted image 20230801160518.png]]

A whole/part relationship (==The parts don't have to be exclusive to the whole==)
"*A whole part relationship but you can swap out parts*"

Semantic Terms:
- Has-a
- Is-a-part-of

Colony has a food cache (but colony can exist without one)
Binding strength: ==weak/loose==
Lifetime: ==separate==
Sharing: ==not exclusive (can be shared)==

LIKE COMPOSITION BUT WITH POINTERS!!!

```cpp
// Address class
class Address {
private:
    std::string street;
    std::string city;
    std::string zip;

};

// Student class with aggregated Address object
class Student {
private:
    std::string name;
    int age;
    Address *address; // Aggregated Address object

};
```

```cpp
class Colony {
private:
  FoodCache* foodCache = nullptr;

public:
  void setFoodCache(FoodCache* foodCache) {
    this->foodCache = foodCache;
  }

};
```

```cpp
// colony has a food cache
// Food chache can exist without the colony (and vice versa)
class FoodCache {
private: 
  int amount = 0;
public:
  FoodCache(int amount) {
    this->amount = amount;
  }

  void addFood(int amount) {
    this->amount = amount;
  }
};
```

## Multiplicity:
---
uses the `0..*` Notation in UML diagram (from 0 to infinity)

## Dependency:
---
uses a dotted arrow `---->` in a UML diagram

![[Pasted image 20230801160540.png]]

"*When one of the functions "depends" on another class*"

an ant is not a food cache and a food cache is not an ant.
Semantic Terms:
- depends on
- delegates to
- uses a

Binding Strength: ==Weak/loose==
Lifetime: ==separate==
Sharing: ==Not exclusive (can be shared)==

```cpp
// Console class for displaying messages
class Console {
public:
    void print(const std::string& message) const {
        std::cout << message << std::endl;
    }
};

// Logger class depends on Console class
class Logger {
private:
    Console console;

public:
    void log(const std::string& message) const {
        console.print("LOG: " + message);
    }
};

int main() {
    Logger logger;
    logger.log("This is a log message.");

    return 0;
}
```

## Association:
---
![[Pasted image 20230801160437.png]]

Two classes have "equal" status (not like one is a part of or belongs to another)
can break/separate and bind to another

Example: Colony and Predator

```cpp
class project;	// forward declaration

class contractor
{
    private:
        project* theProject;
}

class project
{
    private:
        contractor* theContractor;
}
```

## Fake ant colony Project:
---
```cpp
// Ant colony model

// Inheritance (general to specific)
// Parent/Child - ant is parent, queen is child
// superclass/subclass - ^
// ancestor/desendant - ^

// Semantic terms: is a, is like a, is a kind of, etc.

// Directionality: unidirectional
// Binding: strong/tight

// Ant (designation, eat, work, etc.)
// Queen (breed, lay eggs, +noraml ant)
// Soldier (protect)
// Worker
// Foragers
// Transporters
```


## Using Multiple Files:
---
==must have both `.h` and `.cpp` files per external class==
`.h` files include all of declarations for the `class`
EX:
```cpp
//#pragma once // maybe not industry standard

// USE THIS INSEAD OF PRAGMA ONCE
#ifndef _ANT_H_ // has to be unique and match to 
#define _ANT_H_

class FoodCache {
private:
	int amount = 0;
public:
	FoodCache(int amount);
	void addFood(int amount);
}
```

`.cpp` files is where you write your class
EX:
```cpp
#include <iostream> // must be above .h file
using namespace std;
#include "FoodCache.h"
FoodCache::FoodCache(int amount) {
	this->amount = amount;
}
void FoodCache::addFood(int amount) {
	cout << "Adding: " << amount << " items to food cache.";
	this->amount = amount;
}
```

#### Ant Colony:
---
ant colony:
main file:
```cpp
#include <iostream>
using namespace std;
#include "foodCache.h" // include after everything else

int main() 
{
	FoodCache cache(25);
	cache.addFood(15);
}
```

foodCache.h
```cpp
#pragma once // maybe not industry appropriate

class FoodCache {
private:
	int amount = 0;
public:
	FoodCache(int amount);
	void addFood(int amount);
}
```

foodCache.cpp
```cpp
#include <iostream> // must be above .h file
using namespace std;
#include "FoodCache.h"
FoodCache::FoodCache(int amount) {
	this->amount = amount;
}
void FoodCache::addFood(int amount) {
	cout << "Adding: " << amount << " items to food cache.";
	this->amount = amount;
}
```

Ant.h
```cpp
#pragma once 
#include <string>
#include "FoodCache.h"

class Ant {
private:
	int stamina = 0;
protected:
	string designation;
	bool survive(int value);
public:
	Ant(string designation);
	void eat(int amount, FoodCache cache);
}
```

Ant.cpp
```cpp
#include <string>
#include "FoodCache.h"
using namespace std;

Bool Ant::survive(int value) {
	return rand() % value;
}
Ant::Ant(string designation) : designation(designation) {
	cout << "Creating " << desigation << " ant" << endl;	
}

void Ant::eat(int amount, FoodCache cache) {
	cout << "Ant eats for " << amount << " from food cache.";
}
```

Queen.h
```cpp
#ifndef _QUEEN_H_
#define _QUEEN_H_

#include <string>
#include "Ant.h"
using namespace std;

class Queen : public Ant {
public:
	Queen (string designation = "Queen");

	void breed(int amount);
}
```

Queen.cpp
```cpp
#include <iostream>
using namespace std;
#include <string>
#include "Ant.h"

Queen (string designation = "Queen") {
	
}

void breed(int amount);
}
```