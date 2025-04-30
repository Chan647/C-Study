# 자료구조 : 해시테이블(Hash Table)  `unordered_map` / `unordered_set`

## 📂 해시테이블(Hash Table) 이란?
- 해시 테이블은 키(key)를 해시 함수로 변환해 계산된 인덱스에 데이터를 저장하는 키-값 기반 자료구조
- 빠른 데이터 검색과 삽입이 가능하며, 평균 시간 복잡도는 O(1)
- 충돌(collision)을 해결하기 위한 별도의 처리 기법(예: 체이닝, 개방 주소법)이 필요함


## ⏱️ 시간복잡도 
|          |                 |
|----------|-----------------|
| (Search)|	O(1)|
| (Insert)|	O(1)|
| (Delete)|	O(1)|

## ✅ 특징

- 빠른 탐색 속도: 평균적으로 O(1)에 가까운 시간 복잡도
- 충돌(Collision) 처리 필요
- C++에서는 주로 std::unordered_map 또는 std::unordered_set으로 사용

## 🔧 기본 구조
- 해시 함수: 키를 숫자로 변환해 배열의 인덱스로 사용
- 버킷(Bucket): 데이터를 저장하는 배열의 한 칸
- 충돌 처리 방식:
   - 체이닝(Chaining): 같은 인덱스에 연결 리스트로 저장
   - 개방 주소법(Open Addressing): 빈 버킷을 찾아 저장

## 📌 unordered_map 개념

- (key, value) 쌍을 저장하는 해시테이블
- 평균 시간복잡도 O(1)
- 내부적으로 해시함수 + 체이닝 구조 사용


### 🔹 예시

```cpp
#include <unordered_map>
#include <string>
using namespace std;

unordered_map<int, string> hashTable;

hashTable[1] = "Apple";
hashTable[2] = "Banana";
hashTable[42] = "Cherry"; // 충돌 예시

for (const auto& pair : hashTable) {
    cout << pair.first << " : " << pair.second << endl;
}
```


### 🔹 주요 메서드

|                   |                         |
|-------------------|-------------------------|
| insert({key, val})|  값 삽입 |
| find(key)  |         반복자 반환, 없으면 `end()`| 
| erase(key)|          키 삭제 |
| size()  |            원소 개수| 
| clear() |             전체 삭제 |
| [key]|                 삽입 및 접근 |


## 📌  unordered_set 개념

- 값 하나만 저장하는 해시 기반 집합
- 중복 불가
- 빠른 삽입/탐색용으로 유용

### 🔹 예시

```cpp
#include <unordered_set>
using namespace std;

unordered_set<int> s = {10, 20, 30};

for (const auto& elem : s) {
    cout << elem << endl;
}
```

### 🔹 예시 비교

#### `unordered_map`

```cpp
for (const auto& pair : hashTable) {
    cout << pair.first << ", " << pair.second << endl;
}
```

#### `unordered_set`

```cpp
for (const auto& elem : s) {
    cout << elem << endl;
}
```