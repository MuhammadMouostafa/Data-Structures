# Queues

## Introduction to Queues
A **queue** is a linear data structure that follows the **First-In-First-Out (FIFO)** principle. This means that the first element added to the queue will be the first one to be removed. Think of it like a line of people waiting for a bus: the first person in line is the first to board.

---

## Basic Operations on Queues
1. **Push**: Add an element to the rear of the queue.
2. **Pop**: Remove an element from the front of the queue.
3. **Front**: Retrieve the element at the front of the queue without removing it.
4. **IsEmpty**: Check if the queue is empty.

---

## Implementation of Queue Using Circular Arrays (C++)
A queue can be implemented using a **circular array** to efficiently utilize space. Here’s how it works:

### Code Example
```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class Queue {
private:
    int arr[MAX_SIZE];
    int left, right, sz;

public:
    Queue() : left(0), right(0), sz(0) {}

    bool isEmpty() {
        return sz == 0;
    }

    bool isFull() {
        return sz == MAX_SIZE;
    }

    void push(int value) {
        if (isFull()) {
            cout << "Queue Overflow!" << endl;
            return;
        }

        if (isEmpty()) {
            right = left = 0;
        } else {
            right = (right + 1) % MAX_SIZE;
        }

        arr[right] = value;
        sz++;
    }

    int pop() {
        if (isEmpty()) {
            cout << "Queue is Empty!" << endl;
            return -1;
        }

        int value = front();
        left = (left + 1) % MAX_SIZE;
        sz--;

        return value;
    }

    int front() {
        if (isEmpty()) {
            cout << "Queue is empty!" << endl;
            return -1;
        }
        return arr[left];
    }
};

int main() {
    Queue queue;
    queue.push(10);
    queue.push(20);
    queue.push(30);

    cout << "Front element: " << queue.front() << endl; // Output: 10
    cout << "Dequeued element: " << queue.pop() << endl; // Output: 10
    cout << "Front element after pop: " << queue.front() << endl; // Output: 20

    return 0;
}
```

## Implementation of Queue Using Linked Lists (C++)
A queue can also be implemented using a linked list. This approach is dynamic and avoids the size limitations of arrays.

### Code Example
```cpp
#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};

class Queue {
private:
    Node* frontPtr;
    Node* rearPtr;

public:
    Queue() {
        frontPtr = rearPtr = nullptr;
    }

    bool isEmpty() {
        return (frontPtr == nullptr);
    }

    void push(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            frontPtr = rearPtr = newNode;
        } else {
            rearPtr->next = newNode;
            rearPtr = newNode;
        }
    }

    int pop() {
        if (isEmpty()) {
            cout << "Queue Underflow!" << endl;
            return -1;
        }
        int value = frontPtr->data;
        Node* temp = frontPtr;
        frontPtr = frontPtr->next;
        if (frontPtr == nullptr) {
            rearPtr = nullptr;
        }
        delete temp;
        return value;
    }

    int front() {
        if (isEmpty()) {
            cout << "Queue is empty!" << endl;
            return -1;
        }
        return frontPtr->data;
    }
};

int main() {
    Queue queue;
    queue.push(10);
    queue.push(20);
    queue.push(30);

    cout << "Front element: " << queue.front() << endl; // Output: 10
    cout << "Dequeued element: " << queue.pop() << endl; // Output: 10
    cout << "Front element after pop: " << queue.front() << endl; // Output: 20

    return 0;
}
```