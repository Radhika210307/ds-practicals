# ds-practicals

PRACTICAL 01
WAP  to implement doubly linked list ad an ADT that supports the following operations: 
1 insert an element x at the beginning  .
2 insert an element x at the end .
3 remove an element from the beginning .
4  remove an element from the end.


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

