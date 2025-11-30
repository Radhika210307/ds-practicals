# ds-practicals

**PRACTICAL 01**
WAP  to implement doubly linked list ad an ADT that supports the following operations: 
1 insert an element x at the beginning  .
2 insert an element x at the end .
3 remove an element from the beginning .
4  remove an element from the end.

```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int d) : data(d), next(NULL) {}
};

class SinglyLinkedList {
private:
    Node* head;

public:
    SinglyLinkedList() : head(NULL) {}

    ~SinglyLinkedList() {
        // free all nodes
        while (head != NULL) {
            deleteFromBeginning();
        }
    }

    // Insert at beginning
    void insertAtBeginning(int x) {
        Node* temp = new Node(x);
        temp->next = head;
        head = temp;
    }

    // Insert at i-th position (0-based)
    void insertAtPosition(int x, int pos) {
        Node* temp = new Node(x);

        if (pos == 0) {
            temp->next = head;
            head = temp;
            return;
        }

        Node* curr = head;
        for (int i = 0; i < pos - 1 && curr != NULL; i++) {
            curr = curr->next;
        }

        if (curr == NULL) {
            cout << "Position out of range\n";
            delete temp;
            return;
        }

        temp->next = curr->next;
        curr->next = temp;
    }

    // Delete from beginning
    void deleteFromBeginning() {
        if (head == NULL) {
            cout << "List is empty\n";
            return;
        }
        Node* temp = head;
        head = head->next;
        delete temp;
    }

    // Delete from i-th position (0-based)
    void deleteFromPosition(int pos) {
        if (head == NULL) {
            cout << "List is empty\n";
            return;
        }

        if (pos == 0) {
            Node* temp = head;
            head = head->next;
            delete temp;
            return;
        }

        Node* curr = head;
        for (int i = 0; i < pos - 1 && curr != NULL; i++) {
            curr = curr->next;
        }

        if (curr == NULL || curr->next == NULL) {
            cout << "Position out of range\n";
            return;
        }

        Node* temp = curr->next;
        curr->next = temp->next;
        delete temp;
    }

    // Search for element x; return pointer to node or NULL
    Node* search(int x) {
        Node* curr = head;
        while (curr != NULL) {
            if (curr->data == x) return curr;
            curr = curr->next;
        }
        return NULL;
    }

    // Utility: display list
    void display() {
        Node* curr = head;
        if (curr == NULL) {
            cout << "List: NULL\n";
            return;
        }
        cout << "List: ";
        while (curr != NULL) {
            cout << curr->data;
            if (curr->next != NULL) cout << " -> ";
            curr = curr->next;
        }
        cout << " -> NULL\n";
    }
};

int main() {
    SinglyLinkedList list;
    int choice, x, pos;

    while (true) {
        cout << "\nMenu:\n";
        cout << "1. Insert at beginning\n";
        cout << "2. Insert at position (0-based)\n";
        cout << "3. Delete from beginning\n";
        cout << "4. Delete from position (0-based)\n";
        cout << "5. Search for element\n";
        cout << "6. Display list\n";
        cout << "7. Exit\n";
        cout << "Enter choice: ";
        if (!(cin >> choice)) break;

        switch (choice) {
            case 1:
                cout << "Enter value: ";
                cin >> x;
                list.insertAtBeginning(x);
                break;

            case 2:
                cout << "Enter value: ";
                cin >> x;
                cout << "Enter position (0-based): ";
                cin >> pos;
                list.insertAtPosition(x, pos);
                break;

            case 3:
                list.deleteFromBeginning();
                break;

            case 4:
                cout << "Enter position (0-based): ";
                cin >> pos;
                list.deleteFromPosition(pos);
                break;

            case 5:
                cout << "Enter value to search: ";
                cin >> x;
                if (list.search(x) != NULL)
                    cout << x << " found in list.\n";
                else
                    cout << x << " not found.\n";
                break;

            case 6:
                list.display();
                break;

            case 7:
                cout << "Exiting.\n";
                return 0;

            default:
                cout << "Invalid choice.\n";
        }
    }
    return 0;
}
```





