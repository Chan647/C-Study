# 🧮 C++ 알고리즘 : 계수 정렬 (Counting Sort)


---

## 📘 계수 정렬 (Counting Sort) 이란??

- 각 숫자의 등장 횟수를 세어 정렬하는 비교 기반이 아닌 정렬 알고리즘
- 값의 범위가 작고 정수일 때 매우 빠른 O(n + k)의 시간 복잡도를 가짐
- 음수를 처리하려면 보정이 필요하며, 많은 메모리를 사용한다는 단점이 있음

---

## 🔍 동작 과정

예시 배열: `[4, 2, 2, 8, 3, 3, 1]`

1. 최댓값: 8 → count 배열 크기: 9  
2. 등장 횟수 기록  
   → `count[1]=1, count[2]=2, count[3]=2, count[4]=1, count[8]=1`  
3. 누적합 계산  
4. 안정 정렬 (뒤에서부터 순회하며 출력 배열 구성)  
5. 결과: `[1, 2, 2, 3, 3, 4, 8]`

---

## ✅ 요약

| 항목 | 설명 |
|------|------|
| 정렬 방식 | 값의 개수 기반 |
| 시간 복잡도 | O(n + k) (k: 최댓값) |
| 공간 복잡도 | O(k) |
| 안정 정렬 | ✅ (역순 순회로 보장) |
| 제약 조건 | 정수만 가능, 음수 ❌, 범위 작아야 효율적 |

---

## ✅ 예제

```cpp
#include <iostream>
#include <vector>
using namespace std;

void countingSort(int arr[], int n) {
    // 최댓값 탐색
    int maxVal = arr[0];
    for (int i = 1; i < n; ++i)
        if (arr[i] > maxVal)
            maxVal = arr[i];

    // 카운트 배열 생성
    vector<int> count(maxVal + 1, 0);
    for (int i = 0; i < n; ++i)
        count[arr[i]]++;

    // 누적합 계산
    for (int i = 1; i <= maxVal; ++i)
        count[i] += count[i - 1];


    int output[n];
    for (int i = n - 1; i >= 0; --i) {
        output[count[arr[i]] - 1] = arr[i];
        count[arr[i]]--;
    }

 
    for (int i = 0; i < n; ++i)
        arr[i] = output[i];
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {4, 2, 2, 8, 3, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Before sorting: ";
    printArray(arr, n);

    countingSort(arr, n);

    cout << "After sorting: ";
    printArray(arr, n);

    return 0;
}
```

## ✅ 출력 결과

``` 
Before sorting: 4 2 2 8 3 3 1 
After sorting: 1 2 2 3 3 4 8

```