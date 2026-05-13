# Linked Lists

## Purpose: 



## Types:

* **(0) Singly Linked List** -> A list that can only be traversed in one direction, from the head to the node with null pointer which signifies the last node. Traversal to a certain Node would be $O(n)$ as you must pass from the head and through each Node before your target Node. They should contain a pointer to the next node or nullptr for designated final nodes of a list, and each node's respective data.

### Singly Linked List in C++:

```cpp
#include <iostream>
using namespace std;

struct SinglyNode {
    int data; //Node data
    SinglyNode* next; //A pointer to access the next node, must share name with struct, the "next" is our own named variable which simply is for directing to the next Node, if any
};

void ShowNode(SinglyNode* n) {
    while (n != nullptr) {
        cout << n->data << " -> ";
        n = n -> next; // Move to the next node then repeats until reached null pointer
    }
    cout << "Null Pointer" << endl;
}
int main() {
    // Create nodes by NodePointer nodeName = new StructName();
    SinglyNode* car1 = new SinglyNode();
    SinglyNode* car2 = new SinglyNode();
    SinglyNode* car3 = new SinglyNode();
    SinglyNode* car4 = new SinglyNode();
    SinglyNode* car5 = new SinglyNode();
    
    // Set the data of a node
    car1 -> data = 0;
    // Direct the next node
    car1 -> next = car2;
    
    // Repeat for every Node until the last one, car5 in this case
    car2 -> data = 10;
    car2 -> next = car3;
    
    car3 -> data = 20;
    car3 -> next = car4;
    
    car4 -> data = 30;
    car4 -> next = car5;
    
    car5 -> data = 40;
    // Because this will be our last node, we put a null pointer so it can avoid crashing.
    car5 -> next = nullptr;
    
    ShowNode(car1);
    
    // Delete nodes after usage to prevent memory leak, dont forget that.
    delete car1;
    delete car2;
    delete car3;
    delete car4;
    delete car5;

    return 0;
}
```

Output: 
```
0 -> 10 -> 20 -> 30 -> 40 -> Null Pointer
```


* **(1) Doubly Linked List** -> A variation of Singly Linked list that allows traversal in both directions; forward and backward, which requires the addition of an extra pointer which we will refer to as a "previous" pointer, along with the "next" pointer, and the node data.

The previous pointer prevents the need for having to start once again traversing from the head, essentially functioning as a checkpoint, like when you die in a game and you respawn there instead of the very start, saving you from having to travel again to where you left off. More flexible in general than Singly but would need more memory given the extra pointer.

```cpp
struct DoublyList {
  int data;
  DoublyList* next;
  DoublyList* prev; // The checkpoint i just mentioned, allows for bidirectional traversal
}
```

We would want to point the previous destination of the head node to null, since the head itself is already the first, and none come before that; making it pointless to try and traverse there.
```
// Not C++, just a representation of how I visualize it, haven't learned how to attach graphics to Github
(1) Head Node {
  // Components of a node, lets consider these inside the bracket to be
  DoublyList* data = 10
  DoublyList* next -> Node2
  DoublyList* prev -> nullptr

(1) Every following Node {
  DoublyList* data = Multiplies of 10 starting at 10 * 2, lets suppose theres 4 more Nodes after the head, therefore being 20, 30, 40, and 50
  // If not final Node
  DoublyList next -> NextNode
  DoublyList prev -> Their previous node (if any), Node 2's prev would be the head
  // If final Node
  DoublyList next -> nullptr
  DoublyList prev -> if we are to have 5 nodes, this must point to the 4th node. 
```

Now let's have a full implementation.

### Doubly Linked List in C++:

```cpp
#include <iostream>
using namespace std;

struct DoublyNode {
    int data; // Node data
    DoublyNode* next; // Pointer to next node, if any
    DoublyNode* prev; // Pointer to the previous node, serving as a checkpoint we can traverse from, if any. This is the key difference between Doubly and Singly
};
// Visualizaer of our Node traversal and displaying their data in order, traversed in O(n)
void ShowNode(DoublyNode* n) {
    DoublyNode* storage = n; //We start at the head, of course
    DoublyNode* last = nullptr;
    
    while (storage != nullptr) {
        cout << storage->data << " < - > ";
        last = storage; // Sets the last node to the already outputed Node
        storage = storage -> next; // Move to the next node then repeats until reached null pointer
    }
    cout << "Null Pointer" << endl;
    
    // Lets try to traverse backwards using the properties of a Doubly Linked List
    while (last != nullptr) {
        cout << last -> data << " < - > ";
        last = last -> prev;
    }
    cout << "Null Pointer" << endl;
}

    
int main() {
    // Create nodes by NodePointer nodeName = new StructName();
    DoublyNode* car1 = new DoublyNode();
    DoublyNode* car2 = new DoublyNode();
    DoublyNode* car3 = new DoublyNode();
    DoublyNode* car4 = new DoublyNode();
    DoublyNode* car5 = new DoublyNode();
    
    // Set the data of a node
    car1 -> data = 10;
    car1 -> next = car2;
    car1 -> prev = nullptr;
   
    
    // Repeat for every Node until the last one, car5 in this case, including setting the previous into the... previous node.
    car2 -> data = 20;
    car2 -> prev = car1; 
    car2 -> next = car3;
    
    car3 -> data = 30;
    car3 -> prev = car2;
    car3 -> next = car4;
    
    car4 -> data = 40;
    car4 -> prev = car3;
    car4 -> next = car5;
    
    car5 -> data = 50;
    car5 -> prev = car4;
    car5 -> next = nullptr;
    
    ShowNode(car1);
    
    // Delete nodes after usage to prevent memory leak, dont forget that.
    delete car1;
    delete car2;
    delete car3;
    delete car4;
    delete car5;

    return 0;
}
```

Output: 
```
10 < - > 20 < - > 30 < - > 40 < - > 50 < - > Null Pointer
50 < - > 40 < - > 30 < - > 20 < - > 10 < - > Null Pointer
```

### * **(2) Circular Linked List** -> A linked list without any null pointers, because the previous Node of the head (first) Node will be the last Node, and the next Node of the last Node, will be the head Node.
Imagine you are playing UNO! with 4 of your friends, you start first, then 2 more friends play their cards, and finally the last friend plays theirs too. Instead of the game ending right there, it is your turn again (pointing to the first Node after last) and so on until the game ends.

But then there's the iconic Reverse card that inverts the turn order. You were initially the first player, and your friend the last. After they play the card, the turn order inverts itself, and instead of becoming your turn after theirs, it becomes the turn of the previous player and would take quite the time to become your turn again. This can be directly referred to as Reversing Linked Lists, a topic gaining popularity for reasons I am yet to know, more on that later on let's get the fundamentals first.

####  * ** (2.a) Circular Singly List** -> A linked list traversing in a single direction, but instead of the last node pointing to null pointer, it sends you back to head.

####  * ** (2.b) Circular Doubly List** -> Very similar to its Singly variant, except it traverses in both directions and through previous Nodes, also with the last node's next node being the head and the head's previous node being the last node.

One can simply draw a circle, mark two ends, and one can be interpreted as the head (first) and the other the last, which moves back to the head after a cycle or end.

### Circular Doubly Linked List in C++:

```cpp

#include <iostream>
using namespace std;

struct DoublyNode {
    int data; // Node data
    DoublyNode* next; // Pointer to next node, if any
    DoublyNode* prev; // Pointer to the previous node, serving as a checkpoint we can traverse from, if any. This is the key difference between Doubly and Singly
};
// Visualizaer of our Node traversal and displaying their data in order, traversed in O(n)
void ShowNode(DoublyNode* n, int iterations) {
    if (n == nullptr) return;
    
    DoublyNode* storage = n;
    cout << "Traversing [" << iterations << "] times" << endl;
    
    for (int i = 1; i <= iterations; i++) {
        cout << "Node #" << i << " contains: " << storage -> data << " -> ";
        storage = storage -> next;
        
        if (i % 5 == 0) {
            cout << "\nLoop #" << i/5 << endl << endl;
        }
    }
    
}
    
int main() {
    // Create nodes by NodePointer nodeName = new StructName();
    DoublyNode* car1 = new DoublyNode();
    DoublyNode* car2 = new DoublyNode();
    DoublyNode* car3 = new DoublyNode();
    DoublyNode* car4 = new DoublyNode();
    DoublyNode* car5 = new DoublyNode();
    
    // Set the data of a node
    car1 -> data = 10;
    car1 -> next = car2;
    car1 -> prev = car5;
   
   
    car2 -> data = 20;
    car2 -> prev = car1; 
    car2 -> next = car3;
    
    car3 -> data = 30;
    car3 -> prev = car2;
    car3 -> next = car4;
    
    car4 -> data = 40;
    car4 -> prev = car3;
    car4 -> next = car5;
    
    car5 -> data = 50;
    car5 -> prev = car4;
    car5 -> next = car1;
    
    ShowNode(car1, 20); // Set # of iterations
    
    
    // We should also break the circular list after it has done what its asked to before deleting the nodes themselves. 
    car5 -> next = nullptr;
    car1 -> prev = nullptr;
    
    // Delete nodes after usage to prevent memory leak, alternatively can be done dynamically in another class
    delete car1;
    delete car2;
    delete car3;
    delete car4;
    delete car5;
    

    // Just learned now that it is a great practice to set a node to a null pointer after deleting its pointer, preventing working with garbage data if ever accessed
    car1 = nullptr;
    car2 = nullptr;
    car3 = nullptr;
    car4 = nullptr;
    car5 = nullptr;
    
    // It would also be better practice to have these handled dynamically in another class/function, perhaps next time.
    return 0;
}
```
Output: 
```
Traversing [20] times
Node #1 contains: 10 -> Node #2 contains: 20 -> Node #3 contains: 30 -> Node #4 contains: 40 -> Node #5 contains: 50 -> 
Loop #1

Node #6 contains: 10 -> Node #7 contains: 20 -> Node #8 contains: 30 -> Node #9 contains: 40 -> Node #10 contains: 50 -> 
Loop #2

Node #11 contains: 10 -> Node #12 contains: 20 -> Node #13 contains: 30 -> Node #14 contains: 40 -> Node #15 contains: 50 -> 
Loop #3

Node #16 contains: 10 -> Node #17 contains: 20 -> Node #18 contains: 30 -> Node #19 contains: 40 -> Node #20 contains: 50 -> 
Loop #4
```