```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

class SinglyList {
    Node* head;

public:
    SinglyList() { head = NULL; }

    // Insert at beginning
    void insertBeg(int x) {
        Node* temp = new Node();
        temp->data = x;
        temp->next = head;
        head = temp;
    }

    // Insert at ith position
    void insertPos(int pos, int x) {
        Node* temp = new Node();
        temp->data = x;

        if (pos == 1) {
            temp->next = head;
            head = temp;
            return;
        }

        Node* curr = head;
        for (int i = 1; i < pos - 1 && curr != NULL; i++)
            curr = curr->next;

        if (curr == NULL) {
            cout << "Invalid Position\n";
            return;
        }

        temp->next = curr->next;
        curr->next = temp;
    }

    // Remove from beginning
    void deleteBeg() {
        if (head == NULL) return;

        Node* temp = head;
        head = head->next;
        delete temp;
    }

    // Remove from ith position
    void deletePos(int pos) {
        if (head == NULL) return;

        if (pos == 1) {
            deleteBeg();
            return;
        }

        Node* curr = head;
        for (int i = 1; i < pos - 1 && curr->next != NULL; i++)
            curr = curr->next;

        if (curr->next == NULL) {
            cout << "Invalid Position\n";
            return;
        }

        Node* temp = curr->next;
        curr->next = temp->next;
        delete temp;
    }

    // Search an element
    void search(int x) {
        Node* curr = head;
        int pos = 1;
        while (curr) {
            if (curr->data == x) {
                cout << "Element found at position " << pos << "\n";
                return;
            }
            curr = curr->next;
            pos++;
        }
        cout << "Element not found\n";
    }

    void display() {
        Node* curr = head;
        while (curr) {
            cout << curr->data << " ";
            curr = curr->next;
        }
        cout << "\n";
    }
};

int main() {
    SinglyList s;
    s.insertBeg(10);
    s.insertPos(2, 20);
    s.insertPos(3, 30);
    s.display();
    s.search(20);
    s.deletePos(2);
    s.display();
}
```




# PRACTICAL 02
> WAP  to implement doubly linked list ad an ADT that supports the following operations: 
1 insert an element x at the beginning  .
2 insert an element x at the end .
3 remove an element from the beginning .
4  remove an element from the end.

```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int d) : data(d), prev(NULL), next(NULL) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(NULL), tail(NULL) {}

    ~DoublyLinkedList() {
        // free all nodes
        Node* cur = head;
        while (cur != NULL) {
            Node* nxt = cur->next;
            delete cur;
            cur = nxt;
        }
    }

    // 1. Insert at beginning
    void insertAtBeginning(int x) {
        Node* temp = new Node(x);   // create node
        temp->next = head;          // new->next = old head
        temp->prev = NULL;          // new is first so prev=NULL

        if (head != NULL) {
            head->prev = temp;      // old head's prev -> new
        } else {
            tail = temp;            // if list was empty, tail also = new
        }
        head = temp;                // update head
    }

    // 2. Insert at end
    void insertAtEnd(int x) {
        Node* temp = new Node(x);   // create node
        temp->next = NULL;          // last node -> next = NULL
        temp->prev = tail;          // prev -> old tail

        if (tail != NULL) {
            tail->next = temp;      // old tail's next -> new
        } else {
            head = temp;            // list was empty => head = new
        }
        tail = temp;                // update tail
    }

    // 3. Remove from beginning
    void deleteFromBeginning() {
        if (head == NULL) {
            cout << "List is empty\n";
            return;
        }
        Node* temp = head;          // node to delete
        head = head->next;          // move head forward

        if (head != NULL) {
            head->prev = NULL;      // new head's prev = NULL
        } else {
            tail = NULL;            // list became empty
        }
        delete temp;                // free old node
    }

    // 4. Remove from end
    void deleteFromEnd() {
        if (tail == NULL) {
            cout << "List is empty\n";
            return;
        }
        Node* temp = tail;          // node to delete
        tail = tail->prev;          // move tail backward

        if (tail != NULL) {
            tail->next = NULL;      // new tail's next = NULL
        } else {
            head = NULL;            // list became empty
        }
        delete temp;                // free old node
    }

    // Utility: display forward
    void displayForward() const {
        Node* cur = head;
        if (!cur) {
            cout << "List: NULL\n";
            return;
        }
        cout << "List (head -> tail): ";
        while (cur) {
            cout << cur->data;
            if (cur->next) cout << " <-> ";
            cur = cur->next;
        }
        cout << " -> NULL\n";
    }

    // Utility: display backward
    void displayBackward() const {
        Node* cur = tail;
        if (!cur) {
            cout << "List (empty)\n";
            return;
        }
        cout << "List (tail -> head): ";
        while (cur) {
            cout << cur->data;
            if (cur->prev) cout << " <-> ";
            cur = cur->prev;
        }
        cout << " -> NULL\n";
    }
};

int main() {
    DoublyLinkedList dll;
    int choice, x;

    while (true) {
        cout << "\nMenu:\n";
        cout << "1. Insert at beginning\n";
        cout << "2. Insert at end\n";
        cout << "3. Delete from beginning\n";
        cout << "4. Delete from end\n";
        cout << "5. Display forward\n";
        cout << "6. Display backward\n";
        cout << "7. Exit\n";
        cout << "Enter choice: ";
        if (!(cin >> choice)) break;

        switch (choice) {
            case 1:
                cout << "Enter value: ";
                cin >> x;
                dll.insertAtBeginning(x);
                break;
            case 2:
                cout << "Enter value: ";
                cin >> x;
                dll.insertAtEnd(x);
                break;
            case 3:
                dll.deleteFromBeginning();
                break;
            case 4:
                dll.deleteFromEnd();
                break;
            case 5:
                dll.displayForward();
                break;
            case 6:
                dll.displayBackward();
                break;
            case 7:
                cout << "Exiting.\n";
                return 0;
            default:
                cout << "Invalid choice.\n";
        }
    }
    return 0;
}

```


