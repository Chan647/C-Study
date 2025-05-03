
# 🔗 C++ STL :   list (이중 연결 리스트)


---

## ✅ list(리스트)란? 


- 양방향 연결 리스트(doubly linked list)를 구현한 컨테이너
- 임의 접근은 느리지만, 중간 삽입/삭제가 빠르고 효율적
- push_front(), insert(), remove() 등 연결 리스트에 최적화된 함수들을 제공

---

## ✅  예제

```cpp
#include <iostream>
#include <list>
using namespace std;

int main() {
    list<int> lst;

    lst.push_back(10);
    lst.push_back(20);
    lst.push_front(5);       

    cout << "리스트 순회: ";
    for (int x : lst) {
        cout << x << " ";
    }
    cout << endl;

    lst.pop_back();         
    lst.pop_front();         

    cout << "제거 후: ";
    for (int x : lst) {
        cout << x << " ";
    }
    cout << endl;

    return 0;
}
```

---

## ✅ 출력 결과

```
리스트 순회: 5 10 20
제거 후: 10
```

---

## ✅ 주요 함수

| 함수 | 설명 |
|------|------|
| `push_back(val)` | 뒤에 요소 추가 |
| `push_front(val)` | 앞에 요소 추가 |
| `pop_back()` | 마지막 요소 제거 |
| `pop_front()` | 첫 요소 제거 |
| `insert(it, val)` | 특정 위치에 삽입 (iterator 사용) |
| `erase(it)` | 특정 위치의 요소 제거 |
| `clear()` | 전체 요소 삭제 |
| `size()` | 현재 요소 개수 반환 |
| `empty()` | 비어 있는지 여부 확인 |

---

## ✅ 특징 요약

- 인덱스 접근 불가 (`list[i]` ❌)
- 중간 삽입/삭제 빠름 (`O(1)`)
- 양방향 이동 가능한 이터레이터 지원

---