Another great example would be turn-based role-playing games many of us love and spend time on, perhaps the first attacker (head node) will be your leftmost party member, then your second, and so on until... lets say your fourth party member, then the enemy will have their turn to attack, then it becomes your first party member's turn again and this repeats until either side all dies first.

## Operations:

* **Insertion** - Add a new element/data at the beginning of the list
* **Deletion** - Opposite of insertion, deletes an element/data also at the beginning of the list
* **Searching** - Searches for a specified data by travelling starting at the first node (head) by $O(n)$ until it finds a node containing said data.
* **Display** - Display the entire list, which contains all its nodes, respective data, and their next destination nodes
* **Delete** - Not to be confused with "Deletion", it deletes a target data in a certain node, also traversing linearly from the head to its destination.

## Linked List Operations (Singly)

* Insertion at Head - $O(1)$ since the head pointer is usually already known and is executed early given that the head is the beginning of a list.
  
* Insertion at Last Node - $O(n)$ as you must traverse from head to final node.
* Insertion after a certain Node - $O(n)$ as list traversal must start from head to target node, unless there is already a pointer to your target

``` cpp
// Online C++ compiler to run C++ program online
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// The C++ version of your "node" dictionary
struct Node {
    string data;
    Node* next;
};

// Helper function to create a "node"
Node* create_node(string data) {
    Node* new_node = new Node();
    new_node->data = data;
    new_node->next = nullptr;
    return new_node;
}

// Function to insert at head
Node* insert_at_start(Node* head, string data) {
    Node* new_node = create_node(data);
    new_node->next = head;
    return new_node; // This becomes the new head
}

// Function to insert at end
Node* insert_at_end(Node* head, string data) {
    Node* new_node = create_node(data);
    if (head == nullptr) {
        return new_node;
    }

    Node* current = head;
    while (current->next != nullptr) {
        current = current->next;
    }
    current->next = new_node;
    return head;
}

// Function to insert in between Nodes
Node* insert_between(Node* head, string target_data, string new_data) {
    Node* current = head;
    while (current != nullptr) {
        if (current->data == target_data) {
            Node* new_node = create_node(new_data);
            new_node->next = current->next;
            current->next = new_node;
            return head;
        }
        current = current->next;
    }
    cout << "Target " << target_data << " not found." << endl;
    return head;
}

void display_list(Node* head) {
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " -> ";
        current = current->next;
    }
    cout << "NULL" << endl;
}

int main() {
    Node* head = nullptr;
    int num_elements;
    string val;

    // Input initial elements
    cout << "How many Nodes?: ";
    cin >> num_elements;
    
    for (int i = 0; i < num_elements; i++) {
        cout << "Enter node data " << i + 1 << ": ";
        cin >> val;
        head = insert_at_end(head, val);
    }

    display_list(head);

    // Testing the three insertion types
    cout << "\n--- Manual Insertion at Head, End, and Between Nodes ---" << endl;
    
    cout << "Insert at START: ";
    cin >> val;
    head = insert_at_start(head, val);

    cout << "Insert at END: ";
    cin >> val;
    head = insert_at_end(head, val);

    string target;
    cout << "After which value should we insert in the MIDDLE? ";
    cin >> target;
    cout << "Value to insert: ";
    cin >> val;
    head = insert_between(head, target, val);

    cout << "\nFinal List:" << endl;
    display_list(head);

    return 0;
}
```
  
