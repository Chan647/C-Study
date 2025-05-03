# 🧬  C++ 클래스: 상속 (Inheritance)

---

## ✅ 상속이란?

- 기존 클래스를 바탕으로 새로운 클래스를 정의하는 방식
- 코드 재사용성과 확장성 향상
- `is-a` 관계에서 사용

```cpp
class 자식클래스 : public 부모클래스
```

---

## ✅ 예제 

```cpp
#include <iostream>
using namespace std;

// 부모 클래스
class Person {
protected:
    string name;

public:
    Person(string n) {
        name = n;
        cout << "Person 생성자 호출" << endl;
    }

    void introduce() {
        cout << "안녕하세요, 제 이름은 " << name << "입니다." << endl;
    }
};

// 자식 클래스
class Student : public Person {
private:
    int studentID;

public:
    Student(string n, int id) : Person(n) {
        studentID = id;
        cout << "Student 생성자 호출" << endl;
    }

    void study() {
        cout << name << "이(가) 공부하고 있습니다. 학번: " << studentID << endl;
    }
};

int main() {
    Student s("홍길동", 202412);
    s.introduce();  
    s.study();      
    return 0;
}
```

---

## ✅ 출력 결과

```
Person 생성자 호출
Student 생성자 호출
안녕하세요, 제 이름은 홍길동입니다.
홍길동이(가) 공부하고 있습니다. 학번: 202412
```

---

## 🧠 요약

| 항목 | 설명 |
|------|------|
| `: public 부모클래스` | 부모 클래스 상속 선언 |
| `protected` | 자식 클래스에서 접근 가능 |
| 부모 생성자 호출 | `: 부모클래스(매개변수)` 사용 |
| 상속된 함수 | 자식 클래스에서 그대로 사용 가능 |
| 자식 함수 추가 | 기능 확장 가능 |