```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

class DoublyList {
    Node* head;

public:
    DoublyList() { head = NULL; }

    void insertBeg(int x) {
        Node* temp = new Node();
        temp->data = x;
        temp->prev = NULL;
        temp->next = head;
        if (head != NULL) head->prev = temp;
        head = temp;
    }

    void insertEnd(int x) {
        Node* temp = new Node();
        temp->data = x;
        temp->next = NULL;

        if (head == NULL) {
            temp->prev = NULL;
            head = temp;
            return;
        }

        Node* curr = head;
        while (curr->next)
            curr = curr->next;

        curr->next = temp;
        temp->prev = curr;
    }

    void deleteBeg() {
        if (head == NULL) return;

        Node* temp = head;
        head = head->next;
        if (head != NULL) head->prev = NULL;
        delete temp;
    }

    void deleteEnd() {
        if (head == NULL) return;

        Node* curr = head;
        while (curr->next)
            curr = curr->next;

        if (curr->prev) curr->prev->next = NULL;
        else head = NULL;

        delete curr;
    }

    void display() {
        Node* curr = head;
        while (curr) {
            cout << curr->data << " ";
            curr = curr->next;
        }
        cout << endl;
    }
};

int main() {
    DoublyList d;
    d.insertBeg(10);
    d.insertEnd(20);
    d.insertEnd(30);
    d.display();
    d.deleteBeg();
    d.display();
}

```


**PRACTICAL 03**
Write a program to implement circular linked list as an ADT which supports the following operations: i.Insert an element x in the list ii.Remove an element from the list iii.Search for an element x in the list and return its pointer


