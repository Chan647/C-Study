# 🧩 C++ : 추상 클래스(Abstract Class) & 순수 가상 함수 (Pure_Virtual_Function)

---

## ✅ 기본 개념

| 용어 | 설명 |
|------|------|
| 추상 클래스 | 하나 이상의 순수 가상 함수를 포함하는 클래스 |
| 순수 가상 함수 | 구현 없이 선언만 존재하는 함수 (`= 0`) |
| 목적 | 자식 클래스에 강제로 공통 인터페이스 구현을 요구 |

---

## ✅ 추상 클래스 정의

```cpp
class Shape {
public:
    virtual double area(double x, double y = 0) = 0;  // 순수 가상 함수
};
```

- `= 0`은 이 함수가 순수 가상 함수임을 나타냄
- `Shape` 클래스는 객체로 만들 수 없음

---

## ✅ 자식 클래스에서 구현

```cpp
class Rectangle : public Shape {
public:
    double area(double width, double height) override {
        return width * height;
    }
};

class Circle : public Shape {
public:
    double area(double radius, double unused = 0) override {
        return 3.14159 * radius * radius;
    }
};

int main() {
    Shape* s1 = new Rectangle();
    Shape* s2 = new Circle();

    cout << "사각형 넓이 (3 x 4): " << s1->area(3, 4) << endl;
    cout << "원 넓이 (반지름 5): " << s2->area(5) << endl;

    delete s1;
    delete s2;
    return 0;
}
```

---

## ✅ 출력 결과

```
사각형 넓이 (3 x 4): 12
원 넓이 (반지름 5): 78.5397
```

---

## 🧠  요약

| 항목 | 설명 |
|------|------|
| `= 0` | 순수 가상 함수, 자식 클래스에서 반드시 구현해야 함 |
| 추상 클래스 | 직접 객체 생성 불가 |
| 오버라이딩 | 자식 클래스에서 `override` 필수 |
| 다형성 활용 | 부모 포인터 → 자식 함수 호출 (동적 바인딩) |

---

