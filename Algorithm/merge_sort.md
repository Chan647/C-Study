# 🧮 C++ 알고리즘 : 병합 정렬 (Merge Sort)

---

## 📘 병합 정렬 (Merge Sort) 이란??

- 배열을 반으로 나누고, 각각 정렬한 뒤 병합하는 분할 정복 기반 정렬 알고리즘
- 정렬된 두 부분 배열을 병합(merge)하면서 하나의 정렬된 배열로 만드는 것이 핵심
- 시간 복잡도는 항상 O(n log n)으로 안정적임

---

## 🔍 동작 과정

예시 배열: `[5, 3, 8, 4, 2]`

1. `[5, 3, 8, 4, 2]` → `[5, 3]` + `[8, 4, 2]`  
2. `[5, 3]` → `[5]`, `[3]` → 병합 → `[3, 5]`  
3. `[8, 4, 2]` → `[8]`, `[4, 2]` → `[4]`, `[2]` → 병합 → `[2, 4]` → 병합 → `[2, 4, 8]`  
4. 최종 병합: `[3, 5]` + `[2, 4, 8]` → `[2, 3, 4, 5, 8]`

---

## ✅  요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 분할 정복, 안정 정렬 |
| 시간 복잡도 | 최선/평균/최악: O(n log n) |
| 공간 복잡도 | O(n) (추가 배열 필요) |
| 안정 정렬 | ✅ (같은 값 순서 보존됨) |

---

## ✅ 예제

```cpp
#include <iostream>
using namespace std;

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1; 
    int n2 = right - mid;    

    // 임시 배열
    int* L = new int[n1];
    int* R = new int[n2];

    // 데이터 복사
    for (int i = 0; i < n1; ++i) L[i] = arr[left + i];
    for (int j = 0; j < n2; ++j) R[j] = arr[mid + 1 + j];

    // 병합
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j])
            arr[k++] = L[i++];
        else
            arr[k++] = R[j++];
    }

    // 남은 데이터 복사
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];

    delete[] L;
    delete[] R;
}

// 병합 정렬
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;

        mergeSort(arr, left, mid);     
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);  
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

    mergeSort(arr, 0, n - 1);

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