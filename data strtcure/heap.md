#  자료구조: 힙 (Heap)

## 📂 힙이란?

- 완전 이진 트리 기반 자료구조
- 우선순위 큐 구현에 사용
- 두 가지 종류 있음: 최대 힙(Max Heap), 최소 힙(Min Heap)

## ✅ 힙의 종류

- 최대 힙 (Max Heap): 부모 ≥ 자식
- 최소 힙 (Min Heap): 부모 ≤ 자식

## 🔧 힙의 구조

- 완전 이진 트리
- 배열로 구현 가능
- 인덱스 기반 규칙:
  - 부모: `(i - 1) / 2`
  - 왼쪽 자식: `2 * i + 1`
  - 오른쪽 자식: `2 * i + 2`

## ⏱️  시간 복잡도

|        |                    |
|--------|--------------------|
| (push) |  O(log n)|  
| (pop)  | O(log n)  | 
| (top)  |O(1)       |


## 🔹 최대 힙 예시

```cpp 
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> heap = {10, 20, 5, 30, 25};
    make_heap(heap.begin(), heap.end());
    heap.push_back(40);
    push_heap(heap.begin(), heap.end());
    pop_heap(heap.begin(), heap.end());
    heap.pop_back();
    sort_heap(heap.begin(), heap.end());

    for (int n : heap)
        cout << n << " ";
    return 0;
}

## 🔹 최소 힙 예시

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> heap = {10, 20, 5, 30, 25};
    make_heap(heap.begin(), heap.end(), greater<>());
    heap.push_back(2);
    push_heap(heap.begin(), heap.end(), greater<>());
    pop_heap(heap.begin(), heap.end(), greater<>());
    heap.pop_back();
    sort_heap(heap.begin(), heap.end(), greater<>());

    for (int n : heap)
        cout << n << " ";
    return 0;
}
```

## 🔹사용 예시

- 우선순위 큐
- 작업 스케줄링
- 다익스트라 알고리즘
- 최소 비용 문제