```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int d) : data(d), next(NULL) {}
};

class CircularLinkedList {
private:
    Node* head; // pointer to first node (can be NULL)
    Node* tail; // pointer to last node (tail->next == head when non-empty)

public:
    CircularLinkedList() : head(NULL), tail(NULL) {}

    ~CircularLinkedList() {
        if (!head) return;
        // break circularity and delete nodes
        tail->next = NULL;
        Node* cur = head;
        while (cur) {
            Node* nxt = cur->next;
            delete cur;
            cur = nxt;
        }
    }

    // Insert x at the end (after tail). O(1) using tail.
    void insert(int x) {
        Node* temp = new Node(x);
        if (head == NULL) {
            // first node: points to itself
            head = tail = temp;
            temp->next = temp;
        } else {
            temp->next = head;   // new node points to first
            tail->next = temp;   // old last points to new
            tail = temp;         // update tail
        }
    }

    // Remove first occurrence of value x. Prints message if not found.
    void remove(int x) {
        if (head == NULL) {
            cout << "List is empty\n";
            return;
        }

        // Special case: single node
        if (head == tail) {
            if (head->data == x) {
                delete head;
                head = tail = NULL;
                cout << x << " removed (list is now empty)\n";
            } else {
                cout << x << " not found\n";
            }
            return;
        }

        // If head contains x
        if (head->data == x) {
            Node* temp = head;
            head = head->next;
            tail->next = head; // maintain circularity
            delete temp;
            cout << x << " removed\n";
            return;
        }

        // General case: find node prev such that prev->next->data == x
        Node* prev = head;
        Node* cur = head->next;
        while (cur != head && cur->data != x) {
            prev = cur;
            cur = cur->next;
        }

        if (cur == head) {
            // completed full circle, not found
            cout << x << " not found\n";
            return;
        }

        // remove cur
        prev->next = cur->next;
        if (cur == tail) tail = prev; // if we're removing the tail, update it
        delete cur;
        cout << x << " removed\n";
    }

    // Search for x; return pointer to node if found, else NULL
    Node* search(int x) {
        if (head == NULL) return NULL;
        Node* cur = head;
        do {
            if (cur->data == x) return cur;
            cur = cur->next;
        } while (cur != head);
        return NULL;
    }

    // Utility: display list from head once
    void display() const {
        if (head == NULL) {
            cout << "List: NULL\n";
            return;
        }
        cout << "List: ";
        Node* cur = head;
        bool first = true;
        do {
            if (!first) cout << " -> ";
            cout << cur->data;
            first = false;
            cur = cur->next;
        } while (cur != head);
        cout << " -> (back to head)\n";
    }
};

int main() {
    CircularLinkedList cll;
    int choice, x;
    while (true) {
        cout << "\nMenu:\n";
        cout << "1. Insert element\n";
        cout << "2. Remove element (by value)\n";
        cout << "3. Search element\n";
        cout << "4. Display list\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        if (!(cin >> choice)) break;

        switch (choice) {
            case 1:
                cout << "Enter value to insert: ";
                cin >> x;
                cll.insert(x);
                break;
            case 2:
                cout << "Enter value to remove: ";
                cin >> x;
                cll.remove(x);
                break;
            case 3: {
                cout << "Enter value to search: ";
                cin >> x;
                Node* p = cll.search(x);
                if (p) cout << x << " found at node address " << p << "\n";
                else cout << x << " not found\n";
                break;
            }
            case 4:
                cll.display();
                break;
            case 5:
                cout << "Exiting.\n";
                return 0;
            default:
                cout << "Invalid choice.\n";
        }
    }
    return 0;
}

```



```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

class CircularList {
    Node* last;

public:
    CircularList() { last = NULL; }

    void insert(int x) {
        Node* temp = new Node();
        temp->data = x;

        if (last == NULL) {
            temp->next = temp;
            last = temp;
        } else {
            temp->next = last->next;
            last->next = temp;
            last = temp;
        }
    }

    void remove(int x) {
        if (last == NULL) return;

        Node* curr = last->next;
        Node* prev = last;

        do {
            if (curr->data == x) {
                if (curr == last && curr->next == last) {
                    last = NULL;
                } else {
                    prev->next = curr->next;
                    if (curr == last)
                        last = prev;
                }
                delete curr;
                return;
            }
            prev = curr;
            curr = curr->next;
        } while (curr != last->next);
    }

    void search(int x) {
        if (last == NULL) {
            cout << "List Empty\n";
            return;
        }

        Node* curr = last->next;
        int pos = 1;

        do {
            if (curr->data == x) {
                cout << "Element found at position " << pos << endl;
                return;
            }
            curr = curr->next;
            pos++;
        } while (curr != last->next);

        cout << "Element not found\n";
    }

    void display() {
        if (last == NULL) return;

        Node* curr = last->next;
        do {
            cout << curr->data << " ";
            curr = curr->next;
        } while (curr != last->next);
        cout << endl;
    }
};

int main() {
    CircularList c;
    c.insert(10);
    c.insert(20);
    c.insert(30);
    c.display();
    c.search(20);
    c.remove(20);
    c.display();
}

```



**PRACTICAL 04**
Implement Stack as an ADT and use it to evaluate a prefix/postfix expression.


