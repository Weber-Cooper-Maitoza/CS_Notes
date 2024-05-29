## Basics that are different:
- no semicolons needed 
- no main function needed
- don't have to import libraries

## Variables:
One and only way to create a variable is to use `var`. 
Example:
```swift
var playerName = "cooper"   // string
var age = 21                // int
var temperature = 72.6      // double
var activeMember = true     // bool

// If not value is given
var bonusScore: Int
var secondPlayer: String
var levelCompleted: Bool
var ProgressPercentage: Double
```

## Casting (Changing data types):
doesn't do this automatically at ALL!
need to explicitly state when and what to cast.
```swift
var score = 1
var highScore = 100.0

highScore = Double(score)
```

## Constants:
==TRY TO USE LET MORE THAN VAR==
can only set once and cannot change after.
must use key word `let`
Example:
```swift
let myConstantMessage = "Hello"
myConstantMessage = "bye" // ERROR!!!

let iDontKnow: String
```

## Optionals:
When creating a variable without a value `var name: String` you cannot use it until it is initialized. 
==optionals== are used when a variable might have not value at all.
```swift
var firstName: String    // normal variable
var middleName: String?  // Optional String, if nothing then nil (null)
var lastname: String
```

doing things to optional variables:
1. need to check if nil or not nil
2. if not nil, then unwrap value and set that value to a new var
```swift
if optionalInt != nil {
	var unwrappedInt = optionalInt! // <- '!' unwraps the optional
}
```

better way to unwrap optionals (optional binding):
```swift
// this is "optional binding"
if let unwrappedInt = optionalInt {
	print(unwrappedInt)
} else {
	// there's not value
}
```

## Operators:
New operators:
- Closed Range Operator `...` a range of value (start `...` end) it is ==inclusive==
- Half-Open Range Operator `..<` EX. 1`..<`10 -> 1, 2, 3, 4, 5, 6, 7, 8, 9
- `===`: Identity operator is used only with classes or objects of classes to check if they are referencing the same instance.
```swift
if firstMessage === secondMessage {
	print("Yes - they are references to the same instance")
}
```
## Data Structures:

### Arrays:
- 0 based 
- Type-safe
- Mutable(var) or immutable(let)
```swift
var names = ["cooper", "tia", "mitch", "kade", "azi"]
let speedLimits = [15, 25, 30, 40, 60, 75]

names[0] = "connor"
speedLimits[0] = 10 // DOESNT WORK!!!!! because its "let"

names.append("brody")
names.removeLast() // returns the last name and removes it. 

// Type anotation for an array of strings
var myStringArray: [String] = []
```

## Conditional Statements:

### IF / ELSE:
```swift
if score > 10 {
	print("score is 10")
}
```
all conditions must be True or False (not 1 or 0)

### Switch:
==CANNOT HAVE FALL THROUGH==
==Must be Exhaustive==
==EXECUTABLE CODE in each case==
doesn't need a break after each case but can still have one.
```swift
let volcanoExplosivityIndex: int.   // could be 0 or 8

switch volcanoExplosivityIndex {
case 0, 1, 2:
	print("Effusive")
case 3...7: // 3 to 7 (range operator)
	print("Effusive")
case 8:
	print("Mega-colossal")
default:
	print("not a recognized index")
}

```

## Loops:
3 loops in swift:
- While
- repeat-while (do while)
- for-in

### For in loop:
```swift
let bunchOfWords = ["the", "quick", "red", "fox", "jumped", "over"
					"the", "lazy", "dog"]

for word in bunchOfWords {
	print(word)
}
```

### Stride:
if you want to step greater than one at a time then you want to use ==stride==
Example:
```swift
for number in stride(from: 0, through: 256, by: 16) {
	print(number)
}
```


## String interpolation:
REMEMBER `\()`
EXAMPLE:
```swift
// string interpolation

// some example data
var trackName = "Ambre"
var artistName = "Nils Frahm"
var duration = 228

// ...
let message = "Now playing \(trackName) by \(artistName) which is \(durration / 60)m \(duration % 60)s long."

print(message)
```

## Functions / methods:
parentheses are required
==Any parameters passed in functions are CONSTANTS and IMMUTABLE by default==
```swift
func showMessage(number: Int, name: String) {
	print("This function call worked.")
	print("You passed in \(number).")
	print("Your name is \(name).")
}

showMessage(number: 42, name: "cooper")
```

