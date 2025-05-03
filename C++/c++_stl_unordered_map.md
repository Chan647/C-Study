
# ⚡ C++ STL :  unordered_map (해시 기반 키-값 저장)


---

## 📘 unordered_map 이란??

- unordered_map은 순서를 고려하지 않고 키-값 쌍을 저장하는 해시 기반 연관 컨테이너
- 내부적으로 해시 테이블(hash table)을 사용하여 평균적으로 O(1)의 빠른 검색 속도를 제공
- 키의 정렬은 보장되지 않지만, 탐색, 삽입, 삭제가 매우 빠른 것이 장점

---

## ✅  예제

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    unordered_map<string, int> um;

    um["apple"] = 100;
    um["banana"] = 200;
    um["cherry"] = 300;

    cout << "banana: " << um["banana"] << endl;

    for (auto& pair : um) {
        cout << pair.first << " : " << pair.second << endl;
    }

    if (um.find("apple") != um.end()) {
        cout << "apple 존재!" << endl;
    }

    um.erase("cherry");

    return 0;
}
```

---

## ✅ 출력 결과

```
banana: 200
banana : 200
apple : 100
cherry : 300
apple 존재!
```

---

## ✅ 주요 함수

| 함수 | 설명 |
|------|------|
| `um[key] = val` | 값 삽입 또는 수정 |
| `um.at(key)` | 안전한 접근 (예외 발생 가능) |
| `um.find(key)` | 키가 존재하는지 확인 |
| `um.erase(key)` | 해당 키 삭제 |
| `um.size()` | 전체 요소 수 |
| `um.empty()` | 비어 있는지 여부 |

---

## ✅ map vs unordered_map 차이

|항목|	map|	unordered_map|
|----|----|------|
|내부 구조|	Red-Black Tree (이진 탐색 트리)|	Hash Table (해시 테이블)|
|정렬 여부|	키(key)가 자동 정렬됨 (오름차순)|	정렬되지 않음 (입력 순서 무관)|
|탐색 속도 평균|	O(log n)|	O(1) (충돌 없을 때)|
|탐색 속도 최악|	O(log n)	|O(n) (해시 충돌 심할 경우)|
|중복 키 허용 여부|	❌ 중복 키 허용 안됨|	❌ 중복 키 허용 안됨|
|메모리 사용량|	상대적으로 적음|	해시 테이블로 인해 더 많음|
|사용 조건|	정렬된 키가 필요할 때|	빠른 접근이 중요할 때|
|C++ 버전|	C++98부터 지원|	C++11부터 지원|

---