```c++
#include <iostream>
#include <cstring>
#include <cctype>
using namespace std;

// ---------------- STACK ADT ----------------
class Stack {
    int arr[100];
    int top;

public:
    Stack() { top = -1; }

    bool isEmpty() { return top == -1; }
    bool isFull()  { return top == 99; }

    void push(int x) {
        if (isFull()) {
            cout << "Stack Overflow\n";
            return;
        }
        arr[++top] = x;
    }

    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow\n";
            return -1;
        }
        return arr[top--];
    }
};

// --------------- POSTFIX EVALUATION -------------------
int evaluatePostfix(string exp) {
    Stack s;

    for (int i = 0; i < exp.length(); i++) {
        char ch = exp[i];

        // Skip spaces
        if (ch == ' ') continue;

        if (isdigit(ch)) {
            s.push(ch - '0');
        }
        else {
            int b = s.pop();
            int a = s.pop();

            switch (ch) {
                case '+': s.push(a + b); break;
                case '-': s.push(a - b); break;
                case '*': s.push(a * b); break;
                case '/': s.push(a / b); break;
            }
        }
    }
    return s.pop();
}

// ---------------- PREFIX EVALUATION --------------------
int evaluatePrefix(string exp) {
    Stack s;

    // Scan from right to left
    for (int i = exp.length() - 1; i >= 0; i--) {
        char ch = exp[i];

        if (ch == ' ') continue;

        if (isdigit(ch)) {
            s.push(ch - '0');
        }
        else {
            int a = s.pop();
            int b = s.pop();

            switch (ch) {
                case '+': s.push(a + b); break;
                case '-': s.push(a - b); break;
                case '*': s.push(a * b); break;
                case '/': s.push(a / b); break;
            }
        }
    }
    return s.pop();
}

// ---------------- MAIN ---------------------
int main() {
    string postfix = "53+82-*";   // Example
    string prefix  = "- * + 5 3 8 2";

    cout << "Postfix Expression: " << postfix << endl;
    cout << "Postfix Evaluation Result: " << evaluatePostfix(postfix) << endl;

    cout << "Prefix Expression: " << prefix << endl;
    cout << "Prefix Evaluation Result: " << evaluatePrefix(prefix) << endl;

    return 0;
}

```

```c++
#include <iostream>
#include <stack>
#include <string>
using namespace std;

int evaluatePostfix(string exp) {
    stack<int> s;
    for (char ch : exp) {
        if (isdigit(ch)) s.push(ch - '0');
        else {
            int b = s.top(); s.pop();
            int a = s.top(); s.pop();
            switch (ch) {
                case '+': s.push(a + b); break;
                case '-': s.push(a - b); break;
                case '*': s.push(a * b); break;
                case '/': s.push(a / b); break;
            }
        }
    }
    return s.top();
}

int main() {
    string exp = "52+3*";
    cout << "Postfix result: " << evaluatePostfix(exp);
}

```

**implement by linked list**
```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int d) : data(d), next(NULL) {}
};

class Stack {
private:
    Node* top;   // top pointer

public:
    Stack() : top(NULL) {}

    ~Stack() {
        while (!isEmpty()) pop();
    }

    bool isEmpty() {
        return top == NULL;
    }

    // PUSH operation
    void push(int x) {
        Node* temp = new Node(x);
        temp->next = top;   // new node points to old top
        top = temp;         // update top to new node
        cout << x << " pushed onto stack.\n";
```



**PRACTICAL 05**
Implement Queue as an ADT.

```c++
class ArrayQueue {
private:
    int arr[100];
    int front;
    int rear;
    int size;

public:
    ArrayQueue() {
        front = 0;
        rear = -1;
        size = 0;
    }

    bool isEmpty() {
        return size == 0;
    }

    bool isFull() {
        return size == 100;
    }

    void enqueue(int x) {
        if (isFull()) {
            cout << "Queue Overflow\n";
            return;
        }
        rear = (rear + 1) % 100;   // circular increment
        arr[rear] = x;
        size++;
    }

    int dequeue() {
        if (isEmpty()) {
            cout << "Queue Underflow\n";
            return -1;
        }
        int value = arr[front];
        front = (front + 1) % 100; // circular increment
        size--;
        return value;
    }

    int peek() {
        if (isEmpty()) {
            cout << "Queue Empty\n";
            return -1;
        }
        return arr[front];
    }
};

```

```c++
#include <iostream>
using namespace std;

class Queue {
    int arr[50], front, rear;

public:
    Queue() { front = rear = -1; }

    void enqueue(int x) {
        if (rear == 49) {
            cout << "Queue Full\n";
            return;
        }
        if (front == -1) front = 0;
        arr[++rear] = x;
    }

    void dequeue() {
        if (front == -1 || front > rear) {
            cout << "Queue Empty\n";
            return;
        }
        front++;
    }

    void display() {
        for (int i = front; i <= rear; i++)
            cout << arr[i] << " ";
        cout << endl;
    }
};

int main() {
    Queue q;
    q.enqueue(10);
    q.enqueue(20);
    q.display();
    q.dequeue();
    q.display();
}

```


