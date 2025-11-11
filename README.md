# ds-practicals

PRACTICAL 01

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
