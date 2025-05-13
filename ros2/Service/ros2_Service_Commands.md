
# 🧮 ROS 2 : Service 명령어

---

## 📡 Service 명령어

| 명령어 | 설명 |
|--------|------|
| `ros2 service list` | 현재 활성화된 서비스 목록 출력 |
| `ros2 service type <service_name>` | 해당 서비스에서 사용하는 타입 확인 |
| `ros2 service call <service_name> <service_type> '{data}'` | 해당 서비스에 요청 메시지 전송 (클라이언트 역할) |
| `ros2 service find <service_type>` | 지정한 타입의 서비스를 제공하는 서버 검색 |
| `ros2 service info <service_name>` | 해당 서비스의 자세한 정보 출력 (서버, 클라이언트) |



- `ros2 service list` :

<img src="service list.png" alt="service list" width="400"/>

- `ros2 service type` :

<img src="service type.png" alt="service type" width="400"/>

- `ros2 service call` :

<img src="service call.png" alt="service call" width="400"/>

- `ros2 service find` :

<img src="service find.png" alt="service find" width="400"/>

---

## ✅ 예시

- `Type`: 해당 서비스에 대한 ROS2 인터페이스 유형
- `Service Clients`: 서비스에 요청을 보내는 클라이언트 노드 목록
- `Service Servers`: 요청을 처리하는 서버 노드 목록

---

## 🧩 Interface 명령어 (서비스 인터페이스 관련)

| 명령어 | 설명 |
|--------|------|
| ros2 interface list \ grep srv| 사용 가능한 모든 서비스 인터페이스 타입 출력 |
| `ros2 interface show <service_type>` | 특정 서비스 인터페이스의 Request/Response 구조 확인 |

---

### ✅ 예시

- `ros2 interface show` (서비스 구조) :

<img src="service show.png" alt="service show" width="400"/>

---
