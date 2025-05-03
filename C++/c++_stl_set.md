
# 🟢 C++ STL : set (중복 없는 정렬된 집합)

---

## 📘 set 이란??

- 중복되지 않는 원소들을 자동 정렬된 상태로 저장하는 컨테이너
- 내부적으로 이진 탐색 트리(Red-Black Tree)를 사용하여 정렬과 탐색을 효율적으로 수행함
- 삽입 시 자동으로 정렬되며, 탐색/삽입/삭제는 평균 O(log n)의 시간 복잡도를 가짐

---

## ✅  예제

```cpp
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> s;

    s.insert(50);
    s.insert(20);
    s.insert(30);
    s.insert(20);  // 중복 삽입 무시됨

    cout << "set 내용: ";
    for (int x : s) {
        cout << x << " ";
    }
    cout << endl;

    s.erase(30);  // 요소 제거

    if (s.find(50) != s.end()) {
        cout << "50은 존재합니다." << endl;
    }

    return 0;
}
```

---

## ✅ 출력 결과

```
set 내용: 20 30 50
50은 존재합니다.

```

---

## ✅ 주요 함수

| 함수 | 설명 |
|------|------|
| `insert(val)` | 값 삽입 (중복 자동 제거) |
| `erase(val)` | 값 삭제 |
| `find(val)` | 해당 값의 iterator 반환 |
| `size()` | 요소 개수 반환 |
| `clear()` | 전체 요소 삭제 |
| `empty()` | 비어 있는지 확인 |

---

## ✅  요약

- 자동 정렬
- 중복 없음
- 빠른 탐색, 삽입, 삭제 (`O(log n)`)
- 정수, 문자열 등 다양한 타입 가능 (`set<int>`, `set<string>` 등)

---
