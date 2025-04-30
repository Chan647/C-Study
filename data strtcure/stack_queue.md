## 자료구조 : 스택과 큐 (Stack & Queue) 


### 📚 Stack (스택)이란? 

- 스택(Stack) 은 후입선출 (LIFO: Last-In, First-Out) 구조의 자료구조
- 마지막에 넣은 데이터가 가장 먼저 나오는 구조

## ✅ 주요 특징

- 한쪽(top)에서만 삽입/삭제가 일어남
- 함수 호출, 웹 브라우저 뒤로가기, 되돌리기(Undo) 등에 사용

## 🔧 주요 메서드

| `push()` | 스택에 삽입 |
| `pop()` | 스택의 top 요소를 제거 |
| `top()` | 스택의 최상단 요소 반환 |
| `empty()` | 스택이 비어있는지 여부 확인 |
| `size()` | 스택에 있는 요소 개수 반환 |

## ⏱️ 시간복잡도

-  (push)	       O(1)
-  (pop)    	   O(1)
-  (top / peek)    O(1)
-  (size)	       O(1)
-  (empty)	       O(1)

## 📎 예시

#include <stack>
#include <iostream>
using namespace std;

int main() {
    stack<int> s;
    s.push(10);
    s.push(20);
    cout << s.top() << endl;
    s.pop();
    cout << s.top() << endl;
    return 0;
}


### 📚 Queue (큐)란?

- 큐(Queue)는 선입선출 (FIFO: First-In, First-Out) 구조의 자료구조 
- 먼저 들어간 데이터가 가장 먼저 나오는 구조

#### ✅ 주요 특징
- 앞(front)에서 꺼내고, 뒤(back)에서 삽입
- 은행 대기열, 프린터 출력 순서, BFS 알고리즘 등에 사용

#### 🔧 주요 메서드

| `push()` | 큐의 뒤쪽에 삽입 |
| `pop()` | 큐의 앞(front) 요소 제거 |
| `front()` | 큐의 맨 앞 요소 반환 |
| `back()` | 큐의 맨 뒤 요소 반환 |
| `empty()` | 큐가 비어있는지 여부 확인 |
| `size()` | 큐에 있는 요소 개수 반환 |

## ⏱️ 시간 복잡도

-  (enqueue / push)	O(1)
-  (dequeue / pop)	O(1)
-  (front / peek)	O(1)
-  (size)	        O(1)
-  (empty)	        O(1)

#### 📎 예시 

#include <queue>
#include <iostream>
using namespace std;

int main() {
    queue<int> q;
    q.push(10);
    q.push(20);
    cout << q.front() << endl; // 10
    q.pop();
    cout << q.front() << endl; // 20
    return 0;
}

