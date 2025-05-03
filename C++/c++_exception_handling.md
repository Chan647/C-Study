
# ⚠️ C++ : 예외 처리 (Exception Handling)


---

## ✅ 기본 개념

- 예외 처리는 프로그램 실행 중 발생할 수 있는 예기치 못한 오류를 안전하게 처리하는 C++의 구조.

| 키워드 | 설명 |
|--------|------|
| `try` | 예외가 발생할 수 있는 코드 블록 |
| `throw` | 예외를 발생시키는 키워드 |
| `catch` | 예외를 처리하는 블록 (예외의 타입에 따라 선택적으로 처리) |

---

## ✅ 기본 구조

```cpp
try {
    // 예외 발생 가능성 있는 코드
} catch (예외 타입 변수) {
    // 예외 발생 시 처리할 코드
}
```

---

## ✅ 1. try

- 예외가 발생할 수 있는 코드 블록을 감싸는 영역
- 내부에서 `throw`가 실행되면 제어가 `catch`로 이동함

```cpp
try {
    int result = divide(10, 0);
}
```

---

## ✅ 2. throw

- 예외를 직접 발생시키는 키워드
- 즉시 `catch` 블록으로 점프함

```cpp
if (b == 0)
    throw "0으로 나눌 수 없습니다!";  // 문자열 예외 발생
```

- 문자열을 던지면: `const char*` 타입
- 숫자를 던지면: `int` 타입

---

## ✅ 3. catch

- `throw`로 던져진 예외를 받아서 처리하는 블록
- 예외의 타입에 따라 여러 catch 구문 작성 가능

```cpp
catch (const char* msg) {
    cout << "예외 발생: " << msg << endl;
}

catch (int errorCode) {
    cout << "오류 코드: " << errorCode << endl;
}
```

## ✅ 예제

```cpp
#include <iostream>
using namespace std;

double divide(int a, int b) {
    if (b == 0)
        throw "0으로 나눌 수 없습니다!";
    return static_cast<double>(a) / b;
}

int main() {
    try {
        cout << divide(10, 2) << endl;  // 출력: 5
        cout << divide(5, 0) << endl;   // 예외 발생
    }
    catch (const char* msg) {
        cout << "예외 발생: " << msg << endl;
    }
    return 0;
}
```

### ✅ 출력 결과

```
5
예외 발생: 0으로 나눌 수 없습니다!
```

---

## ✅ 다양한 예외 타입 처리

```cpp
throw int(123);                // 정수 예외
throw string("문자열 예외");   // 문자열 예외
throw runtime_error("에러");   // 표준 라이브러리 예외

catch (int e) { ... }
catch (const string& s) { ... }
catch (const exception& e) { ... }
```

---

## 🧠 요약 

| 개념 | 설명 |
|------|------|
| `throw` | 실행 중 예외를 발생 |
| `try` | 예외 발생 가능 코드 블록 |
| `catch` | 예외가 발생했을 때 실행되는 블록 |
| 예외 타입 | 문자열, 숫자, 표준 예외 클래스 등 다양하게 가능 |

---
