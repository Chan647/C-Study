# 🧮 C++ 알고리즘 : 기수 정렬 (Radix Sort)


---

## 📘 기수 정렬 (Radix Sort) 이란??

- 자릿수별로 정렬을 반복하여 전체 숫자를 정렬하는 비교 기반이 아닌 정렬 알고리즘
- LSD(Least Significant Digit) 방식으로 낮은 자릿수부터 차례대로 안정 정렬을 수행
- 시간 복잡도는 O(n × k)로, 비교 기반 정렬보다 빠를 수 있으며 숫자 정렬에 매우 효과적

---

## 🔍 동작 과정

예시 배열: `[170, 45, 75, 90, 802, 24, 2, 66]`

1. 1의 자리 기준 정렬 → `[170, 90, 802, 2, 24, 45, 75, 66]`  
2. 10의 자리 기준 정렬 → `[802, 2, 24, 45, 66, 170, 75, 90]`  
3. 100의 자리 기준 정렬 → `[2, 24, 45, 66, 75, 90, 170, 802]`

---

## ✅ 요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 비교하지 않음, 자릿수 기반 |
| 시간 복잡도 | O(n * k) (n: 원소 개수, k: 자릿수) |
| 공간 복잡도 | O(n + k) |
| 안정 정렬 | ✅ (Counting Sort 기반) |
| 제약 조건 | 정수에만 사용 가능 |

---

##  ✅ 예제

```cpp
#include <iostream>
using namespace std;

void countingSort(int arr[], int n, int exp) {
    int output[n];
    int count[10] = {0};

    // 자릿수에 따라 카운트
    for (int i = 0; i < n; ++i)
        count[(arr[i] / exp) % 10]++;

    // 누적합
    for (int i = 1; i < 10; ++i)
        count[i] += count[i - 1];

    // 출력 배열 생성 
    for (int i = n - 1; i >= 0; --i) {
        int digit = (arr[i] / exp) % 10;
        output[count[digit] - 1] = arr[i];
        count[digit]--;
    }

   
    for (int i = 0; i < n; ++i)
        arr[i] = output[i];
}

// 기수 정렬
void radixSort(int arr[], int n) {
  
    int maxVal = arr[0];
    for (int i = 1; i < n; ++i)
        if (arr[i] > maxVal)
            maxVal = arr[i];


    for (int exp = 1; maxVal / exp > 0; exp *= 10)
        countingSort(arr, n, exp);
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {170, 45, 75, 90, 802, 24, 2, 66};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Before sorting: ";
    printArray(arr, n);

    radixSort(arr, n);

    cout << "After sorting: ";
    printArray(arr, n);

    return 0;
}
```

## ✅ 출력 결과

``` 
Before sorting: 170 45 75 90 802 24 2 66 
After sorting: 2 24 45 66 75 90 170 802

```