# Stacks

You've seen them everywhere: your books, your papers, perhaps even playing cards. Those are examples of stacks you can common find in real life. Thankfully in Computer Science, it does not deviate too far from the stacks we are familiar with.

Observe that when stacking objects, suppose you start with an Ace of Diamonds. At first, it is the only card in the stack. Next, it is the bottom card with 51 more cards on top of it.

We call that "LiFo" or "Last-in-First-Out", and let's simplify that concept with the example I just gave: Try grabbing that specific Ace without touching or displacing the other cards. Nigh impossible right?

In a stack, the top is, as mentioned: the last piece of data inserted, and the first one inserted will be at the very bottom and would need everything else "popped" to access it. We'll get on to Stack Operations soon enough.

## Stack Operations 

* **(0). Pop()** - An operation that pops or deletes the last element inserted or the element at the top of the stack. This is O(1) since it only and will always target the top element.
* **(1). Push()** - The opposite of popping; inserts element at the top of the stack, the position of the other uninvolved elements are unaffected when pushing. We're only after the top after all.
* **(2). topEl()** - Safely return the top element without doing anything else.
* **(3). Clear()** - Fully clears out the stack. If we once had a full deck of cards, that same deck is now thrown in the trash and burnt.
* **(4). isEmpty()** - Inspects if the stack is empty and devoid of any elements. 

### Stacks and Stack Operations in C++: 

```cpp
#include <iostream>
#include <string>
using namespace std;

// Note that it is very similar to Linked Lists
struct Node {
    string data;
    Node* next;
};

// Of course, a stack starts empty
Node* top = nullptr; // Our Stack Top

// Basic Operations

// Adds a new element at the top of the stack, make sure to establish links to the rest of the stack before anything.
void push(string el) {
    Node* newNode = new Node();
    newNode->data = el;
    newNode->next = top;
    top = newNode;
    cout << "Pushed: " << el << endl;
}

// Redirects pointers to preserve the Stack, and THEN we delete the top
void pop() {
    if (top == nullptr) {
        cout << "Stack Underflow! Nothing to pop." << endl;
        return;
    }
    Node* temp = top;
    string poppedVal = top->data;
    top = top->next;
    delete temp;
    cout << "Popped: " << poppedVal << endl;
}

// If its not empty, return the top's data, if it is? We made it tell us, 
void topEl() {
    if (top != nullptr) {
        cout << "Current Top: " << top->data << endl;
    } else {
        cout << "Stack is empty." << endl; // We've already integrated the isEmpty() earlier, this is just practical IMO
    }
}

// Purges the entire Stack
void Clear() {

    while (top != nullptr) {

        pop(); // Keep popping until the top (and the only element left) is nullptr or empty.
    }
        cout << "Bye bye!" << endl;
        topEl(); // Feedback, should tell us the Stack is empty.

}

int main() {

    push("Ace of Spades");
    push("King of Hearts");
    push("Queen of Diamonds");

    topEl(); // Should be Queen because it is the last

    pop();   // Queen is gone
    topEl(); // Returns King since it is now the top

    pop();   
    pop();   // Purges everyone
    pop();   // Normally, popping nothing results in a Stack Underflow
    push("2 of Diamonds"); // Let's add more stuff
    push("King of Clubs");
    topEl(); // It should be King

    Clear(); // Now no one should be left

    return 0;
}
```
