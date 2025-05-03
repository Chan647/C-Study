# 🧭 C++ this 포인터 & static 키워드 

---

## ✅ this 포인터란?

- 클래스 내부에서 자기 자신을 가리키는 포인터
- 주로 멤버변수와 매개변수의 이름이 겹칠 때나, 자기 자신을 리턴할 때 사용

```cpp
class Person {
private:
    string name;

public:
    Person(string name) {
        this->name = name;  // 멤버 변수와 매개변수를 구분
    }

    Person* getThis() {
        return this;
    }

    void show() {
        cout << "이름: " << name << endl;
    }
};
```

---

## ✅ static 변수와 함수

- `static`으로 선언된 멤버는 클래스 전체에 공유되는 변수/함수
- 객체 없이도 사용할 수 있음 (`클래스명::함수()`)

```cpp
class Counter {
private:
    static int count;

public:
    Counter() {
        count++;
        cout << "객체 생성됨. 총 객체 수: " << count << endl;
    }

    static int getCount() {
        return count;
    }
};

// static 멤버 초기화
int Counter::count = 0;
```

```cpp
int main() {
    Counter c1;
    Counter c2;

    cout << "현재까지 생성된 객체 수: " << Counter::getCount() << endl;
    return 0;
}
```

---

## ✅ 실행 결과

```
객체 생성됨. 총 객체 수: 1
객체 생성됨. 총 객체 수: 2
현재까지 생성된 객체 수: 2
```

---

## ✅ static 키워드의 특징
|항목|	설명|
|---|---|
|공유성|	모든 객체가 같은 값을 공유|
|클래스 소속|	객체 없이도 ClassName::member로 사용 가능|
|초기화 위치	|클래스 정의 안이 아니라 밖에서 초기화해야 함|
|주 용도|	객체 수 세기, 공통 설정값 저장, 전역성 제한 등|

## 🧠  요약

| 개념 | 설명 | 사용 예 |
|------|------|---------|
| this | 현재 객체를 가리키는 포인터 | this->변수 |
| static 변수 | 클래스 전체에서 공유됨 | 객체 수, 공통값 |
| static 함수 | 객체 없이 호출 가능 | 클래스명::함수() |

---

