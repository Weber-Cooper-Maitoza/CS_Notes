Next Topic: [[10 - UML]]

#### Object-Oriented Programming (OOP):
---
*Problem-solving by modeling after real-world concepts

Extensible:
*can create own types, classes, objects, etc. to expand upon the language

Three Faucets of OOP:
1. Encapsulation 
2. Inheritance
3. Polymorphism

### Class:
*Describe objects with the same attributes (properties) and operations (functions)

Metaphor 1 - Cookie Cutter 
Metaphor 2 - Blueprint
Metaphor 3 (Rhodes) - Think of it as an assembly line

Use `class` identifier in `PasscalCase`

Classes generally have ==3== parts (none of which are required):
- ==Attributes== (member values) - **properties
- ==Constructors== - **how you instantiate in object (from a class) 
- ==Member functions== - **what the instance (object) does

Feature visibility:
1. Private - access is restricted to the defining class
2. Public - access through out the program
3. Protected - access in the defining class and any subclasses

Classes in CPP have a `Default` Constructor (if no other constructor is defined, default is used)
If any other constructor is defined (expect default), default is no longer available.

#### Default values:
set a `class variable` default value in private area

#### Accessor/Mutator (getter/setter) functions:
- Accessor = `getter`
- Mutator = `setter`

```cpp
#include <iostream>
using namespace std;

class Avatar {
private: // make data members private
	string name;
	int health = 20;
	int maxHealth = 20;
	int strength = 100; // makes a class level variable 
	
	
public: // make constructors public
	Avatar() { // Default constructor
		name = "Anonymus";
	}
	
	Avatar(string aName) {
		name = aName;
	}

	// or use this format (Initilizer list notation)
	Avatar(string aName, int aHealth, int aStrength = 100) : name(aName), health(aHealth), strength(aStrength) {
		maxHealth = health;
	}

	string getName() { // use 'get' name for nameing getting functions
		return name; 	
	}

	int getStrength() {
		return strength;
	}

	int getHealth() {
		return health;
	}

	void setName(string aName) { // mutator function (setter) uses 'set' namestyle
		name = aName;
	}

	void setHealth(int aHealth) {
		health = aHealth;
		if (health < 0) 
			health = 0;
	}
	
	// Member functions
	void printFormattedHealth() {
		cout << name << ": ";
		for (int i = 0; i < health; i++)
			cout << char(3);
		for (int i = health; i < maxHealth; i++)
			cout << "-";

		cout << endl;
	}
};

int main() 
{
	Avatar player("Artimus");
	Avatar enemy1("skeleton", 25);
	Avatar enemy2("Princess", 40, 10000);
	Avatar enemy3;
	enemy1.setName("Golden Warrior");	

	player.setHealth(player.getHealth() - 50);
	cout << player.getHealth();
}

```