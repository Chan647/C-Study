
# 📚 ROS 2 서비스(Service) : 클라이언트(Client)

---

## 🧨 실습 목표

- 커스텀 서비스 인터페이스 작성
- Gazebo 상에서 서비스 요청을 보내 Tiago 로봇을 전진하도록 제어

---

## 🎀 클라이언트의 역할

- 서비스 서버로 전진 요청을 보내고, 결과를 수신
- 사용자로부터 입력받거나 코드 내 설정된 거리만큼 로봇을 이동하도록 요청

---

## 🛠️  커스텀 서비스 인터페이스 정의

- srv/MoveForward.srv

```bash
float64 distance  # 이동 거리 (meters)
---
bool success      # 성공 여부
```

## 🛠️package.xml과 CMakeLists.txt 의존성 추가

```xml

<build_depend>rosidl_default_generators</build_depend>
<exec_depend>rosidl_default_runtime</exec_depend>

```

```cmake
Copy
Edit
rosidl_generate_interfaces(${PROJECT_NAME} 
  "srv/MoveForward.srv"
)
```
- 커스텀 인터페이스를 생성하기 때문에 package.xml도 수정이 필요

---

## 📂 프로젝트 구조
```
tiago_service_examples/
├── CMakeLists.txt
├── package.xml
├── srv/
│   └── MoveForward.srv
└── src/
    └── move_forward_client.cpp
```

---

## 📡 예제 코드

```cpp
#include "rclcpp/rclcpp.hpp"
#include "tiago_service_examples/srv/move_forward.hpp"

using namespace std::chrono_literals;

int main(int argc, char **argv) {
    rclcpp::init(argc, argv);

    auto node = rclcpp::Node::make_shared("move_forward_client");
    auto client = node->create_client<tiago_service_examples::srv::MoveForward>("move_forward");

    while (!client->wait_for_service(1s)) {
        RCLCPP_INFO(node->get_logger(), "Waiting for service...");
    }

    auto request = std::make_shared<tiago_service_examples::srv::MoveForward::Request>();
    request->distance = 1.0;  // 1 meter 이동

    auto result = client->async_send_request(request);
    if (rclcpp::spin_until_future_complete(node, result) == rclcpp::FutureReturnCode::SUCCESS) {
        RCLCPP_INFO(node->get_logger(), "Service Call Success: %s", result.get()->success ? "true" : "false");
    } else {
        RCLCPP_ERROR(node->get_logger(), "Service Call Failed.");
    }

    rclcpp::shutdown();
    return 0;
}
```

---

## ⚙️ CMakeLists.txt 수정

```bash
add_executable(move_forward_client src/move_forward_client.cpp)
ament_target_dependencies(move_forward_client rclcpp tiago_service_examples)
```
---

## 🚀 빌드 및 실행 

```bash
cd ~/ros2_ws
colcon build --packages-select tiago_service_examples
source install/setup.bash


ros2 run tiago_service_examples move_forward_client
```
출력 결과 : 

<img src="service client.png" alt="service client" width="400"/>

- 클라이언트는 Service Call Success : True 메시지 출력