**PRACTICAL 06**
Write a program to implement Binary Search Tree as an ADT which supports the following operations: i.Insert an element x ii.Delete an element x iii.Search for an element x in the BST iv.Display the elements of the BST in preorder, inorder, and postorder traversal


```c++
#include <iostream>
using namespace std;

struct Node {
    int key;
    Node* left;
    Node* right;
    Node(int k) : key(k), left(nullptr), right(nullptr) {}
};

class BST {
private:
    Node* root;

    // recursive helper to insert a key
    Node* insertRec(Node* node, int key) {
        if (node == nullptr) return new Node(key);
        if (key < node->key)
            node->left = insertRec(node->left, key);
        else if (key > node->key)
            node->right = insertRec(node->right, key);
        // if key == node->key, we ignore duplicates (no-op)
        return node;
    }

    // recursive helper to search key
    Node* searchRec(Node* node, int key) const {
        if (node == nullptr || node->key == key) return node;
        if (key < node->key) return searchRec(node->left, key);
        return searchRec(node->right, key);
    }

    // find minimum node in subtree
    Node* minValueNode(Node* node) {
        Node* cur = node;
        while (cur && cur->left != nullptr) cur = cur->left;
        return cur;
    }

    // recursive helper to delete a key
    Node* deleteRec(Node* node, int key) {
        if (node == nullptr) return node;

        if (key < node->key) {
            node->left = deleteRec(node->left, key);
        } else if (key > node->key) {
            node->right = deleteRec(node->right, key);
        } else {
            // node with the key found — handle 3 cases

            // Case 1: no child (leaf)
            if (node->left == nullptr && node->right == nullptr) {
                delete node;
                return nullptr;
            }
            // Case 2: one child
            else if (node->left == nullptr) {
                Node* temp = node->right;
                delete node;
                return temp;
            } else if (node->right == nullptr) {
                Node* temp = node->left;
                delete node;
                return temp;
            }
            // Case 3: two children
            else {
                // get inorder successor (smallest in right subtree)
                Node* succ = minValueNode(node->right);
                node->key = succ->key;                      // copy successor's value
                node->right = deleteRec(node->right, succ->key); // delete successor
            }
        }
        return node;
    }

    // traversal helpers
    void inorderRec(Node* node) const {
        if (!node) return;
        inorderRec(node->left);
        cout << node->key << " ";
        inorderRec(node->right);
    }
    void preorderRec(Node* node) const {
        if (!node) return;
        cout << node->key << " ";
        preorderRec(node->left);
        preorderRec(node->right);
    }
    void postorderRec(Node* node) const {
        if (!node) return;
        postorderRec(node->left);
        postorderRec(node->right);
        cout << node->key << " ";
    }

    // free tree nodes
    void freeRec(Node* node) {
        if (!node) return;
        freeRec(node->left);
        freeRec(node->right);
        delete node;
    }

public:
    BST() : root(nullptr) {}
    ~BST() { freeRec(root); }

    void insert(int key) { root = insertRec(root, key); }

    void deleteNode(int key) { root = deleteRec(root, key); }

    // returns pointer to node if found, else nullptr
    Node* search(int key) const { return searchRec(root, key); }

    void inorder() const {
        if (!root) { cout << "Tree is empty\n"; return; }
        inorderRec(root);
        cout << "\n";
    }
    void preorder() const {
        if (!root) { cout << "Tree is empty\n"; return; }
        preorderRec(root);
        cout << "\n";
    }
    void postorder() const {
        if (!root) { cout << "Tree is empty\n"; return; }
        postorderRec(root);
        cout << "\n";
    }
};

// ---------------------------
// Interactive demo
// ---------------------------
int main() {
    BST tree;
    int choice, x;

    while (true) {
        cout << "\nMenu:\n";
        cout << "1. Insert element\n";
        cout << "2. Delete element\n";
        cout << "3. Search element\n";
        cout << "4. Inorder traversal\n";
        cout << "5. Preorder traversal\n";
        cout << "6. Postorder traversal\n";
        cout << "7. Exit\n";
        cout << "Enter choice: ";
        if (!(cin >> choice)) break;

        switch (choice) {
            case 1:
                cout << "Enter key to insert: ";
                cin >> x;
                tree.insert(x);
                break;
            case 2:
                cout << "Enter key to delete: ";
                cin >> x;
                tree.deleteNode(x);
                break;
            case 3: {
                cout << "Enter key to search: ";
                cin >> x;
                Node* p = tree.search(x);
                if (p) cout << x << " found (node address: " << p << ")\n";
                else cout << x << " not found\n";
                break;
            }
            case 4:
                cout << "Inorder: "; tree.inorder(); break;
            case 5:
                cout << "Preorder: "; tree.preorder(); break;
            case 6:
                cout << "Postorder: "; tree.postorder(); break;
            case 7:
                cout << "Exiting.\n"; return 0;
            default:
                cout << "Invalid choice.\n";
        }
    }
    return 0;
}

```


