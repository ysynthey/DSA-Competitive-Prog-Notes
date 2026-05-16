# Queues 

Welcome to Mcdonald's, please **fall in line**. You're lucky to even be the second in line. The first person before you gets to place an order, leaves, and now you're the first, then you also place your order, leave, the person behind you is now the first in the 
said line, and so on until there is no one left.

If a Stack follows LIFO (Last-In-First-Out); a Queue is also pretty straightforwarded - following FIFO (First-In-First-Out). It can directly be compared to and is literally like the line at the Mcdonalds cashier example we just came up with earlier.

The first person gets served, they leave, the next person becomes first, and it loops on from there. A Queue focus on the person in front just like a Stack focuses on the top of itself. In Computer Science, its logic and implementation are thankfully nearly identitcal
to how it actually happens in real life.

Compared to a Stack however, we implement a pointer to the front of the line, and even the back. This is like a Singly Linked List but with an added "Rear" pointer to keep Enqueue at $O(1)$ efficiency.

## Queue Operations
* **(0). Enqueue()** - Adds an element to the back of the line, we don't skip lines here.

If you have a Queue that goes like this: "John" -> "Mark" -> "Matthew" where John is the first in line, you will be being John in the Queue.

* **(1). Dequeue()** - Remove the element at the front of the Queue/line, Once you place your order for a Big Mac meal, you leave the line and everyone behind you moves forward.

Suppose Matthew is dequeued after ordering food. Mark is now at the front and everyone, yourself included moves 1 step forward in the Queue.

* **(2). firstEl()** - Return the first element without removing it.

Since Mark is at the front of the line, it returns Mark if we run it after that recent Dequeue()

* **(3). isEmpty()** - Check if the queue is empty.

As of present, there's still people lined up, so it should return false

* **(4). Clear()** - Fully clears out the queue.

Everyone is done with what they're doing and leaves. The Queue ends up empty after calling this.



```
NOTE: We're using a longer and slightly different example in the C++
```

``` cpp
#include <iostream>
#include <string>
using namespace std;

struct Node {
    string data;
    Node* next;
};

Node *front = nullptr, *rear = nullptr;

void enqueue(string el) {
    Node* newNode = new Node();
    newNode->data = el;
    newNode->next = nullptr;
    
    if (rear == nullptr) { // If queue is empty
        front = rear = newNode;
        return;
    }
    
    cout << "Queued in " << rear -> data << endl;
    rear->next = newNode; // Link the old tail to the new element
    rear = newNode;       // Move the tail pointer to the new element
    
    
}

void dequeue() {
    
    // Account for when a Queue is empty to begin with
    if (front == nullptr) {
        cout << "Queue Underflow!" << endl;
        return;
    }
    Node* temp = front;
    // Move front to the element behind it.
    front = front->next;
    
    if (front == nullptr) rear = nullptr; // If list became empty
    
    cout << temp-> data << " dequeued" << endl;
    delete temp;
}

void view() {
    Node* curr = front;
    
    // Account for an empty Queue
    if (curr == nullptr) {
        cout << "Queue empty." << endl;
    }
    
    // Start at the front, then move back and see whos there until theres no one left
    while (curr != nullptr) {
        cout << curr -> data;
        if (curr -> next != nullptr)  cout << " <- ";
        
        // Move to the next in Queue
        curr = curr -> next;
    }
    
    cout << endl;
}

//
void firstEl() { 
    if (front != nullptr) {
        cout << "First element: " << front->data << endl;
    } else {
        cout << "Queue is empty." << endl;
    }
}

void clear() {
    // O(n) as we go thru every element in the queue until there is nothing left
    while (front != nullptr) {
        dequeue();
    }
}

bool isEmpty() {
    return front == nullptr;
}

int main() {
    // Five friends enter a McDonald's
    enqueue("Luke");
    enqueue("Jude");
    enqueue("Matthew");
    enqueue("John");
    enqueue("Mark");
    
    
    // Luke removed from Queue
    dequeue();
    
    // Who is left?
    view();
   
    // Should output Jude
    firstEl();
    
    // Everyone has placed an order and left
    clear();
    
    // No one left
    view();
}

```
