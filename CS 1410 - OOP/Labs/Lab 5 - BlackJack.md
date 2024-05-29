```cpp
#include <cctype>
#include <iostream>
#include <string>
using namespace std;

enum Suit {HEARTS, DIAMONDS, CLUBS, SPADES}; // 0, 1, 2, 3

struct Card { 
    int value; // int 2-14 face value 
    Suit suit; // enum 0-3 hearts-spades
};

Card getRandomCard();
void showCard(Card card);
void dealCardAndTotal(int &, int &);

int main () 
{
    char contenue = 'y';
    do {
        srand(time(0));
        int playersAceCount = 0;
        int playerTotal = 0;
        int dealersAceCount = 0;
        int dealersTotal = 0;

        // Sets up dealers first card and adds the value to dealers total
        Card dealerFirstCard = getRandomCard(); 
        if (dealerFirstCard.value == 14){ // an ace
            dealersTotal += 11;
            dealersAceCount += 1;
        }
        else if (dealerFirstCard.value > 10) {
            dealersTotal += 10;
        }
        else {
            dealersTotal += dealerFirstCard.value;
        }
        cout << "Dealer: ";
        showCard(dealerFirstCard);
        cout << "|?|" << endl << endl;

        // deals players first two cards, adds to totals, and counts aces
        cout << "Player: ";
        dealCardAndTotal(playersAceCount, playerTotal);
        dealCardAndTotal(playersAceCount, playerTotal);
        cout << endl;
        cout << "Player Total: " << playerTotal << endl;

        // Game logic
        do{
            char option; 
            cout << "(H)it or (S)tand: ";
            cin >> option;

            if (toupper(option) == 'H'){
            dealCardAndTotal(playersAceCount, playerTotal);
            cout << endl << "Player Total: " << playerTotal << endl;
            if (playerTotal > 21){
                    cout << endl << "Player Busts!" << endl;
                    cout << "-----Dealer Wins-----" << endl;
                    break; 
            }
            } 

            else if (toupper(option) == 'S'){
                cout << "Dealer: ";
                showCard(dealerFirstCard);
                do {
                    dealCardAndTotal(dealersAceCount, dealersTotal);
                } while (dealersTotal <= 17);

                if (dealersTotal > 21){
                    cout << endl << "Dealer Busts!" << endl;
                    cout << "Dealer Total: " << dealersTotal << endl;
                    cout << endl << "-----Player Wins-----" << endl;
                    break;
                }
                else if (dealersTotal > playerTotal) {
                    cout << endl << "Dealer Total: " << dealersTotal << endl;
                    cout << endl << "-----Dealer Wins-----" << endl;
                    break;
                }
                else if (playerTotal > dealersTotal) {
                    cout << endl << "Dealer Total: " << dealersTotal << endl;
                    cout << endl << "-----Player Wins-----" << endl;
                    break;
                }
                else if (playerTotal == dealersTotal) {
                    cout << endl << "Dealer Total: " << dealersTotal << endl;
                    cout << endl << "Player Total: " << playerTotal << endl;
                    cout << endl << "Its a Tie!" << endl;
                }
            }

            else {
                cout << "Please enter a valid option." << endl;
            }

        } while (playerTotal > 21 || dealersTotal < 21);
        cout << "Would you like to play again? (y/n)" << endl;
        cin >> contenue;

    // Specifically for MAC OS 
        system("clear");
    } while (contenue == 'y');

    // Specifically for MAC OS 
    system( "read -n 1 -s -p \"Press any key to continue...\"; echo" );
}

Card getRandomCard() {
    Card card;
    card.value = rand() % 13 + 2; // gets value between 2 - 14
    int suitNumber = rand() % (SPADES +1); // gets value between 0 - 4
    switch (suitNumber) {
        case HEARTS: 
            card.suit = HEARTS;
            break;
        case DIAMONDS:
            card.suit = DIAMONDS;
            break;
        case CLUBS:
            card.suit = CLUBS;
            break;
        case SPADES:
            card.suit = SPADES;
            break;
    }
    return card;
}

void showCard(Card card) {
    string symbol;
    string cardValue;
    switch (card.suit) {
        case HEARTS:
    // Specifically for MAC OS 
            symbol = string("\u2665"); 
            break;
        case DIAMONDS:
    // Specifically for MAC OS 
            symbol = string("\u2666");
            break;
        case CLUBS:
    // Specifically for MAC OS 
            symbol = string("\u2663");
            break;
        case SPADES:
    // Specifically for MAC OS 
            symbol = string("\u2660");
            break;
    }
    switch (card.value) {
        case 14:
            cardValue = "A";
            break;
        case 13:
            cardValue = "K";
            break;
        case 12:
            cardValue = "Q";
            break;
        case 11:
            cardValue = "J";
            break;
        default:
            cardValue = to_string(card.value);
            break;
    }
    cout << "|" << cardValue << symbol << "|"; 
}

void dealCardAndTotal(int &aceCount, int &total){ //be carful of &
    Card newCard = getRandomCard();
    showCard(newCard);

    if (newCard.value == 14){ // an ace
        aceCount += 1;
        total += 11;
    }
    else if (newCard.value > 10) {
        total += 10;
    }
    else {
        total += newCard.value;
    }

    while (aceCount > 0 && total > 21) {
        aceCount -= 1;
        total -= 10;
    }
}


```