```c++
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Insert in BST
Node* insert(Node* root, int data) {
    if (root == NULL) return createNode(data);

    if (data < root->data)
        root->left = insert(root->left, data);
    else
        root->right = insert(root->right, data);

    return root;
}

// Search
bool search(Node* root, int key) {
    if (root == NULL) return false;
    if (root->data == key) return true;
    if (key < root->data) return search(root->left, key);
    return search(root->right, key);
}

// Find minimum (helper)
Node* minValueNode(Node* node) {
    while (node->left != NULL)
        node = node->left;
    return node;
}

// Delete node
Node* deleteNode(Node* root, int key) {
    if (root == NULL) return root;

    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == NULL) {
            Node* temp = root->right;
            delete root;
            return temp;
        }
        else if (root->right == NULL) {
            Node* temp = root->left;
            delete root;
            return temp;
        }

        Node* temp = minValueNode(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}

// Traversals
void inorder(Node* root) {
    if (root) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

void preorder(Node* root) {
    if (root) {
        cout << root->data << " ";
        preorder(root->left);
        preorder(root->right);
    }
}

void postorder(Node* root) {
    if (root) {
        postorder(root->left);
        postorder(root->right);
        cout << root->data << " ";
    }
}

int main() {
    Node* root = NULL;

    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 10);

    cout << "Inorder: "; inorder(root); cout << endl;
    cout << "Preorder: "; preorder(root); cout << endl;
    cout << "Postorder: "; postorder(root); cout << endl;

    cout << "Searching 20: " << (search(root, 20) ? "Found" : "Not Found") << endl;

    root = deleteNode(root, 20);
    cout << "After Deletion Inorder: ";
    inorder(root);
}

```



**PRACTICAL 07**
Write a program to implement insert and search operation in AVL trees.

