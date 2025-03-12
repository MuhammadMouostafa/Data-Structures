# Linked Lists

## Introduction to Linked Lists
A **linked list** is a linear data structure where each element (called a **node**) contains two parts:
1. **Data**: The value stored in the node.
2. **Pointer**: A reference to the next node in the sequence.

Unlike arrays, linked lists are not stored in contiguous memory locations, making them dynamic and flexible in size.

---

## Types of Linked Lists
1. **Singly Linked List**: Each node points only to the next node.
2. **Doubly Linked List**: Each node points to both the next and the previous node.
3. **Circular Linked List**: The last node points back to the first node, forming a loop.

---

## Basic Operations on Linked Lists
1. **Insertion**: Add a node at the beginning, end, or a specific position.
2. **Deletion**: Remove a node from the beginning, end, or a specific position.
3. **Traversal**: Visit each node in the list.
4. **Searching**: Find a node with a specific value.
5. **Updating**: Change the value of a node.

---

## Implementation of Singly Linked List (C++)
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

class LinkedList {
private:
    Node* head;

public:
    LinkedList() {
        head = nullptr;
    }

    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
    }

    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    void deleteNode(int value) {
        if (head == nullptr) return;

        if (head->data == value) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }

        Node* temp = head;
        while (temp->next != nullptr && temp->next->data != value) {
            temp = temp->next;
        }

        if (temp->next != nullptr) {
            Node* nodeToDelete = temp->next;
            temp->next = temp->next->next;
            delete nodeToDelete;
        }
    }

    void printList() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "nullptr" << endl;
    }
};

int main() {
    LinkedList list;
    list.insertAtEnd(10);
    list.insertAtEnd(20);
    list.insertAtBeginning(5);
    list.printList(); // Output: 5 -> 10 -> 20 -> nullptr

    list.deleteNode(10);
    list.printList(); // Output: 5 -> 20 -> nullptr

    return 0;
}
```
## Implementation of Doubly Linked List (C++)
```cpp
#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;
    Node* prev;

    Node(int value) {
        data = value;
        next = nullptr;
        prev = nullptr;
    }
};

class DoublyLinkedList {
private:
    Node* head;

public:
    DoublyLinkedList() {
        head = nullptr;
    }

    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        if (head != nullptr) {
            head->prev = newNode;
        }
        head = newNode;
    }

    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
        newNode->prev = temp;
    }

    void deleteNode(int value) {
        if (head == nullptr) return;

        if (head->data == value) {
            Node* temp = head;
            head = head->next;
            if (head != nullptr) {
                head->prev = nullptr;
            }
            delete temp;
            return;
        }

        Node* temp = head;
        while (temp != nullptr && temp->data != value) {
            temp = temp->next;
        }

        if (temp != nullptr) {
            if (temp->prev != nullptr) {
                temp->prev->next = temp->next;
            }
            if (temp->next != nullptr) {
                temp->next->prev = temp->prev;
            }
            delete temp;
        }
    }

    void printList() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " <-> ";
            temp = temp->next;
        }
        cout << "nullptr" << endl;
    }
};

int main() {
    DoublyLinkedList list;
    list.insertAtEnd(10);
    list.insertAtEnd(20);
    list.insertAtBeginning(5);
    list.printList(); // Output: 5 <-> 10 <-> 20 <-> nullptr

    list.deleteNode(10);
    list.printList(); // Output: 5 <-> 20 <-> nullptr

    return 0;
}
```

## Applications of Linked Lists
1. **Dynamic Memory Allocation**: Linked lists are used in memory management systems.
2. **Implementation of Stacks and Queues**: Linked lists are used to implement stacks and queues.
3. **Graphs and Trees**: Linked lists are used to represent adjacency lists in graphs and nodes in trees.
4. **Music and Video Playlists**: Linked lists are used to manage playlists where songs or videos can be added or removed dynamically.
5. **Undo/Redo Operations**: Linked lists are used in applications like text editors to implement undo/redo functionality.

## Example: Reversing a Linked List
A common problem solved using linked lists is reversing the list. Here’s how it works:
1. Traverse the list.
2. Change the direction of the pointers.

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

class LinkedList {
private:
    Node* head;

public:
    LinkedList() {
        head = nullptr;
    }

    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    void reverse() {
        Node* prev = nullptr;
        Node* current = head;
        Node* next = nullptr;

        while (current != nullptr) {
            next = current->next;
            current->next = prev;
            prev = current;
            current = next;
        }
        head = prev;
    }

    void printList() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "nullptr" << endl;
    }
};

int main() {
    LinkedList list;
    list.insertAtEnd(10);
    list.insertAtEnd(20);
    list.insertAtEnd(30);
    list.printList(); // Output: 10 -> 20 -> 30 -> nullptr

    list.reverse();
    list.printList(); // Output: 30 -> 20 -> 10 -> nullptr

    return 0;
}
```