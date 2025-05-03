# 📌 C++ 알고리즘 : 동적 계획법 (Dynamic Programming)


--- 

## ✅ 동적 계획법(Dynamic Programming) 이란?

- 큰 문제를 작은 부분 문제로 나누어 풀고, 그 결과를 저장하여 중복 계산을 피하는 최적화 기법
- 부분 문제 최적화 (Optimal Substructure) : 작은 문제의 결과를 조합하여 큰 문제를 해결
- 중복 부분 문제 (Overlapping Subproblems) : 같은 계산을 여러 번 하지 않기 위해 저장

---

## ✅ 예제 : 피보나치 수열

### ✅ 비효율적 재귀 방식

```cpp
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n-1) + fibonacci(n-2);
}
```

### ✅ 메모이제이션 사용 (Top-Down)

```cpp
const int MAX = 100;
int dp[MAX];

int fibonacci(int n) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];
    return dp[n] = fibonacci(n-1) + fibonacci(n-2);
}
```

### ✅ 반복문 사용 (Bottom-Up)

```cpp
int fibonacci(int n) {
    int dp[100];
    dp[0] = 0; dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}
```

---

## 4. 성능 비교

| 방식        | 시간 복잡도 | 공간 복잡도 | 특징 |
|-------------|-------------|--------------|------|
| 재귀        | O(2^n)      | O(n)         | 중복 계산 많아 비효율적 |
| 메모이제이션 | O(n)        | O(n)         | 중복 제거, Top-Down |
| 반복문      | O(n)        | O(n)         | 가장 효율적, Bottom-Up |

---
