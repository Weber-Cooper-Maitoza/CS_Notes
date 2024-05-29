Next Topic: [[04 - Loops]]

## If statements:
---

## If else statements:
---

## Switch:
---
A decimal to hex conversition switch
```cpp
switch (n) {
	case 15:
		return "F";
	case 14:
		return "E";
	case 13:
		return "D";
	case 12:
		return "C";
	case 11:
		return "B";
	case 10:
		return "A";
	default:
		return n;
}
```



## Import:
---
```cpp
#include <iostream>

using namespace std;

int main() {
    // Control structures

    // Sequentially

    /*
    int x = 5;          // This runs first
    x += 10;            // This runs second
    cout << x << endl;  // This runs last
    */

    // Relational expressions: expression evaluates to true or false
    // Relational operators:
    // >, <, >=, <=, ==, !=, bool

    /*
    int student = 28;
    bool section = student > 20;

    int missing = 4;
    bool pass = missing <= 3;

    bool isRaining = true;

    // cout << isRaining << endl;

    int y = 5;

    cout << (y = 9) << endl;        // This is not evaluating if y equals 9
    cout << (y == 5) << endl;

    cout << y << endl;
    */

    // if statement (all-or-nothing)
    /*
    char play;
    cout << "Do you want to play a game? (y/n): " << endl;
    cin >> play;

    if (play == 'y')        // Char type use single quotes ''
    {
        cout << "Let's play." << endl;

        // if-else (coke-or-pepsi)
        cout << "I will hide a seed under 1 of 3 cups." << endl;

        srand(time(0));
        int cup = rand() % 3 + 1;

        int choice;
        cout << "Which cup will you choose? (1-3): ";
        cin >> choice;

        if (choice == cup) {
            cout << "That is correct, you win!" << endl;
        } else {
            cout << "Nope. It was in cup " << cup << endl;
        }
    }
    */
    // Common mistake: dangling else

    /*
    bool eggs = true;
    int milk = 0;

    if (milk) {
        if (eggs)
            milk = 12;
    }
    else
        milk = 1;

    cout << milk;
    */
/*
    // if-else if (shades of grey)
    srand(time(0));
    int player = rand() % 13 + 2;
    int computer = rand() % 13 + 2;

    cout << "\nYour card: " << player << endl;
    cout << "My card: " << computer << endl;

    if (player > computer)
        cout << "You win!" << endl;
    else if (computer > player)
        cout << "You lose!" << endl;
    else
        cout << "it's a WAR!" << endl;
*/
    // Logical operators (and = &&, or = ||, not = !)
    srand(time(0));
    int dice1 = rand() % 6 + 1;
    int dice2 = rand() % 6 + 1;

    cout << "|" << dice1 << "||" << dice2 << "|" << endl;

    // Want to check for anything EXCEPT 7
    if (!(dice1 + dice2 == 7)) {
        cout << "Keep Rolling" << endl;

        // AND operator: && (all rel. exp. must be true)
        if (dice1 == 2 && dice2 == 2)
            cout << "Hard 4" << endl;
        else if (dice1 == 3 && dice2 == 3)
            cout << "Hard 6" << endl;
        else if (dice1 == 4 && dice2 == 4)
            cout << "Hard 8" << endl;
        else if (dice1 == 5 && dice2 == 5)
            cout << "Hard 10" << endl;

        // OR operator: || (At least 1 rel. exp. must be true)
        // Win 7 or 11
        // Lose 2, 3, 12
        // any other sets the "point" value

        if (dice1 + dice2 == 7 || dice1 + dice2 == 11)
            cout << "Winner!" << endl;
        else if (dice1 + dice2 == 2 || dice1 + dice2 == 3 || dice1 + dice2 == 12)
            cout << "Loser!" << endl;
        else
            cout << "Point is " << (dice1 + dice2) << endl;

        // MADE UP: Total is 7 or 11 and second dice must be 5
        if ((dice1 + dice2 == 7 || dice1 + dice2 == 11) && dice2 == 5)
            cout << "Made up win!" << endl;

        // Short-circuit evaluation: compiler is lazy

        // TODO Maybe: nested somthing idk

        cout << endl << endl;

        srand(time(0));

        int guess;
        cout << "in which cup will the ball fall? (1, 2, 3, 4): ";
        cin >> guess;

        int roll1 = rand() % 2;     // between 0 and 1
        int roll2;

        if (roll1 == 0) {
            cout << "Ball rolls left" << endl;

            roll2 = rand() % 2 + 1; // between 1 and 2
            if (roll2 == 1) {
                cout << "Ball rolls left and lands in cup 1" << endl;
            } else {
                cout << "Ball rolls left and lands in cup 2" << endl;
            }
        } else {
            cout << "Ball rolls right" << endl;

            roll2 = rand() % 2 + 2; // between 2 and 3
            if (roll2 == 2) {
                cout << "Ball rolls left and lands in cup 3" << endl;
            } else {
                cout << "Ball rolls left and lands in cup 4" << endl;
            }

        }

        if (roll1 + roll2 == guess) {
            cout << "you win!";
        } else {
            cout << "you lose.";
        }

        // TODO: switches (every thing you can do with a switch you can do with an if statement)
        cout << endl << endl;
        // A switch uses a single variable for decisions/branching

        int choice = rand() % 3;

        switch (choice) {
            case 0:
                cout << "Rock" << endl;
                break;
            case 1:
                cout << "Paper" << endl;
                break;
            case 2:
                cout << "scissors" << endl;
                break;
        }


        cout << "There was an old lady who swallowed a..." << endl;

        int start = 3;

        switch (start) {
            case 7:
                cout << "...horse. She died of course." << endl;
                break;
            case 6:
                cout << "...cow to catch the..." << endl;
            case 5:
                cout << "...goat to catch the..." << endl;
            case 4:
                cout << "...dog to catch the..." << endl;
            case 3:
                cout << "...cat to catch the..." << endl;
            case 2:
                cout << "...bird to catch the..." << endl;
            case 1:
                cout << "...spider to catch the..." << endl;
            case 0:
                cout << "...fly..." << endl;
                break;
            default:
                cout << "That was not appart of the story" << endl;
        }

    }

}

```