# 🚀 C++ 클래스


## 📘 클래스(Class)란??

- C++ 클래스는 데이터(멤버 변수)와 기능(멤버 함수)을 하나로 묶은 사용자 정의 자료형
- 현실 세계의 개념을 코드로 모델링하는 설계도 역할을 함.
- 클래스를 기반으로 만든 구체적인 실체를 객체(Object)라고 함

## ✅ 클래스 핵심 구성 요소

| 항목 | 설명 |
|------|------|
| 클래스 정의 | 객체의 설계도 |
| 생성자 / 소멸자 | 객체 생성과 파괴 시 자동 호출되는 함수 |
| 접근 제어자 | 멤버의 접근 범위 제어 (`public`, `private`, `protected`) |
| `this` 포인터 | 현재 객체 자신의 주소를 가리킴 |
| `static` 멤버 | 클래스 전체에서 공유되는 변수/함수 |

---

## ✅ 클래스  개념

| 항목 | 설명 |
|------|------|
| 상속 (Inheritance) | 기존 클래스를 기반으로 새로운 클래스 정의 |
| 다형성 (Polymorphism) | 부모 클래스 포인터로 자식 클래스의 오버라이딩 함수 호출 |
| 가상 함수 (`virtual`) | 런타임에 호출될 함수 결정 (동적 바인딩) |
| 추상 클래스 | 순수 가상 함수를 포함하며, 직접 객체 생성 불가 |
| 연산자 오버로딩 | 클래스 간 연산자(`+`, `==` 등)를 사용자 정의 가능 |


## ✅ 템플릿

| 항목 | 설명 |
|------|------|
| 함수 템플릿 | 자료형에 관계없이 같은 함수 동작을 재사용 |
| 클래스 템플릿 | 다양한 타입을 처리하는 일반화된 클래스 |

---


## ✅ 1. 클래스(Class) 기본 구조

- 사용자 정의 자료형으로, 데이터와 관련 기능을 묶을 수 있음.
- 클래스 구성 요소:
  - **멤버 변수** (데이터)
  - **멤버 함수** (동작)
  - **접근 제어자**: public / private

```cpp
class Car {
private:
    string brand;
    int speed;

public:
    Car(string b, int s) {
        brand = b;
        speed = s;
    }

    void printInfo() {
        cout << "브랜드: " << brand << ", 속도: " << speed << endl;
    }

    void accelerate(int value) {
        speed += value;
    }
};
```

---

## ✅ 2. 접근 제어자 (public vs private)

| 키워드 | 설명 | 접근 가능 위치 |
|--------|------|----------------|
| `public` | 외부에서 접근 가능 | 어디서든 접근 가능 |
| `private` | 외부에서 접근 불가 | 클래스 내부에서만 사용 |

- 원칙: **데이터는 private, 함수는 public**

---

## ✅ 3. Getter / Setter

- `private` 멤버 변수에 안전하게 접근하기 위한 `public` 함수

```cpp
class Person {
private:
    string name;
    int age;

public:
    void setName(string n) { name = n; }
    void setAge(int a) {
        if (a >= 0) age = a;
    }

    string getName() { return name; }
    int getAge() { return age; }
};
```

### 장점:
- 데이터 보호 (캡슐화)
- 유효성 검사
- 유지보수 편리

---

## ✅ 4. 캡슐화 (Encapsulation)

- 객체 내부 구현을 숨기고, 인터페이스만 외부에 노출하는 것
- 목적: 보안성, 유지보수성, 안정성 향상

---


