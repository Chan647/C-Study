# 🧮 ROS 2 : Action 명령어

---

## 🚀 Action 명령어

| 명령어 | 설명 |
|--------|------|
| `ros2 action list` | 현재 사용 가능한 액션 서버 목록 출력 |
| `ros2 action info <action_name>` | 특정 액션 서버에 대한 상세 정보 출력 (Goal, Result, Feedback) |
| `ros2 action send_goal <action_name> <action_type> '{goal_data}'` | 액션 서버에 목표(Goal) 요청 보내기 |
| `ros2 action show <action_type>` | 특정 액션 인터페이스 타입의 Goal, Result, Feedback 구조 보기 |
| `ros2 action cancel <goal_id>` | 특정 Goal ID에 대한 액션 요청 취소 |

---

- `ros2 action list` :

<img src="action list.png" alt="action list" width="400"/>

- `ros2 action info` :

<img src="action info.png" alt="action info" width="400"/>

- `ros2 action info -t` :

<img src="action info -t.png" alt="action info -t" width="400"/>

- `ros2 action send_goal` :

<img src="action goal.png" alt="action send goal" width="400"/>

- `ros2 action show` :

<img src="action show.png" alt="action show" width="400"/>


---

## ✅ 예시

- Type: 액션 인터페이스 유형 (예: `action_tutorials_interfaces/action/Fibonacci`)  
- Goal ID: 특정 Goal 요청에 대한 고유 식별자  
- Status: Goal 처리 상태 (예: accepted, executing, succeeded, canceled)  

---

## 📂 추가 명령어

| 명령어 | 설명 |
|--------|------|
| `ros2 action status <action_name>` | 현재 액션 서버의 Goal 상태 목록 출력 |
| `ros2 action list -t` | 액션 타입 목록 출력 (사용 가능한 액션 인터페이스 유형) |

---