A function type looks like this `(String) -> Bool` or `() -> Void`
### Returning functions:
to return you must use `-> type` 
```swift
function basicFunction() -> String {
	let str = "This is a simple function."
	print(str)
	return str
}

let result = basicFunction()
```

### Customizing argument labels:
to remove Argument Label use `_ ` (you need the space after \_)
```swift
func showMessage(_ message: String) { // <-----------
	print("The text passed in was: \(message).")
}

// call...
showMessage("fourty two")
```

to change argument label you do this:
```swift
func showMessage(printMessage message: String) { // <-----------
	print("The text passed in was: \(message).")
}

// call...
showMessage(printMessage: "fourty two")
```

Some standards:
use `type(of: blah)` instead of `typeOf(of: blah)`

## Enumerations:
lets you create your own data type that can be restricted to what ever you want.
```swift
enum MediaType {    // Start capatalized
	case book
	case movie
	case music
	case game
}

// use....
var itemType: MediaType
itemType = MediaType.book

// later...
itemType = .music    // dont have to write type "MediaType"
```

raw values enumerations:
```swift
enum BottleSize: String {
	case half = "37.5 cl"
	case standard = "75 cl"
	case magnum = "1.5 Liters"
}

var myBottle: BottleSize = .standard
print("Your \(myBottle) is \(myBottle.rawValue)")
// Your standard is 75 cl
```

## Structures:
Cannot leave a struct ==instance== half baked (completed).
a struct is called a ==value type== in Swift
```swift
struct Movie {
	// properties
	var title: String
	var director: String
	var releaseYear: Int
	var genre: String

	// methods
	func summary() -> String {
		return "\(title) is a \(genre) film released in \(releaseYear) and directed by \(director)"
	}
}

// have to fill out completely
var first = Movie(title: "Arrival", director: "Denis Villeneuve", releaseYear: 2016, genre: "Science Fiction")
var second = Movie(title: "Sing Street", director: "John Carney", releaseYear: 2017, genre: "Comedy Musical")

print(first.title)
print(second.title)
second.releaseYear = 2016     // can only do because propertie is "var"

print(first.summary())
print(second.summary())
```

## Dictionaries:
![[Pasted image 20240511084637.png]]

```swift
// Dictionaries

var airlines = ["SWA": "Southwest Airlines", 
				"BAW": "British Airways", 
				"BHA": "Buddah Air", 
				"CPA": "Cathay Pacific" ]

// use [ ] to look up a key 
if let result = airlines["SWA"] {   // OPTIONAL TYPE MIGHT RETURN NIL
	print(result)    // kind of unwraps	
} else {
	print("No Match found")
}

// add or change
airlines["DVA"] = "Discovery Airlines" // this will add a new key/value

// remove by setting to nil
airlines["BHA"] = nil

// Dictionary of String keys and String values
var periodicElements: [String: String]

// Dictionary of Int keys and String values
var employees: [Int: String]

// Iterating through a dictionary
for (code, airline) in airlines {    // Tuple
	print(airline)
}
```

## Tuples:
to create a tuple use `(<value1>, <value2>, <value3>, ...)`
```swift
let cameraType = "Canon"
let photoMode = true
let shutterSpeed = 60
var iso = 640
var aperture = "f1.4"

var basicTuple = (aperture, iso, cameraType)

// can mix literals, constants, variables
var nextTuple = ("Sreing literal!", photoMode, 23124, cameraType)
```

### Returning a tuple from a function
```swift
func randomAlbum() -> (albumTitle: String, length: Int) {   // can use labels or not
	let title = "And in the endless pause there came the sound of bees"
	let duration = 2462

	return (title, duration)
}

// clunky way
let result = randomAlbum()
print(result.0) // think like a simple array (0 = String, 1 = Int)
print(result.albumTitle)
print(result.length)

// better way
let (nextTitle, length) = randomAlbum()
print("Playing next: \(nextTitle)")
print("Which is: \(length / 60)m \(length % 60)m")
```

## Closures:
"Closures let us take lines of code and group it together to use elsewhere in our program."
kind of like ==lambdas==

Closures look like this in regards to function type:
```swift
func contains(Element) -> Bool
```
`(Element) -> Bool`: takes Element and returns Bool

Sorting an array of BOOKS:
![[Pasted image 20240511092852.png]]

