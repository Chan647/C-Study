# 🧠 C++ : 스마트 포인터 (Smart Pointer)

---

## ✅ 기본 개념

- 스마트 포인터는 C++11부터 도입된 자동 메모리 관리 도구
- `new` / `delete`를 직접 사용하지 않고도 메모리 누수 없이 객체를 안전하게 관리할 수 있음
-  unique_ptr, shared_ptr, weak_ptr 등이 있으며, 메모리 누수 방지에 유용함

| 종류 | 설명 |
|------|------|
| `unique_ptr` | 하나의 소유자만 가짐. 복사 불가. 이동만 가능 |
| `shared_ptr` | 여러 포인터가 같은 객체를 공유함 (참조 카운트 사용) |
| `weak_ptr` | `shared_ptr`와 함께 쓰이며 참조 카운트를 증가시키지 않음 |

---

## ✅ unique_ptr 예제

```cpp
#include <iostream>
#include <memory>
using namespace std;

class Dog {
public:
    Dog() { cout << "강아지 생성됨" << endl; }
    ~Dog() { cout << "강아지 소멸됨" << endl; }
    void bark() { cout << "멍멍!" << endl; }
};

int main() {
    unique_ptr<Dog> d1 = make_unique<Dog>();
    d1->bark();

    // unique_ptr<Dog> d2 = d1;     // ❌ 복사 불가
    // unique_ptr<Dog> d2 = move(d1); // ✅ 이동 가능

    return 0;
}
```

---

## ✅ shared_ptr 예제

```cpp
#include <iostream>
#include <memory>
using namespace std;

int main() {
    shared_ptr<Dog> d1 = make_shared<Dog>();
    shared_ptr<Dog> d2 = d1;  // ✅ 참조 카운트 증가

    d1->bark();
    cout << "참조 수: " << d1.use_count() << endl;
    // 출력 : 2
}
```

---

## ✅  요약

| 항목 | unique_ptr | shared_ptr |
|------|------------|------------|
| 소유권 | 단독 | 공유 가능 |
| 복사 | ❌ 불가 | ✅ 가능 |
| 이동 | ✅ 가능 | ✅ 가능 |
| 참조 수 관리 | ❌ 없음 | ✅ 있음 (`use_count()`) |
| 사용 목적 | 단독 자원 관리 | 공유 자원 관리 |

---

## ✅ 장점

- 메모리 누수 방지 (`delete`를 안 써도 됨)
- 코드 안정성 향상 
- 예외 발생 시에도 자동 소멸 보장

---

