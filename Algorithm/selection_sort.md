# 🧮 C++ 알고리즘: 선택 정렬 (Selection Sort)

---

## 📘 선택 정렬 (Selection Sort) 이란??

- 배열에서 가장 작은 값을 선택해 앞쪽부터 차례대로 정렬하는 알고리즘
- 각 단계에서 최솟값을 찾아 현재 위치와 교환하는 방식으로 동작
- 구현이 간단하지만, 시간 복잡도는 O(n²)로 효율이 낮아 작은 데이터에 적합

---

## 🔍 동작 과정

예시 배열: `[5, 3, 8, 4, 2]`

1. 1번째 위치에 가장 작은 값 2 → `[2, 3, 8, 4, 5]`  
2. 2번째 위치에 그다음 작은 값 3 → `[2, 3, 8, 4, 5]`  
3. 3번째 위치에 그다음 작은 값 4 → `[2, 3, 4, 8, 5]`  
4. 4번째 위치에 그다음 작은 값 5 → `[2, 3, 4, 5, 8]`

---

## ✅ 특징 요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 비교 기반, 제자리 정렬(in-place) |
| 시간 복잡도 | 평균/최악/최선 모두 O(n²) |
| 공간 복잡도 | O(1) |
| 안정 정렬 | ❌ (같은 값의 순서가 바뀔 수 있음) |

---

## ✅  예제

```cpp
#include <iostream>
using namespace std;

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        int minIdx = i;
        for (int j = i + 1; j < n; ++j) {
            if (arr[j] < arr[minIdx]) {
                minIdx = j;
            }
        }
     
        int temp = arr[i];
        arr[i] = arr[minIdx];
        arr[minIdx] = temp;
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

    selectionSort(arr, n);

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

