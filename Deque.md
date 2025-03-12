# Deque (Double-Ended Queue)

## Introduction to Deque
A **deque** (double-ended queue) is a linear data structure that allows insertion and deletion of elements from both the front and the rear. It combines the features of a stack and a queue, making it highly versatile.

---

## Basic Operations on Deque
1. **push_front**: Add an element to the front of the deque.
2. **push_back**: Add an element to the rear of the deque.
3. **pop_front**: Remove an element from the front of the deque.
4. **pop_back**: Remove an element from the rear of the deque.
5. **front**: Retrieve the element at the front of the deque without removing it.
6. **back**: Retrieve the element at the rear of the deque without removing it.
7. **isEmpty**: Check if the deque is empty.

---

## Implementation of Deque Using Circular Arrays (C++)
A deque can be implemented using a **circular array** to efficiently utilize space. Here’s how it works:

### Code Example
```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class Deque {
private:
    int arr[MAX_SIZE];
    int start, end, sz;

public:
    Deque() : start(0), end(0), sz(0) {}

    bool isEmpty() {
        return sz == 0;
    }

    bool isFull() {
        return sz == MAX_SIZE;
    }

    void push_front(int value) {
        if (isFull()) {
            cout << "Deque Overflow!" << endl;
            return;
        }

        if (isEmpty()) {
            start = end = 0;
        } else {
            start = (start - 1 + MAX_SIZE) % MAX_SIZE;
        }

        arr[start] = value;
        sz++;
    }

    void push_back(int value) {
        if (isFull()) {
            cout << "Deque Overflow!" << endl;
            return;
        }

        if (isEmpty()) {
            start = end = 0;
        } else {
            end = (end + 1) % MAX_SIZE;
        }

        arr[end] = value;
        sz++;
    }

    int pop_front() {
        if (isEmpty()) {
            cout << "Deque Underflow!" << endl;
            return -1;
        }

        int value = arr[start];
        start = (start + 1) % MAX_SIZE;
        sz--;

        return value;
    }

    int pop_back() {
        if (isEmpty()) {
            cout << "Deque Underflow!" << endl;
            return -1;
        }

        int value = arr[end];
        end = (end - 1 + MAX_SIZE) % MAX_SIZE;
        sz--;

        return value;
    }

    int front() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return -1;
        }
        return arr[start];
    }

    int back() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return -1;
        }
        return arr[end];
    }
};

int main() {
    Deque deque;
    deque.push_back(10);
    deque.push_back(20);
    deque.push_front(5);

    cout << "Front element: " << deque.front() << endl; // Output: 5
    cout << "Back element: " << deque.back() << endl; // Output: 20

    cout << "Popped from front: " << deque.pop_front() << endl; // Output: 5
    cout << "Popped from end: " << deque.pop_back() << endl; // Output: 20

    return 0;
}
```

## Implementation of Deque Using Linked Lists (C++)
A deque can also be implemented using a doubly linked list, which allows efficient insertion and deletion at both ends.

### Code Example
```cpp
#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* prev;
    Node* next;

    Node(int value) {
        data = value;
        prev = next = nullptr;
    }
};

class Deque {
private:
    Node* frontPtr;
    Node* backPtr;

public:
    Deque() {
        frontPtr = backPtr = nullptr;
    }

    bool isEmpty() {
        return (frontPtr == nullptr);
    }

    void push_front(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            frontPtr = backPtr = newNode;
        } else {
            newNode->next = frontPtr;
            frontPtr->prev = newNode;
            frontPtr = newNode;
        }
    }

    void push_back(int value) {
        Node* newNode = new Node(value);
        if (isEmpty()) {
            frontPtr = backPtr = newNode;
        } else {
            newNode->prev = backPtr;
            backPtr->next = newNode;
            backPtr = newNode;
        }
    }

    int pop_front() {
        if (isEmpty()) {
            cout << "Deque Underflow!" << endl;
            return -1;
        }

        int value = frontPtr->data;
        Node* temp = frontPtr;
        frontPtr = frontPtr->next;

        if (frontPtr == nullptr) {
            backPtr = nullptr;
        } else {
            frontPtr->prev = nullptr;
        }

        delete temp;
        return value;
    }

    int pop_back() {
        if (isEmpty()) {
            cout << "Deque Underflow!" << endl;
            return -1;
        }

        int value = backPtr->data;
        Node* temp = backPtr;
        backPtr = backPtr->prev;

        if (backPtr == nullptr) {
            frontPtr = nullptr;
        } else {
            backPtr->next = nullptr;
        }

        delete temp;
        return value;
    }

    int front() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return -1;
        }
        return frontPtr->data;
    }
 
    int back() {
        if (isEmpty()) {
            cout << "Deque is empty!" << endl;
            return -1;
        }
        return backPtr->data;
    }
};

int main() {
    Deque deque;
    deque.push_back(10);
    deque.push_back(20);
    deque.push_front(5);

    cout << "Front element: " << deque.front() << endl; // Output: 5
    cout << "Rear element: " << deque.back() << endl; // Output: 20

    cout << "Popped from front: " << deque.pop_front() << endl; // Output: 5
    cout << "Popped from rear: " << deque.pop_back() << endl; // Output: 20

    return 0;
}
```