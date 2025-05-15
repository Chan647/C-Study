# 🔐 C++ 클래스 : Getter & Setter

---

## ✅ 기본 개념

- Getter와 Setter는 클래스의 private 멤버 변수에 안전하게 접근하고 수정할 수 있도록 도와주는 함수

| 함수 | 역할 |예시|
|------|------|-----|
| Getter | 멤버 변수의 값을 **읽는 함수** | getName();|
| Setter | 멤버 변수의 값을 **설정하는 함수** |setName("홍길동");|

---

## 📌 Getter/Setter의 역할 
|목적|	이유|
|----|----|
|데이터를 보호|	외부에서 직접 접근하지 못하게 함 (private)|
|유효성 검사 가능|	잘못된 값 차단 (if (score >= 0 && score <= 100))|
|유지보수 쉬움|	인터페이스만 바꾸지 않으면 내부 구조는 자유롭게 변경 가능|

## ✅ 예제

```cpp
#include <iostream>
using namespace std;

class Person {
private:
    string name;
    int age;

public:
    // Setter
    void setName(string n) {
        name = n;
    }

    void setAge(int a) {
        age = a;
    }

    // Getter
    string getName() {
        return name;
    }

    int getAge() {
        return age;
    }
};

int main() {
    Person p;
    p.setName("홍길동");
    p.setAge(30);

    cout << "이름: " << p.getName() << endl;
    cout << "나이: " << p.getAge() << endl;

    return 0;
}
```

---

## ✅ 출력 결과

```
이름: 홍길동
나이: 30
```

---

## ✅  요약

| 항목 | 설명 |
|------|------|
| `private` 변수 | 외부에서 직접 접근 불가 |
| `getter()` | 변수 값 반환 |
| `setter()` | 변수 값 변경 |
| 장점 | 캡슐화, 무결성 유지, 제어된 접근 제공 |

---

