# 🧮 ROS 2 : Topic & Interface 명령어



---

## 📡 Topic  명령어

| 명령어 | 설명 |
|--------|------|
| `ros2 topic list` | 현재 활성화된 토픽 목록 출력 |
| `ros2 topic echo <topic_name>` | 특정 토픽의 메시지를 실시간으로 출력 |
| `ros2 topic pub <topic_name> <msg_type> '{data: 값}'` | 해당 토픽에 메시지를 발행 (퍼블리셔 역할) |
| `ros2 topic info <topic_name>` | 해당 토픽에 연결된 퍼블리셔와 서브스크라이버 정보 출력 |
| `ros2 topic type <topic_name>` | 해당 토픽에서 사용하는 메시지 타입 확인 |
| `ros2 topic hz <topic_name>` | 메시지가 발행되는 주기 (Hz) 측정 |

---
- ros2 topic list :

<img src="topic list.png" alt="topic list" width="400"/>

- ros2 topic echo :

<img src="topic echo.png" alt="topic echo" width="400"/>

- ros2 topic info :

<img src="topic info.png" alt="topic info" width="400"/>

---

## ✅ 예시

- `Type`: 해당 토픽에 대한 ROS2 인터페이스 유형
- `Publisher count`: 토픽에 연결된 활성 Publisher의 수
- `Subscription count`: 토픽에 연결된 활성 Subscription 수

---


## 🧩 Interface 명령어

| 명령어 | 설명 |
|--------|------|
| `ros2 interface list` | 사용 가능한 모든 interface(msg, srv, action) 타입 출력 |
| `ros2 interface show <interface_name>` | 특정 메시지 타입의 필드 구조 확인 |
| `ros2 interface packages` | 인터페이스를 제공하는 패키지 목록 보기 |
| `ros2 interface proto <type>` |인터페이스의 프로토타입을 보여주는 명령어|

---

### ✅ 예시

- ros2 interface list :

<img src="interface list.png" alt="interface list" width="400"/>

- ros2 interface show :

<img src="interface show.png" alt="interface show" width="400"/>

---