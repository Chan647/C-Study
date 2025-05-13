# 📚 ROS 2 : Interface & Topic



---

## 🧩  Interface 란?

- 노드 간 통신에 사용되는 데이터 구조
- 3가지 유형이 있으며, 모두 `.msg`, `.srv`, `.action` 파일로 정의됨

---

### 📦 Interface의 종류

| 유형 | 설명 | 예시 |
|------|------|------|
| `msg` | 단방향 메시지 (주로 Topic에서 사용) | `std_msgs/msg/String.msg` |
| `srv` | 요청-응답 메시지, 양방향 통신에 사용 (Service에서 사용) | `example_interfaces/srv/AddTwoInts.srv` |
| `action` | 진행 상태가 있는 비동기 작업 메시지, 양방향 통신에 사용 | `action_msgs/action/Fibonacci.action` |

---

## 📡 Topic 이란?

- 노드 간 메시지를 비동기적으로 주고받기 위한 통신 채널
- Publisher-Subscriber 모델 기반
  - Publisher가 메시지를 Topic에 발행
  - Subscriber가 해당 Topic을 구독하여 메시지를 수신

---

### 특징

| 항목 | 설명 |
|------|------|
| 통신 방식 | 단방향 (Publisher → Subscriber) |
| 메시지 타입 | Interface 중 `.msg` 사용 |
| 특징 | 비동기 통신 , 다대다 통신, 고유한 메세지 타입 |

---

### 예시 흐름

1. `talker_node` → `/chatter` → 메시지 발행
2. `listener_node` ← `/chatter` ← 메시지 수신

---

## ✅ 요약

| 개념 | 역할 | 주 사용처 |
|------|------|-----------|
| Interface (`.msg`) | 통신할 데이터의 구조 정의 | Topic, Service, Action |
| Topic | 메시지를 주고받는 통신 채널 | Publisher/Subscriber 노드 간 통신 |