## Recursion:
---
program stack:
![[Pasted image 20231107174320.png]]

```cpp
#include <iostream>

using namespace std;

void counter(int val) {
	val++;
	if (val < 10) {
		counter(val);
	}
	count << val << endl;
}

int main() {
	counter(0);
	cin.get();
	return 0;
}
```

A loop with a stack.  Every function finishes 
USE CALL STACK

Most often used with branching 

## Parallel:
---
```cpp
unsigned int numRegions {100};
unsigned int nextTicket { };

void parallelCountSixes( ) {
	int myTicket{ -1 };
	int localCount{ 0 };	
	while (true) {
		theOneAndOnlyMutex.lock()
		myTicket = nextTicket;
		nextTicket++;
		theOneAndOnlyMutex.unlock()
		if (myTicket < numRegions) {
			
		  unsigned int startIndex{ N / numRegions * myTicket };
		  unsigned int endIndex{ N / numThreads * (threadID + 1) };
		  printf("I'm thread %u, starting my work before I die\n", threadID, startIndex, endIndex);
		  for (unsigned int i = startIndex; i < endIndex; ++i) {
		    if (arr[i] == 6) {
		      ++localCount;
		    }
		  }
		} 
		else {
			break;
		}
	}
}
```
Nov 7: 987650

EXAM 2: 14th through 20th

sort algorithms
big O
search and sort

## Trees:
---
the goal:
- Average: O(log n) 
- Worst: O(n)
![[Pasted image 20231109174806.png]]
depth - starting at o from the ROOT
height - starting at o from the farthest LEAF

A tree is:
1. one and only one Root Node
2. NO cycles
3. every parent must have 0, 1, or 2 children

can use a linked list

### Sorted Binary Trees
---
Average Lookup: O(log n)
worst  Lookup: O(n)
average insertion: O(log n)
Worst Insertion: O(n)

```cpp
#include <iostream>
#include <string>

using namespace std;

template <typename T>
struct Node {
	T data{};
	Node<T>* left{nullptr};
	Node<T>* right{nullptr};
}

template <typename T>
class SortedBinaryTree {
public:
	void insert(const T& data);
	void preOrder() const;
	void inOrder() const;
	void postOrder() const;
	void destroy() const;
	~SortedBinaryTree();
private:
	void preOrder(Node<T>* ptr) const;
	void inOrder(Node<T>* ptr) const;
	void postOrder(Node<T>* ptr) const;
	destroy(Node<T>* ptr) const;
	Node<T>* root{nullptr};
}


int main () {
	SortedBinaryTree<string> students;
	students.insert("Duck");
	students.insert("Pineapple");
	students.insert("Refried Beans");
	students.insert("Apple Sauce");
	students.insert("Garlic");
	students.insert("Cilantro");

	cin.get()
	return 0;
}
```

#### Insert Method:
```cpp
template <typename T>
void SortedBinaryTree::insert(const T& data) {
	Node<T>* newNode = new Node<T>;
	newNode->data = data;
	// Specific scenario: empty
	if (!root) {
		root = newNode;
		return;
	}
	// General scenario: 
	Node<T> curr = root;
	while (true) {
		if (data < curr->data) {
			if (!curr->left){
				// Nothing here, we insert here!
				curr->left = newNode;
				return;
			}
			else {
				// go left
				curr = curr->left;
			}
		} 
		else {
			if (!curr->right){
				// Nothing here, we insert here!
				curr->right = newNode;
				return;
			}
			else {
				// go right
				curr = curr->right;
			}
		}
	}
}
```

#### Traversal Method:
![[Pasted image 20231109185140.png]]
Use Recursion
sudo code:
#### Pre-order Traversal:
```cpp
if ( ptr ) {
	display
	recurse left
	recurse right
}
```

```cpp
template <typename T>
void SortedBinaryTree<T>::preOrder() const {
	preOrder(this->root);
}

template <typename T>
void SortedBinaryTree<T>::preOrder(Node<T>* ptr) const {
	if (ptr) {
		cout << "[" << ptr->data << "]" << " ";
		preOrder(ptr->left);
		preOrder(ptr->right);
	}
}

```

#### In-Order Traversal:
```cpp
template <typename T>
void SortedBinaryTree<T>::inOrder() const {
	inOrder(this->root);
}

template <typename T>
void SortedBinaryTree<T>::inOrder(Node<T>* ptr) const {
	if (ptr) {
		preOrder(ptr->left);
		cout << "[" << ptr->data << "]" << " "
		preOrder(ptr->right);
	}
}
```

####  Post-Order Traversal:
```cpp
template <typename T>
void SortedBinaryTree<T>::postOrder() const {
	postOrder(this->root);
}

template <typename T>
void SortedBinaryTree<T>::postOrder(Node<T>* ptr) const {
	if (ptr) {
		preOrder(ptr->left);
		preOrder(ptr->right);
		cout << "[" << ptr->data << "]" << " "
	}
}
```

#### Destroy method:
post-order, because the children need to die first then their parents.
```cpp
template <typename T>
SortedBinaryTree::~SortedBinaryTree() {

}
```
destroy public:
```cpp
template <typename T>
void SortedBinaryTree<T>::destroy() {
	distroy(this->root);
}
```
destroy private:
```cpp
template <typename T>
void SortedBinaryTree<T>::destroy(node<T>* ptr) {
	if (ptr) {
		distroy(ptr->left);
		distroy(ptr->right);
		delete ptr;
	}
}
```

#### Delete node method:
O(log n) 
find number candidates in between the left and right values.
go right once and then right as far as possible