need to provide a CLOSURE that takes `(Element, Element)` or (Book, Book) and returns Bool 
==(You can think of this as "how can the sorting algorithm figure out how to compare the CUSTOM elements so it can sort")== Thus a closure is like a lambda
EXAMPLE:
```swift
// are these two Book elements in the right order alread?
if firstBook.readingAge <= secondBook.readingAge {
	return true
} else {
	return false
}
```


EXAMPLE:
![[Pasted image 20240511093559.png]]
```swift
let allBooks = [book1, book2, book3, book4, book5]

// verbose and clunky way of doing this
func compareTwoBooks(firstBook: Book, secondBook: Book) -> Bool {
	if firstBook.readingAge <= secondBook.readingAge {
		return true
	} else {
		return false
	}
}

let ageSortedBooks = allBooks.sorted(by: compareTwoBooks) // not calling the function but passing the code it's using

ageSortedBooks // the new array sorted

// HOW TO ACTUALLY DO THIS!!!!
// 1. remove func compareTwoBooks
// 2. put parameters and return in curly brace
// 3. use 'in' to seperate function type with code
// 4. paste into function at takes the closure
let ageSortedBooks = allBooks.sorted(by: {
	(firstBook: Book, secondBook: Book) -> Bool 
	in
	if firstBook.readingAge <= secondBook.readingAge {
		return true
	} else {
		return false
	}
})

// CAN SHORTEN EVEN FURTHER
let ageSortedBooks = allBooks.sorted(by: {
	// type inference. dont need
	//(firstBook: Book, secondBook: Book) -> Bool 
	//in
	
	//if firstBook.readingAge <= secondBook.readingAge {
	if $0.readingAge <= $1.readingAge {
		return true
	} else {
		return false
	}
})

// CAN SHORTEN EVEN EVEN FURTHER
// TRAILING CLOSURE
let ageSortedBooks = allBooks.sorted {
	if $0.readingAge <= $1.readingAge {
		return true
	} else {
		return false
	}
}

// CAN SHORTEN EVEN EVEN EVEN FURTHER
let ageSortedBooks = allBooks.sorted {return $0.readingAge <= $1.readingAge}

// CAN SHORTEN EVEN EVEN EVEN EVEN FURTHER
let ageSortedBooks = allBooks.sorted {$0.readingAge <= $1.readingAge}

let shortestToLongest = allBooks.sorted { $0.pageCount <= $1.pageCount }

// create a filtered array
let booksForUnder10s = allBooks.filter { $0.readingAge < 10 }
```

## Classes and Objects:
### Defining and Instantiating Classes
```swift
class Appliance {
	// properties
	var manufacturer: String = ""
	var model: String = ""
	var voltage: Int = 0
	var capacity: Int?

	// methods
	func getDetails() -> String {
		// self is like 'this'
		var message = "This is the \(self.model) from \(self.manufacturer)."	
		if self.voltage >= 220 {
			message += "This model is for European usage"	
		}
		return message
	}
}

// ...later, create an instance of Appliance
var kettle = Appliance()
kettle.manufacturer = "Megappliance, Inc"
kettle.model = "TeaMaster 5000"
print(kettle.getDetails())
```

### Adding initializers and de-initializer:
```swift
class Appliance {
	// properties
	var manufacturer: String = ""
	var model: String = ""
	var voltage: Int = 0
	var capacity: Int?

	// methods
	func getDetails() -> String {
		// self is like 'this'
		var message = "This is the \(self.model) from \(self.manufacturer)."	
		if self.voltage >= 220 {
			message += "This model is for European usage"	
		}
		return message
	}

	// initializer (constructor)
	init() 
		self.manufacturer = "default manufacturer"
		self.model = "default model"
		self.voltage = 120
	}

	// additional initializer
	init(withVoltage: Int) {
		self.manufacturer = "default manufacturer"
		self.model = "default model"
		self.voltage = withVoltage
	}

	// de-initializer
	deinit {
		// preform cleanup code here...
		// release a file resource...
		// release a network resource...	
	}
}

var cafatiere = Appliance(withVoltage: 220)
```

SIDE NOTE:
ARC (automatic reference counting) is Swift's garbage collector. This is responsable for dealocating and freeing memory that isn't being used anymore.

## Differences between Structs and Classes:
1. Structs have ==Member-wise initializers==, classes do not
```swift
// can only do if Struct
var toaster = Appliance(manufacturer: "AcmeCorp", model: "Toastmatic")
```

