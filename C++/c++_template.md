# 📦 C++ :  템플릿 (Templates) 

---

## ✅ 기본 개념

- 템플릿은 자료형에 관계없이 함수와 클래스를 재사용할 수 있게 해주는 C++ 기능

| 항목 | 설명 |
|------|------|
| 함수 템플릿 | 다양한 타입에 대해 동일한 동작 수행 |
| 클래스 템플릿 | 타입에 따라 유연한 클래스 생성 |
| 장점 | 코드 재사용성 향상, 자료형 유연성 확보 |

---

## ✅ 예제 - 함수

```cpp
#include <iostream>
using namespace std;

template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    cout << add(3, 5) << endl;                // int
    cout << add(2.5, 4.1) << endl;            // double
    cout << add<string>("Hi, ", "Everyone") << endl;  // string
}
```

### ✅ 출력 결과

```
8
6.6
Hi, Everyone
```

---

## ✅  예제 - 클래스

```cpp
template <typename T>
class Box {
private:
    T value;

public:
    Box(T v) : value(v) {}

    void show() {
        cout << "값: " << value << endl;
    }
};
```

```cpp
int main() {
    Box<int> b1(10);
    Box<string> b2("Hello");

    b1.show();  
    b2.show();  
}
```
---

### ✅ 출력 결과

```
값: 10
값: Hello

```

---
## 🧠  요약

| 항목 | 설명 |
|------|------|
| `template<typename T>` | 템플릿 타입 변수 선언 |
| `add<T>()` | T 타입을 기반으로 함수 생성 |
| `Box<T>` | T 타입에 맞는 클래스 인스턴스 생성 |
| 장점 | 코드 중복 제거, 타입 안전성 보장 |

---

