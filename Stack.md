# Stacks

## Introduction to Stacks
A **stack** is a linear data structure that follows the **Last-In-First-Out (LIFO)** principle. This means that the last element added to the stack will be the first one to be removed. Think of it like a stack of plates: you can only add or remove plates from the top.

---

## Basic Operations on Stacks
1. **Push**: Add an element to the top of the stack.
2. **Pop**: Remove the element from the top of the stack.
3. **Peek (or Top)**: Retrieve the element at the top of the stack without removing it.
4. **IsEmpty**: Check if the stack is empty.
5. **IsFull**: Check if the stack is full (only applicable in fixed-size stacks).

---

## Implementation of Stacks
Stacks can be implemented using:
1. **Arrays**: A fixed-size array where the top of the stack is tracked using an index.
2. **Linked Lists**: A dynamic implementation where each node points to the next element.

### Stack Implementation Using Arrays (C++)
```cpp
#include <iostream>
using namespace std;

#define MAX_SIZE 100

class Stack {
private:
    int arr[MAX_SIZE];
    int topIndex;

public:
    Stack() {
        topIndex = -1;
    }

    void push(int value) {
        if (topIndex >= MAX_SIZE - 1) {
            cout << "Stack Overflow!" << endl;
            return;
        }
        arr[++topIndex] = value;
    }

    int pop() {
        if (topIndex < 0) {
            cout << "Stack Underflow!" << endl;
            return -1;
        }
        return arr[topIndex--];
    }

    int top() {
        if (topIndex < 0) {
            cout << "Stack is empty!" << endl;
            return -1;
        }
        return arr[topIndex];
    }

    bool isEmpty() {
        return (topIndex < 0);
    }
};

int main() {
    Stack stack;
    stack.push(10);
    stack.push(20);
    stack.push(30);

    cout << "Top element: " << stack.top() << endl; // Output: 30
    cout << "Popped element: " << stack.pop() << endl; // Output: 30
    cout << "Top element after pop: " << stack.top() << endl; // Output: 20

    return 0;
}
```

### Stack Implementation Using Linked Lists (C++)
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

class Stack {
private:
    Node* topNode;

public:
    Stack() {
        topNode = nullptr;
    }

    void push(int value) {
        Node* newNode = new Node(value);
        newNode->next = topNode;
        topNode = newNode;
    }

    int pop() {
        if (topNode == nullptr) {
            cout << "Stack Underflow!" << endl;
            return -1;
        }
        int value = topNode->data;
        Node* temp = topNode;
        topNode = topNode->next;
        delete temp;
        return value;
    }

    int top() {
        if (topNode == nullptr) {
            cout << "Stack is empty!" << endl;
            return -1;
        }
        return topNode->data;
    }

    bool isEmpty() {
        return (topNode == nullptr);
    }
};

int main() {
    Stack stack;
    stack.push(10);
    stack.push(20);
    stack.push(30);

    cout << "Top element: " << stack.top() << endl; // Output: 30
    cout << "Popped element: " << stack.pop() << endl; // Output: 30
    cout << "Top element after pop: " << stack.top() << endl; // Output: 20

    return 0;
}
```

## Applications of Stacks
1. **Function Call Management**: Stacks are used to manage function calls and recursion in programming languages.
2. **Expression Evaluation**: Stacks are used to evaluate expressions (e.g., infix to postfix conversion).
3. **Undo/Redo Operations**: Stacks are used in text editors to implement undo/redo functionality.
4. **Balanced Parentheses**: Stacks are used to check if parentheses in an expression are balanced.

---

## Example: Balanced Parentheses
A common problem solved using stacks is checking if a given string of parentheses is balanced. Here’s how it works:
1. Traverse the string.
2. Push opening parentheses onto the stack.
3. Pop from the stack when a closing parenthesis is encountered.
4. If the stack is empty at the end, the parentheses are balanced.

```cpp
#include <iostream>
#include <stack>
using namespace std;

bool isBalanced(string expr) {
    stack<char> s;
    for (char ch : expr) {
        if (ch == '(' || ch == '{' || ch == '[') {
            s.push(ch);
        } else if (ch == ')' || ch == '}' || ch == ']') {
            if (s.empty()) return false;
            char top = s.top();
            s.pop();
            if ((ch == ')' && top != '(') || 
                (ch == '}' && top != '{') || 
                (ch == ']' && top != '[')) {
                return false;
            }
        }
    }
    return s.empty();
}

int main() {
    string expr = "{([()])}";
    if (isBalanced(expr)) {
        cout << "Balanced" << endl;
    } else {
        cout << "Not Balanced" << endl;
    }
    return 0;
}