2. Classes support inheritance. Structs do not.

![[Pasted image 20240511104041.png]]

Structs and enums are copied when assigned to a new variable and original cannot be changed by updating the copy.

## Inheritance:
```swift
class Appliance {             // SUPERCLASS
	var make: String
	var model: String
	init() {
		self.make = "default"	
		self.model = "default"
	}
	final func printDetails() { // final stops from being inhereted
		print("Make: \(self.make) \nModel: \(self.model)")
	}
}

// define a new class
class Toaster: Appliance {    // SUBCLASS
	// new property
	var slices: Int

	override init() {
		self.slices = 2
		super.init() // access the inhereted init class
	}

	// new method
	func toast() {
		print("Irradiating now...")
	}
}

var myToaster = Toaster()
```

## Extensions:

### Adding Functionality with Extensions
```swift
extension String {
	func removeSpaces() -> String {
		let filteredCharacters = self.filter { $0 != " " }
		return String(filtertedCharacters)
	}
}

let album = "Decks and drums and rock and roll"
let scriptio = "Neque porro quisam est qui dolorem ipsum quia dolor sit amet"
let phrase = "Lov is now here"

print(album.removeSpaces())
print(scriptio.removeSpaces())
print(phrase.removeSpaces())
```

## Computed Properties:
```swift
class Player {
	// stored properties
	var name: String
	var livesRemaining: Int
	var enemiesDestroyed: Int
	var penalty: Int
	var bonus: Int

	// computed property
	var score: Int {
		get {
			return (enemiesDestroyed * 1000) + bonus + (livesRemaining * 5000) - penalty	
		}	
		set { 
			print("you passed in \(newValue).")	
		}
	}

	init(name: String) {
		self.name = name
		self.livesRemaining = 3
		self.enemiesDestroyed = 0
		self.enalty = 0
		self.bonus = 0	
	}
}


let newPlayer = Player(name: "Ava")

newPlayer.enemiesDestroyed = 326
newPlayer.penalty = 872
newPlayer.bonus = 25000

print("The final score is: \(newPlayer.score)")
newPlayer.score = 125000
// output: "you passed in 125000."
```

Shorthand for a readonly computed property:
```swift
var score: Int {
	return (enemiesDestroyed * 1000) + bonus + (livesRemaining * 5000) -
		penalty	
}
```

## Protocols:
Protocol - a set of rules or code of behavior 
```swift
protocol MyProtocol {
	// what methods are required?
	func showMessage()

	// what properties?
	var name: String { get }
}

struct MyStruct: MyProtocol {
	// need showMessage function
	func showMessage() {
		print("Hello world")
	}

	var name: String {
		return "sebastioan"
	}
}
```


```swift
class Player: CustomStringConvertible {
	// stored properties
	var

	var description: String {
		return "Player..."
	}
}
```

## Error Handling:
1. define the error
2. throw the error
3. handle the error
```swift
enum ServerError: Error{ // Error is a protocol that you dont have to add
	case noConnection
	case serverNotFound
	case authenticationRefused
}

fucn checkStatus (serverNumber: Int) throws -> String {
	switch serverNumber {
	case 1:
		print("You have no connection.") 
		throw ServerError.noConnection
	case 2:
		print("Authentication failed.") 
		throw ServerError.authenticationRefused
	case 3:
		print("Server 3 is up and running!") 
	default:
		print("Cant find server.") 
		throw ServerError.serverNotFound
	}
	return "Success!"
}
```

## Do-Catch and Try:
How to handle a error
```swift
do {
	let result = try checkStatus(serverNumber: 1)
	print(result)
} catch ServerError.noConnection {
	print("No connection.")	
} catch {
	print("The problem is: \(error)")
}

let result: String?

do {
	result = try checkStatus(serverNumber: 3)
} catch {
	result = nil
}

// better way
let result = try? checkStatus(serverNumber: 1)

if result != nil {
	print(result!)
}
```

## Guard and Defer:
Guard - like an if else statement
```swift
guard some-condition-i-need-to-be-true else {
	what-we-do-if-it-isn't
}

guard let unwrappedVal = optionalVal else {
	//what be do if it isn't true
	// return / throw / break / continue
}
```

Defer - will be called just before you exit the code block youre in
```swift
func someFunction() {
	defer {
		// your clean-up code	
	}
	// code...
}
```