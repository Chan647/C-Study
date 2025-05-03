
# 📌 C++ 알고리즘 : 이진 탐색 (Binary Search)


---

## ✅ 이진 탐색 (Binary Search)이란?

- 정렬된 배열에서만 사용 가능한 탐색 알고리즘
- 탐색 범위를 절반씩 줄이며 값을 찾음
- 시간 복잡도 : O(log n)

---

## 🔧 이진 탐색 예제

```cpp
#include <iostream>
#include <vector>
using namespace std;

int binarySearch(const vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;
}

int main() {
    vector<int> arr = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
    int target;

    cout << "찾고 싶은 숫자를 입력하세요: ";
    cin >> target;

    int result = binarySearch(arr, target);

    if (result != -1) {
        cout << "찾는 값 " << target << " 은(는) 인덱스 " << result << " 에 있습니다." << endl;
    } else {
        cout << "찾는 값이 배열에 없습니다." << endl;
    }

    return 0;
}
```

---

## 🧰 STL `binary_search` 사용 예제

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> arr = {2, 4, 6, 8, 10, 12, 14};
    int target = 8;

    if (binary_search(arr.begin(), arr.end(), target)) {
        cout << "찾았다! " << target << " 은(는) 배열 안에 있어요." << endl;
    } else {
        cout << "못찾았다! " << target << " 은(는) 배열에 없어요." << endl;
    }

    return 0;
}
```

--- 

## 📝 요약

| 항목 | 설명 |
|------|------|
| 전제조건 | 정렬된 배열 |
| 시간 복잡도 | O(log n) |
| 직접 구현 | 인덱스를 반환 |
| STL 함수 | 값의 존재 여부만 반환 (bool) |
| 관련 함수 | `binary_search`, `lower_bound`, `upper_bound` |

