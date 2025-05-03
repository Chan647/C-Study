
# 🌟 C++ : STL (Standard Template Library) 


---

## ✅ STL이란?

-  C++에서 제공하는 표준화된 자료구조와 알고리즘 라이브러리 
- 템플릿 기반으로 구현되어 다양한 데이터 타입에 대해 재사용 가능한 코드 작성을 도움

---

## ✅ STL 주요 구성요소

| 구성 요소 | 설명 | 예시 |
|-----------|------|------|
| **컨테이너 (Container)** | 데이터를 저장하는 자료구조 | `vector`, `list`, `map`, `set` |
| **반복자 (Iterator)** | 컨테이너 원소를 순회하는 포인터처럼 동작하는 객체 | `begin()`, `end()` |
| **알고리즘 (Algorithm)** | 정렬, 탐색 등 컨테이너를 다루는 함수 | `sort()`, `find()`, `count()` |
| **함수 객체 (Function Object)** | 함수처럼 동작하는 클래스/객체 | `greater<int>()` |
| **어댑터 (Adapter)** | 기존 컨테이너를 변형해서 사용하는 도구 | `stack`, `queue`, `priority_queue` |

---

## ✅ 주요 컨테이너 종류

| 컨테이너 | 설명 | 특징 |
|----------|------|------|
| `vector` | 동적 배열 | 인덱스 접근, 추가 빠름 |
| `list` | 이중 연결 리스트 | 삽입/삭제 빠름, 인덱스 없음 |
| `deque` | 양방향 큐 | 앞뒤 삽입/삭제 용이 |
| `set` | 중복 없는 정렬된 집합 | 자동 정렬 |
| `map` | 키-값 쌍의 정렬된 연관 배열 | 키 기준 정렬 |
| `unordered_map` | 해시 기반 키-값 | 빠른 탐색, 정렬 없음 |
| `stack` | LIFO 구조 | top(), push(), pop() |
| `queue` | FIFO 구조 | front(), push(), pop() |

---

## ✅ STL 사용 시 필요한 헤더

| 컨테이너 | 헤더 |
|----------|------|
| `vector` | `<vector>` |
| `list` | `<list>` |
| `map`, `set` | `<map>`, `<set>` |
| `unordered_map`, `unordered_set` | `<unordered_map>`, `<unordered_set>` |
| `stack`, `queue` | `<stack>`, `<queue>` |

---

## 🧠 STL  요약

| 컨테이너 | 구조 | 특징 |
|----------|------|------|
| `vector` | 동적 배열 | 빠른 인덱스, 추가 쉬움 |
| `list` | 이중 연결 리스트 | 삽입/삭제 빠름 |
| `map` | 정렬된 키-값 | 키 기준 정렬 |
| `unordered_map` | 해시 테이블 | 매우 빠름, 정렬 없음 |
| `set` | 정렬된 집합 | 중복 제거, 자동 정렬 |
| `stack` | LIFO | top/push/pop |
| `queue` | FIFO | front/push/pop |

---


## ✅ STL의 장점

- 빠르고 안정적인 표준 구현 제공
- 템플릿 기반으로 다양한 자료형에 재사용 가능
- 자료구조 + 알고리즘 결합으로 생산성 향상
- 컨테이너 간 인터페이스 통일성 제공

---

