# 🧠 C++ : 다형성 (Polymorphism) 

---

## 📘 다형성(Polymorphism) 이란?

- 다형성은 같은 인터페이스로 서로 다른 동작을 수행할 수 있게 하는 객체지향 개념
- C++에서는 주로 가상 함수(virtual function)를 통해 런타임 다형성을 구현
- 이를 통해 유연하고 확장성 있는 코드를 작성할 수 있으며, 동적 바인딩이 핵심

## ✅ 핵심 키워드

| 키워드 | 설명 |
|--------|------|
| `virtual` | 부모 클래스 함수가 자식에서 재정의될 수 있도록 허용 |
| `override` | 자식 클래스가 부모의 virtual 함수를 재정의할 때 명시 |
| 다형성 | 하나의 인터페이스로 여러 동작을 수행할 수 있는 능력 |

## ✅ 동적 바인딩이란? 

- 동적 바인딩이란, 프로그램 실행 중(runtime)에 호출할 함수가 결정되는 방식
- C++에서는 virtual 함수가 선언된 경우, 포인터나 참조를 통해 함수가 호출될 때 객체의 실제 타입에 따라 어떤 함수가 실행될지 결정됨

---

## ✅ 예제 

```cpp
#include <iostream>
using namespace std;

class Animal {
public:
    virtual void speak() {
        cout << "동물이 소리를 냅니다." << endl;
    }
};

class Dog : public Animal {
public:
    void speak() override {
        cout << "멍멍!" << endl;
    }
};

class Cat : public Animal {
public:
    void speak() override {
        cout << "야옹!" << endl;
    }
};

int main() {
    Animal* a1 = new Dog();
    Animal* a2 = new Cat();

    a1->speak();  // 멍멍!
    a2->speak();  // 야옹!

    delete a1;
    delete a2;
    return 0;
}
```
---

## ✅ 출력 결과

```
멍멍!
야옹!
```

---

## ✅ 예제 

```cpp
#include <iostream>
#include <cmath>
using namespace std;

// 부모 클래스
class Shape {
public:
    virtual double area(double x, double y = 0) = 0;  // 순수 가상 함수 (추상 클래스)
};

// 자식 클래스: 직사각형
class Rectangle : public Shape {
public:
    double area(double width, double height) override {
        return width * height;
    }
};

// 자식 클래스: 원
class Circle : public Shape {
public:
    double area(double radius, double unused = 0) override {
        return 3.14159 * radius * radius;
    }
};

int main() {
    Shape* s1 = new Rectangle();
    Shape* s2 = new Circle();

    cout << "직사각형 (3x4)의 넓이: " << s1->area(3, 4) << endl;
    cout << "원 (반지름 5)의 넓이: " << s2->area(5) << endl;

    delete s1;
    delete s2;
    return 0;
}

```
---

##  ✅ 출력 결과

```
직사각형 (3x4)의 넓이: 12
원 (반지름 5)의 넓이: 78.5397
```
---


## ✅ 동작 요약

| 개념 | 설명 |
|------|------|
| 부모 포인터로 자식 객체 가리킴 | `Animal* a = new Dog();` |
| virtual 함수 | 런타임 시 실제 객체 타입에 따라 함수 호출 (동적 바인딩) |
| override | 정확한 재정의 명시, 실수 방지 |

---

## ⚠️ 만약 virtual을 생략하면?

```cpp
class Animal {
public:
    void speak() {  // virtual 없음
        cout << "동물이 소리를 냅니다." << endl;
    }
};
```

- `Animal* a = new Dog(); a->speak();`  
  → 출력: `"동물이 소리를 냅니다."`  
  → 정적 바인딩 발생

---

## ✅ 정적바인딩이란?

- 함수 호출이 컴파일 시간에 결정되는 방식입니다.
- 주로 비가상 함수, static 함수, 생성자 등에 적용되며, 실행 속도가 빠름

---

## 🔧 특징

|항목|	설명|
|----|-----|
|시점|	컴파일 타임에 결정됨|
|성능|	빠름 (런타임 비교 없이 직접 호출)|
|사용 대상|	일반 함수, static 함수, 생성자, 비가상 함수 등|
|대비 개념|	동적 바인딩 (Dynamic Binding) — virtual 함수 기반|