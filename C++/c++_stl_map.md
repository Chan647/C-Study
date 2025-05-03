
# 🗂️ C++ STL : map (정렬된 키-값 쌍)


---
## 📘 map이란??

- map은 키-값(key-value) 쌍을 저장하는 연관 컨테이너
- 키는 자동으로 정렬되며 중복이 허용되지 않으며, 탐색 속도가 빠름
- 내부적으로 이진 탐색 트리(Red-Black Tree)로 구현되어 있어 정렬과 탐색에 효율적

---

## ✅  예제

```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<string, int> score;

    score["철수"] = 85;
    score["영희"] = 92;
    score["민수"] = 78;

    for (auto& pair : score) {
        cout << pair.first << " : " << pair.second << endl;
    }

    cout << "영희 점수: " << score["영희"] << endl;

    score.erase("민수");

    cout << "삭제 후: " << endl;
    for (auto& p : score) {
        cout << p.first << " : " << p.second << endl;
    }

    return 0;
}
```

---

## ✅ 출력 예시

```
민수 : 78
영희 : 92
철수 : 85
영희 점수: 92
삭제 후:
영희 : 92
철수 : 85
```

---

## ✅ 주요 함수

| 함수 | 설명 |
|------|------|
| `m[key] = val` | 값 삽입 또는 수정 |
| `m.at(key)` | 안전하게 접근 (예외 발생 가능) |
| `m.find(key)` | 키에 대한 iterator 반환 (`end()`이면 없음) |
| `m.erase(key)` | 해당 키 삭제 |
| `m.size()` | 전체 쌍 수 반환 |
| `m.empty()` | 비어있는지 확인 |

---

## ✅  요약

- 자동 정렬 (`O(log n)`)
- 중복 키 불가
- 삽입과 삭제도 빠름
- 키와 값의 타입은 자유롭게 설정 가능 (`map<string, int>`, `map<int, string>` 등)

---

