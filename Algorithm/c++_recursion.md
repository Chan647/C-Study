# 📌C++ 알고리즘 : 재귀 (Recursion)

---

## ✅ 재귀란?

- 자기 자신을 다시 호출하는 함수
- 문제를 더 작은 문제로 나누어 해결
- 반드시 종료 조건(Base Case)이 있어야 함
- 반복문 없이도 반복적인 로직 구현 가능

---

### 📌 구조

```cpp
return_type function_name(parameters) {
    if (종료 조건)
        return 값;
    else
        return function_name(더 작은 문제);
}
```

---

## 🧪 예제 : 팩토리얼 (n!)

```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    if (n == 0)
        return 1;
    else
        return n * factorial(n - 1);
}

int main() {
    int number;
    cout << "정수를 입력하세요: ";
    cin >> number;

    cout << number << "! = " << factorial(number) << endl;
    return 0;
}
```

### ✅ 출력 결과

```
정수를 입력하세요: 5
5! = 120
```

---

## 🧪 예제 : 피보나치 수열

```cpp
#include <iostream>
using namespace std;

int fibonacci(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;
    cout << "몇 번째 피보나치 수를 구할까요? ";
    cin >> n;

    cout << n << "번째 피보나치 수는 " << fibonacci(n) << "입니다." << endl;
    return 0;
}
```

### ✅ 출력 결과

```
몇 번째 피보나치 수를 구할까요? 6
6번째 피보나치 수는 8입니다.
```

---

## ⚠️ 주의사항
- 재귀에는 반드시 종료 조건이 있어야 함
- 너무 깊은 재귀는 스택 오버플로우 발생 가능
- 반복문으로 대체 가능한 경우도 있음


