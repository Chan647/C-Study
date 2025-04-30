#  자료구조: 연결 리스트 (Linked List)

##  📂 연결리스트(Linked List)란?
- 연결 리스트는 노드(Node)들이 포인터를 통해 연결되어 있는 선형 자료구조 
- 각 노드는 데이터를 저장하는 `data` 필드와 다음 노드를 가리키는 `next` 포인터를 가짐

## ✅ 주요 특징

- 동적 크기	배열과 달리 미리 크기를 정하지 않아도 되고, 필요 시 동적으로 확장 가능
- 빠른 삽입/삭제	중간 또는 앞부분에서도 O(1) 시간에 가능 (단, 위치를 찾는 시간 제외)
- 느린 접근 속도	인덱스로 접근이 불가능하며, 순차 탐색이 필요함 (O(n))
- 포인터 사용	각 노드는 data와 next 포인터로 구성됨

## ✅ 종류

- 단일 연결 리스트 (Singly Linked List)
- 이중 연결 리스트 (Doubly Linked List)
- 원형 연결 리스트 (Circular Linked List)

## ⏱️ 시간 복잡도
|            |                  |
|------------|------------------|
|(Search)	| O(n)	|
|  (Insert)	| O(1) ~ O(n)	|
|  (Delete)	| O(1) ~ O(n)	|
|  (Length) | O(n)|	
|  (Print)	| O(n)|	


## 🔹예시

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

void append(Node*& head, int value) {
    Node* newNode = new Node{value, nullptr};
    if (!head) {
        head = newNode;
        return;
    }
    Node* temp = head;
    while (temp->next)
        temp = temp->next;
    temp->next = newNode;
}

void insertAt(Node*& head, int position, int value) {
    Node* newNode = new Node{value, nullptr};
    if (position == 0) {
        newNode->next = head;
        head = newNode;
        return;
    }
    Node* temp = head;
    for (int i = 0; i < position - 1 && temp; i++) {
        temp = temp->next;
    }
    if (!temp) {
        cout << "Position out of range!" << endl;
        delete newNode;
        return;
    }
    newNode->next = temp->next;
    temp->next = newNode;
}

void printList(Node* head) {
    while (head) {
        cout << head->data << " -> ";
        head = head->next;
    }
    cout << "nullptr" << endl;
}

int main() {
    Node* head = nullptr;
    append(head, 10);
    append(head, 20);
    insertAt(head, 1, 15); // 10 -> 15 -> 20
    printList(head);
    return 0;
}
```

## 💡 사용 예시
- 동적 큐, 스택 구현
- 메모리 효율적 리스트 처리
- 삽입/삭제가 빈번한 데이터 구조