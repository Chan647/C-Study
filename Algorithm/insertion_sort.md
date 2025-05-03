# 🧮 C++ 알고리즘 : 삽입 정렬 (Insertion Sort)

---

## 📘 삽입 정렬 (Insertion Sort) 이란??

- 배열의 각 원소를 순차적으로 정렬된 부분에 적절하게 삽입해나가는 정렬 알고리즘
- 매 반복마다 현재 원소를 앞쪽의 정렬된 부분과 비교하며 올바른 위치에 끼워 넣음으로써 정렬을 진행
- 간단하고 안정적인 알고리즘이지만, 최악 및 평균 시간 복잡도가 O(n²)이어서 데이터가 많을 때는 비효율적

---

## 🔍 동작 과정

예시 배열: `[5, 3, 8, 4, 2]`

1. 3은 5보다 작으므로 앞으로 이동 → `[3, 5, 8, 4, 2]`  
2. 8은 제자리 유지 → `[3, 5, 8, 4, 2]`  
3. 4는 8보다 작고 5보다 작음 → `[3, 4, 5, 8, 2]`  
4. 2는 모두보다 작음 → `[2, 3, 4, 5, 8]`

---

## ✅ 특징 요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 비교 기반, 제자리 정렬(in-place) |
| 시간 복잡도 | 평균/최악: O(n²), 최선(이미 정렬): O(n) |
| 공간 복잡도 | O(1) |
| 안정 정렬 | ✅ (같은 값의 순서 보존) |

---

## ✅ 예제

```cpp
#include <iostream>
using namespace std;

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
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

    insertionSort(arr, n);

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
