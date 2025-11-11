# ds-practicals

PRACTICAL 01
WAP  to implement doubly linked list ad an ADT that supports the following operations: 
1 insert an element x at the beginning  .
2 insert an element x at the end .
3 remove an element from the beginning .
4  remove an element from the end.

#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int val) {
        data = val;
        next = nullptr;
    }
};

class SinglyLinkedList {
private:
    Node* head;

public:
    SinglyLinkedList() {
        head = nullptr;
    }

    // 1. Insert element at beginning
    void insertAtBeginning(int x) {
        Node* newNode = new Node(x);
        newNode->next = head;
        head = newNode;
    }

    // 2. Insert element at ith position (0-based index)
    void insertAtPosition(int x, int pos) {
        if (pos < 0) {
            cout << "Invalid position!" << endl;
            return;
        }

        Node* newNode = new Node(x);

        if (pos == 0) {
            newNode->next = head;
            head = newNode;
            return;
        }

        Node* current = head;
        for (int i = 0; i < pos - 1 && current != nullptr; i++) {
            current = current->next;
        }

        if (current == nullptr) {
            cout << "Position out of range!" << endl;
            delete newNode;
            return;
        }

        newNode->next = current->next;
        current->next = newNode;
    }

    // 3. Remove element from beginning
    void removeFromBeginning() {
        if (head == nullptr) {
            cout << "List is empty!" << endl;
            return;
        }

        Node* temp = head;
        head = head->next;
        cout << "Removed element: " << temp->data << endl;
        delete temp;
    }

    // 4. Remove element from ith position
    void removeFromPosition(int pos) {
        if (head == nullptr) {
            cout << "List is empty!" << endl;
            return;
        }

        if (pos < 0) {
            cout << "Invalid position!" << endl;
            return;
        }

        if (pos == 0) {
            Node* temp = head;
            head = head->next;
            cout << "Removed element: " << temp->data << endl;
            delete temp;
            return;
        }

        Node* current = head;
        for (int i = 0; i < pos - 1 && current->next != nullptr; i++) {
            current = current->next;
        }

        if (current->next == nullptr) {
            cout << "Position out of range!" << endl;
            return;
        }

        Node* temp = current->next;
        current->next = temp->next;
        cout << "Removed element: " << temp->data << endl;
        delete temp;
    }

    // 5. Search for an element and return its pointer
    Node* search(int x) {
        Node* current = head;
        int position = 0;
        while (current != nullptr) {
            if (current->data == x) {
                cout << "Element " << x << " found at position " << position
                     << " (address: " << current << ")" << endl;
                return current;
            }
            current = current->next;
            position++;
        }
        cout << "Element " << x << " not found in the list." << endl;
        return nullptr;
    }

    // Display the list
    void display() {
        if (head == nullptr) {
            cout << "List is empty." << endl;
            return;
        }
        Node* current = head;
        cout << "Linked List: ";
        while (current != nullptr) {
            cout << current->data << " -> ";
            current = current->next;
        }
        cout << "NULL" << endl;
    }
};

// ---------------------------
// Example Usage
// ---------------------------
int main() {
    SinglyLinkedList list;

    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtPosition(30, 1);
    list.display();

    list.removeFromBeginning();
    list.display();

    list.removeFromPosition(1);
    list.display();

    list.search(10);
    list.search(99);

    return 0;
}


PRACTICAL 02
WAP  to implement doubly linked list ad an ADT that supports the following operations: 
1 insert an element x at the beginning  .
2 insert an element x at the end .
3 remove an element from the beginning .
4  remove an element from the end.


#include <stdio.h>
#include <stdlib.h>

// Structure for a node in the doubly linked list
typedef struct Node {
    int data;
    struct Node* prev;
    struct Node* next;
} Node;

// Head and tail pointers (global for simplicity)
Node* head = NULL;
Node* tail = NULL;

// Function to create a new node
Node* createNode(int x) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = x;
    newNode->prev = NULL;
    newNode->next = NULL;
    return newNode;
}

// 1. Insert an element at the beginning
void insertAtBeginning(int x) {
    Node* newNode = createNode(x);
    if (head == NULL) {
        head = tail = newNode;
    } else {
        newNode->next = head;
        head->prev = newNode;
        head = newNode;
    }
    printf("%d inserted at beginning.\n", x);
}

// 2. Insert an element at the end
void insertAtEnd(int x) {
    Node* newNode = createNode(x);
    if (tail == NULL) {
        head = tail = newNode;
    } else {
        tail->next = newNode;
        newNode->prev = tail;
        tail = newNode;
    }
    printf("%d inserted at end.\n", x);
}

// 3. Remove an element from the beginning
void removeFromBeginning() {
    if (head == NULL) {
        printf("List is empty. Cannot remove.\n");
        return;
    }
    Node* temp = head;
    printf("Removed %d from beginning.\n", temp->data);
    head = head->next;
    if (head != NULL)
        head->prev = NULL;
    else
        tail = NULL;
    free(temp);
}

// 4. Remove an element from the end
void removeFromEnd() {
    if (tail == NULL) {
        printf("List is empty. Cannot remove.\n");
        return;
    }
    Node* temp = tail;
    printf("Removed %d from end.\n", temp->data);
    tail = tail->prev;
    if (tail != NULL)
        tail->next = NULL;
    else
        head = NULL;
    free(temp);
}

// Function to display the list
void display() {
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }
    Node* temp = head;
    printf("List: ");
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

// Main function to test the ADT
int main() {
    int choice, x;
    while (1) {
        printf("\n--- Doubly Linked List Operations ---\n");
        printf("1. Insert at Beginning\n");
        printf("2. Insert at End\n");
        printf("3. Remove from Beginning\n");
        printf("4. Remove from End\n");
        printf("5. Display\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
        case 1:
            printf("Enter element: ");
            scanf("%d", &x);
            insertAtBeginning(x);
            break;
        case 2:
            printf("Enter element: ");
            scanf("%d", &x);
            insertAtEnd(x);
            break;
        case 3:
            removeFromBeginning();
            break;
        case 4:
            removeFromEnd();
            break;
        case 5:
            display();
            break;
        case 6:
            printf("Exiting...\n");
            exit(0);
        default:
            printf("Invalid choice.\n");
        }
    }
    return 0;
}

