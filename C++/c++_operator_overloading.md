#  🧬 C++ : 연산자 오버로딩 (Operator Overloading)


---

## ✅ 기본 개념

- C++에서는 사용자 정의 타입(클래스)에도 `+`, `==`, `[]` 등 연산자를 직접 구현할 수 있음. 이를 연산자 오버로딩이라 함
- 연산자 오버로딩은 `operator+`, `operator==` 등으로 함수처럼 정의
- 주로 가독성과 직관성을 위해 사용
- 객체끼리의 수학 연산, 비교, 출력 등을 가능하게 함

---

## ✅ 예제 

```cpp
#include <iostream>
using namespace std;

class Point {
private:
    int x, y;

public:
    Point(int a = 0, int b = 0) : x(a), y(b) {}

    // 연산자 오버로딩: +
    Point operator+(const Point& other) {
        return Point(x + other.x, y + other.y);
    }

    // 연산자 오버로딩: ==
    bool operator==(const Point& other) {
        return x == other.x && y == other.y;
    }

    void print() {
        cout << "(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    Point p1(2, 3);
    Point p2(4, 1);

    Point p3 = p1 + p2;  // operator+ 호출
    p3.print();          // (6, 4)

    if (p1 == p2) {
        cout << "같은 좌표입니다." << endl;
    } else {
        cout << "다른 좌표입니다." << endl;
    }

    return 0;
}
```

---

## ✅ 출력 결과

```
(6, 4)
다른 좌표입니다.
```

---

## 🧠  요약

| 항목 | 설명 |
|------|------|
| `operator+` | 객체 간 더하기 구현 |
| `operator==` | 객체 비교 구현 |
| 연산자 함수는 멤버 함수로 구현 | 비멤버 함수로도 가능 |
| `<<`, `[]`, `()` 등도 오버로딩 가능 | STL 호환성 강화 |

---


