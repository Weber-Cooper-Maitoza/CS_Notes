### Color Conversion:
```cpp
#include <iostream>
#include <string>
using namespace std;

string conversion(int r, int g, int b);
string dec_hex(int n);

int main() {
    string delim;
    int r, g, b;
    cout << "Enter an RGB color in the format r, g, b: ";
    cin >> r >> delim >> g >> delim >> b;
    string hex_output = conversion(r, g, b);
    cout << "The hexadecimal equivalent is: #" << hex_output << endl;
}

string conversion(int r, int g, int b) {
    string converted_string;
    int first_hex_r = r/16, second_hex_r = r%16,
        first_hex_g = g/16, second_hex_g = g%16,
        first_hex_b = b/16, second_hex_b = b%16;
    converted_string = dec_hex(first_hex_r) +
                    dec_hex(second_hex_r) +
                    dec_hex(first_hex_g)  +
                    dec_hex(second_hex_g) +
                    dec_hex(first_hex_b)  +
                    dec_hex(second_hex_b);
    return converted_string;
}

string dec_hex(int n) {
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
            return to_string(n);
    }
}

```
### Input Validation:
```cpp
#include <iostream>
#include <string>
using namespace std;

string input(string statement, string option1, string option2);

int main() {

  string response = input("Go to the forest or the beach: ", "forest", "beach");
  cout << "You choose to go to the " << response << "." << endl;
}

string input(string statement, string option1, string option2) {
  string user_input;
  cout << statement;
  cin >> user_input;
  if (user_input == option1)
      return option1;
  else if (user_input == option2)
      return option2;
  else
      cout << "That is not a valid response" << endl;
}

```
### NIM:
```cpp
#include <iostream>
#include <cstdlib>

using namespace std;

bool isValidMove(int userMove, int stones);
int computerMove(int stones);

int main() {
    srand(time(0));
    int stones = rand() % 20;

    int userMove;
    int compMove;

    do {
        cout << "Stones in the pile: " << stones << endl;
        cout << "How many will you take? (1-3): ";
        cin >> userMove;

        if (not isValidMove(userMove, stones)){
            cout << "That's not a valid amount." << endl;
            cout << endl;
        }
        else{
            stones -= userMove;
            // if stones == 0, you lose
            if (stones == 0){
                cout << "________You Lose!________" << endl;
                break;
            }
            compMove = computerMove(stones);
            stones -= compMove;
            // if stones == 0, you win
            if (stones == 0){
                cout << "________You win!________" << endl;
                break;
            }
            cout << endl;
        }
    } while (stones > 0);
}

bool isValidMove(int userMove, int stones) {
    if (stones != 1 || userMove > stones){
        if ((userMove < 1) || (userMove > 3) || (userMove >= stones))
            return false;
        else
            return true;
    }
    else
        return true;
}

int computerMove(int stones){
    srand(time(0));
    int compMove = rand() % 2 + 1;
    if ((stones == 1) || (stones == 2)){
        cout << "Computer takes 1." << endl;
        return 1;
    }
    else if (stones == 3){
        cout << "Computer takes 2." << endl;
        return 2;
    }
    else if (stones == 4){
        cout << "Computer takes 3." << endl;
        return 3;
    }
    else{
        cout << "Computer takes " << compMove << "." << endl;
        return compMove;
    }
}
```