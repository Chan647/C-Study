# 🧮 C++ 알고리즘 : 퀵 정렬 (Quick Sort)


---

## 📘 퀵 정렬 (Quick Sort) 이란??

- 분할 정복(divide and conquer) 전략을 사용하는 고속 정렬 알고리즘입니다.
- 피벗(pivot)을 기준으로 배열을 작은 값과 큰 값으로 분할한 뒤, 재귀적으로 정렬
- 평균 시간 복잡도는 O(n log n)으로 빠르지만, 최악의 경우 O(n²)도 발생할 수 있음

---

## 🔍 동작 과정

예시 배열: `[5, 3, 8, 4, 2]`  
- 피벗: 5  
- 왼쪽(작은 값들): `[3, 4, 2]`  
- 오른쪽(큰 값들): `[8]`  
- 정렬 후: `[2, 3, 4] + [5] + [8]` → `[2, 3, 4, 5, 8]`

---

## ✅  요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 분할 정복, 제자리 정렬(in-place) |
| 시간 복잡도 | 평균: O(n log n), 최악: O(n²) |
| 공간 복잡도 | O(log n) (재귀 호출 스택) |
| 안정 정렬 | ❌ (동일한 값 순서 보장 X) |

---

## ✅  예제

```cpp
#include <iostream>
using namespace std;

// 분할 함수
int partition(int arr[], int low, int high) {
    int pivot = arr[high];  
    int i = low - 1;       

    for (int j = low; j < high; ++j) {
        if (arr[j] < pivot) {
            ++i;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

// 퀵 정렬 함수
void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high); 

        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
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

    quickSort(arr, 0, n - 1);

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
