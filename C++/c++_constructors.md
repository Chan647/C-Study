# 🧱 C++ 생성자(Constructor)와 소멸자(Destructor)

---
## ✅ 생성자 (Constructor)란?

- 객체가 생성될 때 자동으로 호출되는 특수한 함수
- 클래스 이름과 동일하며, 반환형이 없다
- 객체 초기화 용도로 사용
- 오버로딩 가능 (매개변수 여러 개 사용 가능)

```cpp
class Animal {
public:
    Animal(string n) {
        name = n;
        cout << "생성자 호출: " << name << " 생성됨!" << endl;
    }
};
```

---

## ✅ 소멸자 (Destructor)란?

- 객체가 소멸될 때 자동으로 호출되는 함수
- `~클래스이름()` 형식
- 메모리 정리, 로그 출력 등에 사용
- 오버로딩 불가능

```cpp
class Animal {
public:
    ~Animal() {
        cout << "소멸자 호출: " << name << " 삭제됨!" << endl;
    }
};
```
---

## 📘 오버로딩(Overloading)이란?

- 오버로딩은 같은 이름의 함수나 연산자를 다양한 방식으로 재정의하는 것
- 함수 오버로딩은 매개변수의 개수나 타입이 다른 함수를 같은 이름으로 여러 개 정의하는 것
- 연산자 오버로딩은 기존 연산자(+, -, == 등)에 사용자 정의 동작을 부여하는 것

---

## 📘 오버라이딩(Overriding)이란?

- 오버라이딩은 부모 클래스에 정의된 가상 함수(virtual function)를 자식 클래스에서 재정의하는 것
- 함수 이름, 반환형, 매개변수까지 모두 부모와 동일해야 함
- 주로 다형성(polymorphism)을 구현하기 위해 사용됨

---

## 🔍 오버로딩(Overloading) vs 오버라이딩(Overriding) 차이

|구분|	오버로딩 (Overloading)|	오버라이딩 (Overriding)|
|------|-------|----------|
|적용 위치	|같은 클래스 내부|	상속 관계 (자식 클래스)|
|이름|	같음	|같음|
|매개변수|	다를 수 있음|	완전히 동일해야 함|
|목적|	함수 다양성 제공|	다형성 구현|
|키워드 필요?|	❌ 없음|	✅ virtual, override 사용 권장|
|실행 시점|	컴파일 타임	|런타임 (동적 바인딩)|

---

## ✅  예제: 생성자 + 소멸자

```cpp
#include <iostream>
using namespace std;

class Animal {
private:
    string name;

public:
    Animal(string n) {
        name = n;
        cout << "🐾 생성자 호출: " << name << " 생성됨!" << endl;
    }

    ~Animal() {
        cout << "💨 소멸자 호출: " << name << " 삭제됨!" << endl;
    }

    void speak() {
        cout << name << "가(이) 소리칩니다!" << endl;
    }
};

int main() {
    Animal a1("강아지");
    a1.speak();

    {
        Animal a2("고양이");
        a2.speak();
    }

    return 0;
}
```

---

## ✅ 생성자 오버로딩

- 클래스 내에 매개변수의 수나 타입이 다른 생성자를 여러 개 정의하는 것
- 객체를 생성할 때 다양한 초기화 방법을 제공
- C++은 자동으로 매칭되는 생성자를 선택하여 호출함

---

## ✅ 예제 

```cpp
#include <iostream>
using namespace std;

class Book {
private:
    string title;
    int price;

public:
    
    Book() {
        title = "제목 없음";
        price = 0;
        cout << "[기본 생성자 호출]" << endl;
    }

    Book(string t, int p) {
        title = t;
        price = p;
        cout << "[매개변수 생성자 호출]" << endl;
    }

    void printInfo() {
        cout << "제목: " << title << ", 가격: " << price << "원" << endl;
    }
};

int main() {
    Book b1;
    b1.printInfo();

    Book b2("C++ 마스터 클래스", 35000);
    b2.printInfo();

    return 0;
}
```

---

## 🧠 요약 

| 항목 | 설명 |
|------|------|
| 생성자 | 객체 생성 시 호출, 오버로딩 가능 |
| 소멸자 | 객체 소멸 시 호출, 1개만 존재 |
| 기본 생성자 | 매개변수 없음 |
| 매개변수 생성자 | 인자를 통해 초기화 |
| 오버로딩 | 생성자 여러 개 정의 가능 |

---
