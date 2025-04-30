#  자료구조: 덱(Deque)

## 📂 덱(Deque)이란?

- 덱(Deque)은 Double-Ended Queue 의 약자 
- 앞과 뒤 두 방향에서 모두 삽입과 삭제가 가능한 자료구조

### ✅ 주요 특징

- 스택처럼도, 큐처럼도 활용 가능
- 양방향 삽입/삭제가 필요할 때 사용
- 슬라이딩 윈도우, 캐시 구현 등에 유용

## ⏱️ 시간 복잡도

- (push_front)	O(1)
- (push_back)	O(1)
- (pop_front)	O(1)
- (pop_back)	O(1)
- (at(index))   O(1)

### 🔧 주요 메서드 

- push_front() 앞에 삽입 
- push_back()  뒤에 삽입 
- pop_front()  앞의 요소 제거 
- pop_back()   뒤의 요소 제거 
- front()      맨 앞에 있는 요소 반환
- back()       맨 뒤에 있는 요소 반환 
- empty()      덱이 비어있는지 여부 확인 
- size()       요소 개수 반환 

### 📎 예시 

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main() {
    deque<int> d;

    d.push_back(10);    
    d.push_front(20);  
    d.push_back(30);    

    cout << "Front: " << d.front() << endl;
    cout << "Back: " << d.back() << endl;  

    d.pop_front();
    cout << "Front after pop_front: " << d.front() << endl; 

    d.pop_back();
    cout << "Back after pop_back: " << d.back() << endl;

    return 0;
}
```

### 🔍 덱의 사용 

- 슬라이딩 윈도우 최대값 구하기
- 양방향 삽입/삭제가 필요한 큐 구현