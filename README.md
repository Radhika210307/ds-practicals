# ds-practicals

PRACTICAL 01
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
