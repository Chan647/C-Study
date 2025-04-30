#  자료구조: 트리(Tree)


## 📘 트리란?

- 트리는 계층적(hierarchical) 구조를 가진 비선형 자료구조
- 하나의 루트(Root) 노드를 중심으로 여러 자식 노드들이 연결된 구조
- 각 노드는 데이터를 저장하며, 부모-자식 관계를 가짐
- 사이클이 없는 그래프의 일종

## ⏱️ 시간복잡도

- (Search)	O(log n)
- (Insert)	O(log n)
- (Delete)	O(log n)


## 🔧 트리의 용어

루트(Root)    	트리의 시작점이 되는 노드
리프(Leaf)	    자식이 없는 노드
노드(Node)    	데이터를 저장하는 트리의 요소
간선(Edge)	    노드 간 연결선
부모(Parent) 	특정 노드를 연결하는 위쪽 노드
자식(Child) 	특정 노드 아래에 연결된 노드
깊이(Depth) 	루트에서 특정 노드까지의 거리
높이(Height)	노드에서 리프까지 가장 긴 경로의 길이
서브트리	    특정 노드를 루트로 하는 부분 트리

## 📚 트리 종류 

일반 트리               	자식 수 제한 없는 트리
이진 트리(Binary Tree)	    노드당 자식이 최대 2개
완전 이진 트리	            왼쪽부터 차례대로 채워진 이진 트리
포화 이진 트리           	모든 레벨이 꽉 찬 이진 트리
이진 탐색 트리(BST)     	왼쪽 < 루트 < 오른쪽
균형 이진 트리(AVL)	        높이 균형을 맞춘 트리
힙(Heap)	               완전 이진 트리 + 정렬 성질 (최대/최소 힙)
트라이(Trie)	           문자열 저장용 트리
세그먼트 트리,펜윅 트리     구간 합 등 빠른 연산용 특수 트리

## 🌳 기본 구조

struct Node {
    int data;
    Node* left;
    Node* right;
};

- `data`: 노드의 값
- `left`: 왼쪽 자식 노드 포인터
- `right`: 오른쪽 자식 노드 포인터



### 1. 노드 생성

Node* createNode(int value) {
    Node* newNode = new Node();
    newNode->data = value;
    newNode->left = nullptr;
    newNode->right = nullptr;
    return newNode;
}

### 2. 중위 순회 (Inorder Traversal)

void inorderTraversal(Node* node) {
    if (node == nullptr) return;
    inorderTraversal(node->left);
    cout << node->data << " ";
    inorderTraversal(node->right);
}


### 3. 전위 순회 (Preorder Traversal)

void preorderTraversal(Node* node) {
    if (node == nullptr) return;
    cout << node->data << " ";
    preorderTraversal(node->left);
    preorderTraversal(node->right);
}


### 4. 후위 순회 (Postorder Traversal)

void postorderTraversal(Node* node) {
    if (node == nullptr) return;
    postorderTraversal(node->left);
    postorderTraversal(node->right);
    cout << node->data << " ";
}


## 📚 트리 사용 예시

- 파일 시스템 (디렉토리 구조)
- 데이터베이스 인덱스 (B-트리, B+트리)
- 웹의 DOM 구조
- 이진 탐색 트리 (Binary Search Tree)
- 힙 구조 (Heap)
- 의사결정 트리 (AI 알고리즘)
- 압축 알고리즘 (허프만 트리)
