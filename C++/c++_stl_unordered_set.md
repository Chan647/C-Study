
# 🔶 C++ STL : unordered_set (해시 기반 중복 없는 집합)

---

## 📘 unordered_set 이란??

- 중복되지 않는 원소들을 저장하는 해시 기반의 컨테이너
- 내부적으로 해시 테이블(hash table)을 사용하여 평균 O(1)의 빠른 탐색, 삽입, 삭제를 지원
- 원소의 순서가 보장되지 않지만, 빠른 검색 성능이 필요한 경우에 매우 유용

---

## ✅ 주요 특징

| 항목 | 설명 |
|------|------|
| 내부 구조 | 해시 테이블 |
| 정렬 여부 | ❌ 없음 (무작위 순서) |
| 중복 여부 | ❌ 불가 (중복 자동 제거) |
| 시간 복잡도 | 평균 `O(1)` (탐색, 삽입, 삭제) |
| 헤더 | `<unordered_set>` |

---

## ✅  예제

```cpp
#include <iostream>
#include <unordered_set>
using namespace std;

int main() {
    unordered_set<int> uset;

    uset.insert(10);
    uset.insert(20);
    uset.insert(30);
    uset.insert(20);  // 중복 무시됨

    cout << "unordered_set 내용: ";
    for (int x : uset) {
        cout << x << " ";
    }
    cout << endl;

    uset.erase(10);

    if (uset.find(20) != uset.end()) {
        cout << "20은 존재합니다." << endl;
    }

    return 0;
}
```

---

## ✅ 출력 결과 (무작위 순서)

```
unordered_set 내용: 30 10 20
20은 존재합니다.
```

---

## ✅ 주요 함수

| 함수 | 설명 |
|------|------|
| `insert(val)` | 값 삽입 |
| `erase(val)` | 값 제거 |
| `find(val)` | 값 존재 여부 확인 |
| `size()` | 요소 개수 반환 |
| `empty()` | 비어 있는지 여부 |
| `clear()` | 전체 요소 제거 |

---

## ✅ set vs unordered_set 차이

|항목|	set	|unordered_set|
|-----|-----|------|
|내부 구조|	이진 탐색 트리 (Red-Black Tree)	|해시 테이블 (Hash Table)|
|원소 정렬 여부|	✅ 자동 정렬됨 (오름차순)|	❌ 순서 보장 안 됨|
|중복 허용 여부|	❌ 중복된 값 저장 불가|	❌ 동일|
|탐색 속도 평균|	O(log n)|	O(1) (충돌 없을 경우)|
|탐색 속도 최악|	O(log n)|	O(n) (해시 충돌이 심한 경우)|
|메모리 |사용	적음|	비교적 많음|
|사용 목적|	정렬된 데이터가 필요한 경우|	빠른 탐색 속도가 중요한 경우|
|사용 가능 시점|	C++98부터 지원	|C++11부터 지원|
---

