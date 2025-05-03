# 🧮 C++ 알고리즘 : 힙 정렬 (Heap Sort)


---

## 📘 힙 정렬 (Heap Sort) 이란??

- 최대 힙(Max Heap) 또는 최소 힙(Min Heap)을 이용해 정렬하는 알고리즘
- 배열을 힙 구조로 변환한 후, 가장 큰(또는 작은) 값을 하나씩 꺼내어 정렬
- 시간 복잡도는 항상 O(n log n)이며, 불안정 정렬

---

## 🔍 동작 과정

예시 배열: `[5, 3, 8, 4, 2]`

1. 최대 힙 구성 → `[8, 4, 5, 3, 2]`  
2. 8과 끝값 교환 → `[2, 4, 5, 3, 8]`  
3. 힙 재구성 → `[5, 4, 2, 3, 8]`  
4. 반복 → `[2, 3, 4, 5, 8]` (오름차순 정렬 완료)

---

## ✅ 요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 비교 기반, 제자리 정렬 (in-place) |
| 시간 복잡도 | 최선/평균/최악: O(n log n) |
| 공간 복잡도 | O(1) |
| 안정 정렬 | ❌ (같은 값의 순서 보존 안됨) |

---

## ✅ 예제

```cpp
#include <iostream>
using namespace std;

// 힙 재구성
void heapify(int arr[], int n, int i) {
    int largest = i;       
    int left = 2 * i + 1;     
    int right = 2 * i + 2;    

    if (left < n && arr[left] > arr[largest])
        largest = left;

    if (right < n && arr[right] > arr[largest])
        largest = right;

    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}

// 힙 정렬
void heapSort(int arr[], int n) {
    // 최대 힙 생성
    for (int i = n / 2 - 1; i >= 0; --i)
        heapify(arr, n, i);

    // 요소 하나씩 꺼내서 정렬
    for (int i = n - 1; i > 0; --i) {
        swap(arr[0], arr[i]);  
        heapify(arr, i, 0);    
    }
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {5, 3, 8, 4, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Before sorting: ";
    printArray(arr, n);

    heapSort(arr, n);

    cout << "After sorting: ";
    printArray(arr, n);

    return 0;
}
```
## ✅ 출력 결과

``` 
Before sorting: 5 3 8 4 2 
After sorting: 2 3 4 5 8

```