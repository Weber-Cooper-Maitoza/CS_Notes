### Number Guesser:
```cpp
#include <iostream>

using namespace std;

int main() {
    srand(time(0));
    int userNumber;
    int compNumber = rand() % 100 + 1;

    cout << "What Is Your Number: " << endl;
    cin >> userNumber;

    while (userNumber != compNumber) {

        if (userNumber > compNumber) {
            cout << "Too high!" << endl;
        }
        else if (userNumber < compNumber) {
            cout << "Too Low!" << endl;
        }

        cout << "What Is Your Number: " << endl;
        cin >> userNumber;
    }
    cout << "You got it!" << endl << "The number is [" << compNumber << "]" << endl;
}

```
### Rock Paper Scissors Lizard Spock:
```cpp
#include <iostream>
#include <list>
#include <ostream>

int main() {
  using namespace std;

  int user_option, play_again;
  const char *options[5] = {"Rock",
                            "Paper",
                            "Scissors",
                            "Lizard",
                            "Spock"};

  play_again = 1;
  while (play_again == 1) {
    srand(time(0));
    int comp_option = rand() % 5 + 1;

    // introduction
    cout << "Let's play Rock, Paper, Scissors, Lizard, Spock!" << endl;
    cout << "What will you choose?" << endl
         << "(1) Rock, (2) Paper, (3) Scissors, (4) Lizard, (5) Spock: ";

    // gather user's option
    cin >> user_option;
    cout << endl;
    cout << "You choose " << options[user_option - 1] << "." << endl;
    cout << "Computer chooses " << options[comp_option - 1] << "." << endl;
    cout << endl;

    if (comp_option == user_option) {
      cout << "It's a tie." << endl;
    }
    else if ((comp_option == 1 && user_option == 2) ||
               (comp_option == 2 && user_option == 3) ||
               (comp_option == 3 && user_option == 1) ||
               (comp_option == 5 && user_option == 4) ||
               (comp_option == 3 && user_option == 5) ||
               (comp_option == 4 && user_option == 1) ||
               (comp_option == 4 && user_option == 3) ||
               (comp_option == 2 && user_option == 4) ||
               (comp_option == 5 && user_option == 2) ||
               (comp_option == 1 && user_option == 5)) {
      cout << "You Win!" << endl;
    }
    else {
      cout << "You lost." << endl;
    }

    cout << "Play again? (1 - Yes, 2 - No): ";
    cin >> play_again;
    cout << endl;
  }
}

```
### Yahtzee:
```cpp
#include <algorithm>
#include <cstdlib>
#include <iostream>

using namespace std;

int main() {

    // Roll dice at random
    srand(time(0));
    int dice[5] = {};
    for (int i = 0; i < 5; i++)
        dice[i] = rand() % 6 + 1;

    // Sort the dice lowest to highest
    sort(dice, dice + 5);

    // Display the dice on the console
    for (int i = 0; i < 5; i++)
        cout << "|" << dice[i];
    cout << "|" << endl;

    // store the dice in integer value
    int d1 = dice[0], d2 = dice[1], d3 = dice[2], d4 = dice[3], d5 = dice[4];

    // TODO: complete the lab

    if (d1 == d2 && d2 == d3 && d3 == d4 && d4 == d5)
        cout << "\nYahtzee! 50 points" << endl;
    else if (d1 == (d2 - 1) && d2 == (d3 - 1) && d3 == (d4 - 1) && d4 == (d5 - 1))
        cout << "\nStraight: 40 points" << endl;
    else if ((d2 == (d3 - 1) && d3 == (d4 - 1) && d4 == (d5 - 1)) ||
             (d1 == (d3 - 1) && d3 == (d4 - 1) && d4 == (d5 - 1)) || //FIXME: write logic
             (d1 == (d2 - 1) && d2 == (d4 - 1) && d4 == (d5 - 1)) ||
             (d1 == (d2 - 1) && d2 == (d3 - 1) && d3 == (d5 - 1)) ||
             (d1 == (d2 - 1) && d2 == (d3 - 1) && d3 == (d4 - 1)))
        cout << "\nSmall Straight: 30 points" << endl;
    else if (((d1 == d2 && d2 == d3) && (d4 == d5)) ||
             ((d1 == d2) && (d3 == d4 && d4 == d5)))
        cout << "\nFull House: 25 points" << endl;
    else if ((d1 == d2 && d2 == d3 && d3 == d4) ||
             (d2 == d3 && d3 == d4 && d4 == d5))
        cout << "\n4 of a kind: " << (d3 * 4) << " points" << endl;
    else if ((d1 == d2 && d2 == d3) ||
             (d2 == d3 && d3 == d4) ||
             (d3 == d4 && d4 == d5))
        cout << "\n3 of a kind: " << (d3 * 3) << " points" << endl;
    else
        cout << "\nChance: " << (d1 + d2 + d3 + d4 + d5) << " points" << endl;
}

```