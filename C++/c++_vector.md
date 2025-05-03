
# 📌 C++ STL : vector (벡터)


---
## ✅ vector(벡터)란?

- C++ STL에서 가장 많이 쓰이는 동적 배열
- 배열과 유사하지만, 원소 추가/삭제 시 자동으로 크기가 조절됨
- 효율적인 임의 접근(random access)과 push_back() 같은 유연한 삽입 함수를 제공

---

## ✅ 기본 문법 및 예제

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v;             // 빈 벡터 생성
    v.push_back(10);           // 요소 추가
    v.push_back(20);
    v.push_back(30);

    cout << "첫 번째 요소: " << v[0] << endl;
    cout << "총 개수: " << v.size() << endl;

    for (int i = 0; i < v.size(); i++) {
        cout << v[i] << " ";
    }
    cout << endl;

    v.pop_back();            

    for (int x : v) {          
        cout << x << " ";
    }
    cout << endl;

    return 0;
}
```

---

## ✅ 출력 결과

```
첫 번째 요소: 10
총 개수: 3
10 20 30
10 20
```

---

## ✅ 주요 함수

| 함수 | 설명 |
|------|------|
| `push_back(val)` | 마지막에 요소 추가 |
| `pop_back()` | 마지막 요소 제거 |
| `size()` | 요소 개수 반환 |
| `empty()` | 벡터가 비었는지 여부 확인 |
| `v[i]` / `v.at(i)` | 인덱스 접근 (`at()`은 예외 검사 포함) |
| `clear()` | 모든 요소 삭제 |

---

## ✅ 요약

- 인덱스 접근이 빠름 (`O(1)`)
- 마지막에 추가/제거 빠름 (`O(1)`)
- 중간 삽입/삭제는 느림 (`O(n)`)
- 내부적으로 메모리를 자동 관리

---

