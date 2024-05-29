
## Overview:
---
Hijacks the features of other functions to work with your class

Overloads:
- Two or more functions with the same time but different parameters

```cpp
// int min(int a, int b);
min(4, 5); 

// double min(double a, double b);
min(4.5, 6.7); 

// char min(char a, char b);
min('a', 'b'); 
```

*Templates lets you fill in the blanks for other functions*

## Standard Template Library:
---
Standard Template Library (STL)
"*a collection of algorithms, containers, iterators, function objects (functors), and adaptors that can be used (and reused) to simplify C++ programs.*"

EX: `vector<Ant>`, `sort<Vial>`

Demonstration:
```cpp
class Word {
private:
	string word;
	int score;

public:
  Word() {
    word = "empty";
    score = rand() % 200;
  }

  Word(string word) : word(word) {
    score = rand() % 200;
  }

  Word(string word, int score) : word(word), score(score) {}
};
```

## How to Create a Template:
---

creating a template for ADD function.
```cpp
int add(int a, int b) {
	return a + b;
}

template <typename T>
T add(T a, T b) {
	return a + b;
}
```

`T` is a substitute variable.
Object needs an overloaded `+` for the template to work.

## Template to Make Smart Pointers:
---

