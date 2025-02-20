#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

class DoublyLinkedList {
public:
    Node* head;
    Node* tail;

    DoublyLinkedList() {
        head = nullptr;
        tail = nullptr;
    }

    // Menambahkan elemen di tengah list
    void push_mid(int value) {
        cout << "Pushing " << value << " at mid..." << endl;
        Node* newNode = new Node{value, nullptr, nullptr};
        if (!head) {
            head = tail = newNode;
            cout << "List was empty, inserted as first node." << endl;
            return;
        }
        
        Node* slow = head;
        Node* fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        
        newNode->next = slow->next;
        newNode->prev = slow;
        if (slow->next) slow->next->prev = newNode;
        slow->next = newNode;
        if (newNode->next == nullptr) tail = newNode;
        cout << "Inserted " << value << " in the middle." << endl;
    }

    // Menghapus elemen dari depan list
    void delete_front() {
        if (!head) {
            cout << "List is empty, cannot delete front." << endl;
            return;
        }
        cout << "Deleting front node: " << head->data << endl;
        Node* temp = head;
        head = head->next;
        if (head) head->prev = nullptr;
        else tail = nullptr;
        delete temp;
    }

    // Menghapus elemen dari belakang list
    void delete_back() {
        if (!tail) {
            cout << "List is empty, cannot delete back." << endl;
            return;
        }
        cout << "Deleting back node: " << tail->data << endl;
        Node* temp = tail;
        tail = tail->prev;
        if (tail) tail->next = nullptr;
        else head = nullptr;
        delete temp;
    }

    // Menghapus elemen di tengah list berdasarkan nilai
    void delete_mid(int value) {
        if (!head) {
            cout << "List is empty, cannot delete " << value << "." << endl;
            return;
        }
        Node* temp = head;
        while (temp && temp->data != value) {
            temp = temp->next;
        }
        if (!temp) {
            cout << "Value " << value << " not found in the list." << endl;
            return;
        }

        cout << "Deleting node with value: " << value << endl;
        if (temp->prev) temp->prev->next = temp->next;
        if (temp->next) temp->next->prev = temp->prev;
        if (temp == head) head = temp->next;
        if (temp == tail) tail = temp->prev;
        delete temp;
    }

    // Menampilkan elemen dalam list
    void display() {
        cout << "Current List: ";
        Node* temp = head;
        while (temp) {
            cout << temp->data << " <-> ";
            temp = temp->next;
        }
        cout << "NULL" << endl;
    }
};

int main() {
    DoublyLinkedList dll;
    dll.push_mid(10);
    dll.display();
    dll.push_mid(20);
    dll.display();
    dll.push_mid(30);
    dll.display();

    dll.delete_front();
    dll.display();

    dll.delete_back();
    dll.display();

    dll.delete_mid(20);
    dll.display();

    return 0;
}
