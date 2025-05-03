
# 📥 C++ STL : stack & queue

---

## 📘stack 이란??

- 후입선출(LIFO, Last-In First-Out) 방식의 컨테이너 어댑터
- 내부적으로 deque나 vector 등을 기반으로 하며, 맨 위(top) 원소에 접근할 수 있음
- push(), pop(), top() 함수로 데이터 삽입, 삭제, 조회를 수행함

---

## ✅ stack (스택)

- 구조: **LIFO (Last-In, First-Out)**  
- 사용 예: 함수 호출 스택, 되돌리기, 괄호 검사 등
- 헤더: `<stack>`

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> s;
    s.push(10);
    s.push(20);
    s.push(30);

    while (!s.empty()) {
        cout << s.top() << " ";  
        s.pop();               
    }

    return 0;
}
```

### ✅ 출력 결과

```
30 20 10
```

---

## 📘queue 이란??

- 선입선출(FIFO, First-In First-Out) 방식의 컨테이너 어댑터
- push(), pop(), front(), back() 함수로 양 끝에서 데이터 삽입과 삭제를 수행함
- 내부적으로는 주로 deque를 기반으로 구현되며, 줄 서기 구조의 작업에 적합

---

## ✅ queue (큐)

- 구조: **FIFO (First-In, First-Out)**  
- 사용 예: 대기열, 작업 처리, 프린터 큐 등
- 헤더: `<queue>`

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    queue<int> q;
    q.push(100);
    q.push(200);
    q.push(300);

    while (!q.empty()) {
        cout << q.front() << " ";  
        q.pop();                  
    }

    return 0;
}
```

### ✅ 출력 결과

```
100 200 300
```

---

## ✅ 공통 주요 함수

| 함수 | 설명 |
|------|------|
| `push(val)` | 요소 추가 |
| `pop()` | 요소 제거 |
| `top()` (stack) / `front()` (queue) | 최상단 / 최전방 요소 확인 |
| `size()` | 요소 개수 |
| `empty()` | 비어있는지 확인 |

---
