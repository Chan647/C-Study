# 🧱 C++ 클래스 : 접근 제어자 (Access Specifiers) 


---
## 📘 접근제어자(Access Specifiers)란?

- 접근 제어자는 클래스의 멤버(변수와 함수)에 대한 접근 범위를 지정하는 키워드
- public, private, protected의 3가지가 있으며, 각기 다른 접근 수준을 가짐
- 이를 통해 캡슐화와 정보 은닉을 구현하여 객체 지향 프로그래밍의 안정성을 높임

---

## ✅ 접근 제어자 종류

| 키워드 | 의미 | 접근 가능 위치 | 사용 예 |
|--------|------|----------------|----------|
| `public` | 누구나 접근 가능 | 클래스 내부, 외부, 자식 클래스 | 외부 인터페이스 |
| `private` | 클래스 내부에서만 접근 가능 | 클래스 내부만 | 민감한 데이터 |
| `protected` | 클래스 내부 + 자식 클래스에서만 접근 가능 | 부모 클래스, 자식 클래스 | 상속 구조에서 내부 공유 |

---

## ✅ 예제

```cpp
class Sample {
public:
    int a;          // 외부 접근 가능
protected:
    int b;          // 자식 클래스에서 접근 가능
private:
    int c;          // 클래스 내부에서만 접근 가능
};

Sample s;
s.a = 1;   // ✅ OK
s.b = 2;   // ❌ 오류 (protected)
s.c = 3;   // ❌ 오류 (private)
```

---

## ✅ 예제

### 🔓 public
```cpp
class Car {
public:
    void drive();  // 외부에서 호출 가능
};
```

### 🔐 private
```cpp
class Car {
private:
    int speed;  // 외부에서 직접 접근 불가
public:
    void setSpeed(int s) { speed = s; }  // public 인터페이스로 우회 접근
};
```

### 🛡️ protected
```cpp
class Animal {
protected:
    string name;
};

class Dog : public Animal {
public:
    void bark() {
        cout << name << "가 짖습니다.";  // ✅ 가능
    }
};
```

---

## ✅ 접근 가능 요약표

| 접근 대상 | 클래스 내부 | 자식 클래스 | 외부 객체 |
|------------|---------------|----------------|----------------|
| `public`    | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ❌ |
| `private`   | ✅ | ❌ | ❌ |

---

## ✅ 상황별 접근 제어자 사용

| 상황 |  접근 제어자 | 이유 |
|------|------------------|------|
| 외부에 노출할 함수 | `public` | 사용자 인터페이스로 제공 |
| 내부 전용 변수 | `private` | 직접 수정 방지, 안전성 |
| 상속에서 내부 공유 | `protected` | 외부 차단 + 자식 공유 가능 |

---