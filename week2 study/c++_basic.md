
# 📘 C++ 기초 문법 정리 (1단계)

본 문서는 C++ 초보자가 반드시 알아야 할 10가지 기초 문법 개념을 정의합니다.

---

## 1. 자료형 (Data Types)

데이터를 저장할 때 사용하는 형태로, 메모리 공간과 표현 범위가 다릅니다.

- `int`: 정수형 (예: 1, -5)
- `float`: 실수형 (예: 3.14)
- `double`: 더 정밀한 실수형
- `char`: 문자형 (예: 'A')
- `bool`: 논리형 (true, false)

```cpp
int age = 25;
float pi = 3.14;
bool isOpen = true;
```

---

## 2. 변수 (Variable)

데이터를 저장하기 위한 이름이 붙은 메모리 공간입니다.

```cpp
int x = 10;
char grade = 'A';
```

---

## 3. 입출력 (Input/Output)

사용자로부터 값을 입력받거나 결과를 출력합니다.

```cpp
int a;
cin >> a;                     // 입력
cout << "입력한 값: " << a;   // 출력
```

---

## 4. 조건문 (Conditional Statement)

특정 조건에 따라 실행 흐름을 제어합니다.

```cpp
if (a > b) {
    cout << "a가 b보다 큽니다.";
} else {
    cout << "a가 b보다 작거나 같습니다.";
}
```

---

## 5. 반복문 (Loop)

특정 코드를 반복해서 실행합니다.

```cpp
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}

while (x > 0) {
    x--;
}
```

---

## 6. 함수 (Function)

코드의 재사용성과 구조화를 위해 사용합니다.

```cpp
int add(int a, int b) {
    return a + b;
}
```

---

## 7. 포인터 (Pointer)

변수의 주소를 저장하는 변수입니다.

```cpp
int x = 10;
int* ptr = &x;
```

---

## 8. 참조자 (Reference)

변수의 또 다른 이름(별칭)을 정의합니다.

```cpp
int a = 5;
int& ref = a;
ref = 10;  // a도 10이 됨
```

---

## 9. 구조체 (struct)

여러 데이터를 하나의 구조로 묶는 사용자 정의 자료형입니다.

```cpp
struct Person {
    string name;
    int age;
};

Person p1 = {"Alice", 30};
```

---

## 10. 열거형 (enum)

관련 있는 상수들의 집합을 이름 붙여 표현할 수 있게 해줍니다.

```cpp
enum Color { RED, GREEN, BLUE };

Color c = RED;
```

---