```c++
#include <iostream>
using namespace std;

struct Node {
    int key;
    Node* left;
    Node* right;
    int height;
    Node(int k) : key(k), left(nullptr), right(nullptr), height(1) {}
};

class AVL {
private:
    Node* root;

    // utility: node height (null -> 0)
    int height(Node* n) {
        return n ? n->height : 0;
    }

    // utility: balance factor = height(left) - height(right)
    int getBalance(Node* n) {
        return n ? height(n->left) - height(n->right) : 0;
    }

    // right rotate subtree rooted with y
    Node* rightRotate(Node* y) {
        Node* x = y->left;
        Node* T2 = x->right;

        // rotation
        x->right = y;
        y->left = T2;

        // update heights
        y->height = 1 + max(height(y->left), height(y->right));
        x->height = 1 + max(height(x->left), height(x->right));

        return x; // new root
    }

    // left rotate subtree rooted with x
    Node* leftRotate(Node* x) {
        Node* y = x->right;
        Node* T2 = y->left;

        // rotation
        y->left = x;
        x->right = T2;

        // update heights
        x->height = 1 + max(height(x->left), height(x->right));
        y->height = 1 + max(height(y->left), height(y->right));

        return y; // new root
    }

    // recursive insert helper
    Node* insertRec(Node* node, int key) {
        // 1. normal BST insertion
        if (node == nullptr)
            return new Node(key);

        if (key < node->key)
            node->left = insertRec(node->left, key);
        else if (key > node->key)
            node->right = insertRec(node->right, key);
        else
            return node; // duplicates ignored

        // 2. update height of this ancestor node
        node->height = 1 + max(height(node->left), height(node->right));

        // 3. get balance factor to check whether node became unbalanced
        int balance = getBalance(node);

        // 4. If unbalanced, there are 4 cases

        // Case LL: left-left (rotate right)
        if (balance > 1 && key < node->left->key)
            return rightRotate(node);

        // Case RR: right-right (rotate left)
        if (balance < -1 && key > node->right->key)
            return leftRotate(node);

        // Case LR: left-right -> first left rotate left child, then right rotate node
        if (balance > 1 && key > node->left->key) {
            node->left = leftRotate(node->left);
            return rightRotate(node);
        }

        // Case RL: right-left -> first right rotate right child, then left rotate node
        if (balance < -1 && key < node->right->key) {
            node->right = rightRotate(node->right);
            return leftRotate(node);
        }

        // return unchanged node pointer
        return node;
    }

    // recursive search helper
    Node* searchRec(Node* node, int key) const {
        if (node == nullptr || node->key == key) return node;
        if (key < node->key) return searchRec(node->left, key);
        return searchRec(node->right, key);
    }

    // inorder display (useful for testing — will be sorted)
    void inorderRec(Node* node) const {
        if (!node) return;
        inorderRec(node->left);
        cout << node->key << " ";
        inorderRec(node->right);
    }

    // free nodes
    void freeRec(Node* node) {
        if (!node) return;
        freeRec(node->left);
        freeRec(node->right);
        delete node;
    }

public:
    AVL() : root(nullptr) {}
    ~AVL() { freeRec(root); }

    // Public insert
    void insert(int key) {
        root = insertRec(root, key);
    }

    // Public search: returns pointer or nullptr
    Node* search(int key) const {
        return searchRec(root, key);
    }

    // Utility: print inorder (sorted order)
    void inorder() const {
        if (!root) { cout << "Tree empty\n"; return; }
        inorderRec(root);
        cout << "\n";
    }
};

// ----------------------
// Demo / usage
// ----------------------
int main() {
    AVL tree;
    int choice, x;

    cout << "AVL Demo\n";
    while (true) {
        cout << "\nMenu:\n";
        cout << "1. Insert\n";
        cout << "2. Search\n";
        cout << "3. Inorder display\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        if (!(cin >> choice)) break;

        switch (choice) {
            case 1:
                cout << "Enter key to insert: ";
                cin >> x;
                tree.insert(x);
                cout << x << " inserted.\n";
                break;
            case 2:
                cout << "Enter key to search: ";
                cin >> x;
                if (tree.search(x))
                    cout << x << " found in tree.\n";
                else
                    cout << x << " NOT found.\n";
                break;
            case 3:
                cout << "Inorder: ";
                tree.inorder();
                break;
            case 4:
                cout << "Exiting.\n";
                return 0;
            default:
                cout << "Invalid choice.\n";
        }
    }
    return 0;
}

```



```c++
#include <iostream>
using namespace std;

struct Node {
    int data, height;
    Node* left;
    Node* right;
};

int height(Node* n) {
    return n ? n->height : 0;
}

int getBalance(Node* n) {
    return n ? height(n->left) - height(n->right) : 0;
}

Node* newNode(int key) {
    Node* node = new Node();
    node->data = key;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

Node* rightRotate(Node* y) {
    Node* x = y->left;
    Node* T2 = x->right;

    x->right = y;
    y->left = T2;

    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

Node* leftRotate(Node* x) {
    Node* y = x->right;
    Node* T2 = y->left;

    y->left = x;
    x->right = T2;

    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

Node* insert(Node* node, int key) {
    if (node == NULL)
        return newNode(key);

    if (key < node->data)
        node->left = insert(node->left, key);
    else if (key > node->data)
        node->right = insert(node->right, key);
    else
        return node;

    node->height = 1 + max(height(node->left), height(node->right));

    int balance = getBalance(node);

    if (balance > 1 && key < node->left->data)
        return rightRotate(node);

    if (balance < -1 && key > node->right->data)
        return leftRotate(node);

    if (balance > 1 && key > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    if (balance < -1 && key < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
}

bool search(Node* root, int key) {
    if (!root) return false;
    if (root->data == key) return true;
    if (key < root->data) return search(root->left, key);
    return search(root->right, key);
}

void inorder(Node* root) {
    if (root) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

int main() {
    Node* root = NULL;

    root = insert(root, 30);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 10);

    cout << "Inorder: ";
    inorder(root);
    cout << endl;

    cout << "Search 20: " << (search(root, 20) ? "Found" : "Not Found");
}

```


