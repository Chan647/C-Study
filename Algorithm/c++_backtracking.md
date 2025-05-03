# 📌 C++ 알고리즘 : 백트래킹 (Backtracking)

---

## ✅ 백트래킹(Backtracking) 이란?

- 모든 경우의 수를 탐색하되, 유망하지 않은 경로는 빠르게 포기하고 다른 경로를 탐색하는 기법
- 모든 가능한 선택지를 시도하지만, 중간에 조건에 맞지 않으면 탐색을 멈추고 되돌아옴
- 보통 재귀(Recursion)를 사용해 구현

---

### 🔄 백트래킹 흐름

1. 현재 상태에서 가능한 선택지를 하나 선택
2. 그 선택지로 재귀 호출 (다음 단계로 이동)
3. 조건을 만족하지 않으면 되돌아오기 (Backtrack)
4. 다른 선택지를 탐색

---

## 🧪예제: 순열 만들기

- 1부터 N까지 숫자를 이용해 가능한 모든 순열을 생성

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> permutation;
vector<bool> visited;

void backtrack(int n, int depth) {
    if (depth == n) {
        for (int num : permutation) {
            cout << num << " ";
        }
        cout << endl;
        return;
    }

    for (int i = 1; i <= n; ++i) {
        if (!visited[i]) {
            visited[i] = true;
            permutation.push_back(i);
            backtrack(n, depth + 1);
            visited[i] = false;
            permutation.pop_back();
        }
    }
}

int main() {
    int n;
    cout << "n을 입력하세요: ";
    cin >> n;

    visited.resize(n + 1, false);
    backtrack(n, 0);

    return 0;
}
```

### 🧾 입력 예시
```
n을 입력하세요: 3
```

### ✅ 출력 결과
```
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```

## ✅ 요약

- "선택 → 이동 → 복구" 순서로 진행
- visited 배열과 결과 벡터를 잘 관리할 것
- 다양한 문제에 확장 가능 (N-Queen, 미로 탐색, 조합, 부분 집합 등)
