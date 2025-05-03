# 🧮 C++ 알고리즘 : 버블 정렬 (Bubble Sort)

---

## 📘 버블 정렬(Bubble Sort)이란??

-  서로 인접한 두 원소를 비교하여 교환하는 방식의 정렬 알고리즘
- 구현이 간단하지만, 시간 복잡도는 O(n²)로 느려서 작은 데이터에 적합

---

## 🔍 동작 과정

예시 배열: `[5, 3, 8, 4, 2]`

1. (5,3) → 교환 → `[3,5,8,4,2]`  
2. (5,8) → 그대로  
3. (8,4) → 교환 → `[3,5,4,8,2]`  
4. (8,2) → 교환 → `[3,5,4,2,8]`  
...  
최종 결과: `[2, 3, 4, 5, 8]`

---

## ✅  요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 비교 기반, 제자리 정렬(in-place) |
| 시간 복잡도 | 평균/최악: O(n²), 최선(이미 정렬): O(n) |
| 공간 복잡도 | O(1) |
| 안정 정렬 | ✅ (같은 값의 원소 순서 보존) |

---

## ✅ 예제

```cpp
#include <iostream>
using namespace std;

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        bool swapped = false;
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                // swap
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        if (!swapped) break;
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

    bubbleSort(arr, n);

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
