Pearson correlation coefficient:
![[pearsonCorrelationCoefficient.png]]

Pearson Correlation Program:
`#include <strings> // Needed for getline()`

```cpp
const int SIZE = 1000; // make it big if you dont know limit
double set1[SIZE]; 
int index = 0; // Keep track of how many iterations

string input;
do {
	cout << "Enter a value for X set, leave blank to quit: ";
	getline(cin, input);

	if (!input.empty()) { // Reads string to see if string is empty
		if (!isdigit(input[0]) && !(input[0] == '-' && isdigit(input[1])))
			cout << "Please type numbers only." << endl;
		else {
			set1[index++] = stod(input);
			cout << "Adding " << stod(input) << "." << endl;
		}
	}
	
} while (!input.empty());

print(set1, index);

int size = index;
double* set2 = new double[size]; // To dynamically set size of "set2" durring runtime

string input2;
for (int i = 0; i < size; i++) {
	cout << "Enter value " << (i+1) << " of " << size << " for y set: ";
	getline(cin, input2);

	if (input2.empty() || !isdigit(input2[0]) && !(isdigit(input[0]) && !(input[0] == '-' && isdigit(input[1])))) {
		cout << "Please enter numbers only." << endl;
		i--; // Automatically rewind 'i' value 
	}

	else {
		set2[i] = stod(input2);
		cout << "Adding " << stod(input2) << " to set." << endl;
	}
}

print(set2, size);

cout << "Correlation coefficient: " << correl(set1, set2, size);

delete [set2];
```

Printing function:
```cpp
void print(double set[], int size) {
	for (int i = 0; i < size; i++)
		cout << "[" << set[i] << "]";
	cout << endl;
}
```

Mean function:
```Cpp
double mean(double set[], in size) {
	double total = 0;
	for (int i = 0; i < size; i++)
		total += set[i];
	return total / size;		
}
```

Correlation function:
```cpp
double correl(double x[], double y[], int size) {

	double meanX = mean(x, size);
	double meanY = mean(y, size);

	double numSum = 0;
	double xSquareSum = 0;
	double ySquareSum = 0;

	for (int i = 0; i < size; i++) {
		numSum += (x[i] - meanX) * (y[i] - meanY);
		xSquareSum += pow(x[i] - meanX, 2);
		ySquareSum += pow(y[i] - meany, 2);
	}

	return numSum / sqrt(xSquareSum * ySquareSum);
}	
```

Roll tracker mode function for midterm:
```cpp

// in main()
const in ROLL_COUNT = 1000;
srand(time(0));

int tracker[2][11] = { 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 };

for (int i = 0; i < ROLL_COUNT; i++) {
	int d1 = rand() % 6 + 1;
	int d2 = rand() % 6 + 1;
	
	int index = find(tracker[0], 11, d1 + d2);
	tracker[1][index]++;
}

cout << "Roll: ";
print(tracker[0], 11);

cout << "Count: ";
print(tracker[1], 11);

// use print() from top
int print(int a[], int size);

// find funtion
int find(int a[], int size, int value) {
	for (int i = 0; i < size; i++)
		if (a[i] == value)
			return i;
	return -1;
}
```