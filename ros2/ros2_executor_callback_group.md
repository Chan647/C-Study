
# 📚 ROS 2 : Executor & Callback Group 

---

## 🧩 Executor란?
 
- ROS 2에서 노드의 콜백을 실행하는 엔진 역할

---

## 📡 주요 역할:  

  - 콜백 큐 관리  
  - 콜백 함수 실행 (예: 토픽 수신, 서비스 요청 처리 등)  
  - 노드들의 이벤트 루프를 관리

---

## ✨ 콜백(callback)이란?

- 특정 이벤트나 조건이 발생했을 때 자동으로 호출되는 함수
- 토픽 수신, 서비스 요청 처리 등에서 콜백 함수 활용
- 어떤 조건이 만족 될 때, 자동으로 호출
---
## 📦  종류:  

- Single-ThreadedExecutor  
  - 한 번에 하나의 콜백만 실행
  - 순차적으로 작업을 처리하므로 동기화 이슈가 없음
  - 코드가 단순하고 디버깅이 용이
  - 콜백 처리 속도가 느려질 수 있어 실시간성이 낮음
   
- Multi-ThreadedExecutor 
  - 여러 콜백을 병렬로 동시에 실행할 수 있음
  - 처리 속도가 빨라 고성능 작업에 적합
  - 스레드 간 동기화 문제와 경쟁 상태를 주의해야 함
  - 복잡한 코드 구조와 디버깅 난이도가 높음

---

## ✅ 사용 예시

```cpp
rclcpp::executors::SingleThreadedExecutor executor;
executor.add_node(node);
executor.spin();
```

---

## 🧩 Callback Group 이란?

- 콜백 함수들을 논리적으로 묶어 실행 방식을 제어하는 기능
- 그룹 내 콜백의 동시 실행 여부를 설정할 수 있음
- 주로 멀티스레드 환경에서 동시 실행을 제어하고 리소스 충돌을 방지하는 데 사용됨
---
## 📡 주요 역할  

- 콜백 동시 실행 여부 설정 (Mutually Exclusive vs Reentrant)  
- Executor의 스케줄링 대상 관리  
---

## 📦 종류
- MutuallyExclusiveCallbackGroup
  - 그룹 내 콜백 함수들은 한 번에 하나만 실행됨
  - 동시 실행을 막아 리소스 충돌을 방지
  - 센서 데이터 처리 등 순차적 처리가 필요한 경우에 적합
  
- ReentrantCallbackGroup
  - 그룹 내 콜백 함수들이 동시에 실행될 수 있음
  - 멀티스레드 환경에서 병렬 처리를 허용
  - 리소스 충돌 관리가 필요하지만 처리 속도가 향상됨

---
## ✅ 사용 예시

```cpp
auto callback_group = node->create_callback_group(
    rclcpp::CallbackGroupType::MutuallyExclusive
);
```

---

## ✅ Executor & Callback Group 관계

| 항목 | 설명 |
|------|------|
| Executor | 콜백 큐를 관리하고 실행 |
| Callback Group | 콜백의 실행 방식 정의 (독점/병렬) |
| 연결 | Executor가 Callback Group 내 콜백을 실행 |

- 실행 흐름  
  1. 노드에서 콜백 그룹 생성  
  2. Executor가 노드를 스핀 (spin)  
  3. Callback Group 설정에 따라 콜백 실행 방식 결정  

---

