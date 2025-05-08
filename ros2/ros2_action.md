# 🌐 ROS 2 : 액션(Action) 

---

## 📘 액션(Action)이란?

- 오래 걸리는 작업(Long-running task)을 처리할 때 사용하는 비동기 통신 메커니즘
- Service처럼 요청(Request)과 응답(Response)을 처리하지만, 중간 피드백(Feedback)을 주고받을 수 있다는 것이 가장 큰 특징
- 클라이언트와 서버로 구성
- Goal, Feedback, Result 세 가지 메세지 유형을 사용

---

## ⚙️ 작동 원리

- 메세지 유형

1. Goal (목표): 클라이언트가 서버에 보내는 작업 요청
2. Feedback (피드백): 서버가 클라이언트에게 중간 결과를 전달
3. Result (결과): 작업이 끝났을 때 클라이언트에게 최종 결과를 전달


---

### 🧩 내부 통신 구조

- Goal 요청: 클라이언트 → 서버 (`SendGoal` 서비스 사용)
- Feedback 수신: 서버 → 클라이언트 (`/feedback` 토픽 사용)
- Result 수신: 클라이언트 → 서버 (`GetResult` 서비스 사용)
- Cancel 요청: 작업 중단 가능 (`CancelGoal` 서비스 사용)

---

## 🌟  특징

| 항목 | 설명 |
|------|------|
| 통신 방식 | 비동기 (async), 피드백 가능 |
| 구성 요소 | Goal, Feedback, Result |
| 사용 상황 | 경로 생성, 로봇 팔 제어, 이미지 처리 등 시간이 오래 걸리는 작업 |
| 내부 구현 | Topic + Service 조합 |
| 취소 지원 | 작업 취소 가능 (`CancelGoal`) |

---

## 🧾 인터페이스 타입 : Action

### ✅ 예시

```action
int32 order                 # Goal (요청할 작업)
---
int32[] sequence            # Result (최종 결과)
---
int32[] partial_sequence    # Feedback (중간 상태)
```

- `---` 으로 세 부분을 구분: Goal / Result / Feedback

---

## ✅ 주요 용도

- 로봇 제어 작업	
- 경로 계획 (Navigation)	
- 이미지/센서 처리 요청	
- 시뮬레이션/조작 요청	
- 미션 실행 시스템