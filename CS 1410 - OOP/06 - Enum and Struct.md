Next Topic: [[07 - Strings]]

Aggregate Data: grouping data

## Enumeration:
---
Enumerations: a set of integer constants

first constant = 0

```cpp
enum {
    ROCK, PAPER, SCISSORS, LIZARD, SPOCK
};
```

- ROCK = 0
- PAPER = 1
- SCISSORS = 2
- LIZARD = 3
- SPOCK = 4

Use: *so you don't have to remember the number. It IS a constant. Used as a place holder f*

## Structures:
---
Structures: containers for storing, organizing, transporting, and accessing data ######

*a proto class*

```cpp
struct Book {
    string author;
    string title;
    double price;
    int number;
};

Book book1 = { "Petrie", "The Breaker", 17.99, 97818 }; //initilization
Book book2 = { "Doccichi", "The Breaker", 17.99, 97818 }; //initilization

Book book4;
book4.author = "Child";
```

### Import:
---
```cpp
#include <iostream>
using namespace std;

#define MAX_HEALTH 25
const int MAX_STAMINA = 30;

enum {
    ROCK, PAPER, SCISSORS, LIZARD, SPOCK
};

enum {
    STRENGTH = 20, CHARM, DEFENSE = 15, ATTACK, LOOKS
};

enum Color { RED, YELLOW, BLUE, GREEN, WILD };

struct Point {
    int x;
    int y;
};

struct UnoCard {
    int value;
    Color color;
};

struct Book {
    string author;
    string title;
    double price;
    int number;
};

void printBook(Book book);
Book makeNewBook(string title);

int main()
{
    // aggregate data: grouping data
    // C++ an extensible language

    // PascalCase
    // camelCase
    // snake_case
    // CAPS_CASE

    // Enumerations: a set of integer constants
        // Does it have to be upper case? - a lot of other programming languages do

    Color card1 = RED;
    Color card2 = BLUE;

    if (card1 == RED) {
        cout << "This card is red" << endl;
    }

    // Structures: containers for storing, organizing, transporting, and accessing data ######

    Book book1 = { "Petrie", "The Breaker", 17.99, 97818 }; // Copy-List initilization
    Book book2 = { "Doccichi", "The Breaker", 17.99, 97818 }; // List initilization

    printBook(book1);

    Book book4;
    book4.author = "Child";

    printBook(book4);

    Point pointA = {5, 6};
    Point pointB;

    pointB.x = 5;
    pointB.y = 6;

    // if (pointA.x >= 0 && pointA.x <= width) {
    //     // on the screen horizontally
    // }

    // skipping pointers

    // copying a struct
    Book book6 = book1;
    book6.title = "The ice man";

    printBook(book6);

    Book book7 = makeNewBook("Dune");
    printBook(book7);
     
    // Arrays (next time)
    // Classes 


    // cout << "Strength: " << STRENGTH << endl;
    // cout << "Charm: " << CHARM << endl;
    // cout << "DEFENSE: " << DEFENSE << endl;
    // cout << "ATTACK: " << ATTACK << endl;
    // cout << "LOOKS: " << LOOKS << endl;

    


}

void printBook(Book book) {
    cout << "Author: " << book.author << endl;
    cout << "title: " << book.title << endl; 
    cout << "Author: " << book.author << endl; 
    cout << "Author: " << book.author << endl;
    cout << endl;       
}

Book makeNewBook(string title) {
    Book book;
    book.title = title;
    return book;
}

```