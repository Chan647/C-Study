
# 📚 ROS 2 : Global Localization 

---

## 📣 Global Localization이란?

- 로봇의 위치를 전혀 모를 때 지도 전체에 입자를 무작위로 분포시켜 위치를 탐색하는 방법
- AMCL Localization 실패 시, 또는 로봇 전원 재시작 후 위치 정보를 모를 때 주로 사용

---
## 🧨 Global Localization 실습

- 터미널에서 Global Localization 실행
- 프로그램을 통한 Global Localization

---
## 📥 환경 준비

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

- Navigation2 실행 :

```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py \
    use_sim_time:=true map:=/home/chan/map/my_map.yaml
```

---

## 📌  터미널에서 Global Localization 실행

```bash
ros2 service call /reinitialize_global_localization std_srvs/srv/Empty
```

- 호출 즉시, Particle Cloud가 지도 전체에 퍼짐  
- 로봇이 센서 데이터를 수집하며 위치를 점차 수렴
- teleop_twist_keyboard 이를 사용해 수동 조작

- 출력 결과 :

<img src="global localization.png" alt="global localization" width="400"/>

- teleop_twist_keyboard 를 이용하여 조작
- 초기 위치 추정 실패함

## 📌 프로그램 상에서 Global Localization 실행

### 📁 패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake global_localization_client --dependencies rclcpp std_srvs
```
---
### 📄 예제 코드


```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_srvs/srv/empty.hpp"  

int main(int argc, char **argv)
{
    rclcpp::init(argc, argv);
    auto node = rclcpp::Node::make_shared("global_localization_client");

    // 서비스 클라이언트 생성
    auto client = node->create_client<std_srvs::srv::Empty>("/reinitialize_global_localization");

    // 서비스가 제공될 때까지 대기
    if (!client->wait_for_service(std::chrono::seconds(5))) {
        RCLCPP_ERROR(node->get_logger(), "서비스 /reinitialize_global_localization 를 찾을 수 없습니다.");
        return 1;
    }

    // 빈 요청 생성 (Empty 서비스)
    auto request = std::make_shared<std_srvs::srv::Empty::Request>();

    // 서비스 호출
    auto result = client->async_send_request(request);

    // 결과 대기
    if (rclcpp::spin_until_future_complete(node, result) == rclcpp::FutureReturnCode::SUCCESS) {
        RCLCPP_INFO(node->get_logger(), "✅ Global Localization 요청 성공!");
    } else {
        RCLCPP_ERROR(node->get_logger(), "❌ Global Localization 요청 실패!");
    }

    rclcpp::shutdown();
    return 0;
}
```
---

### ⚙️ CMakeLists.txt 수정

```cmake

add_executable(global_localization_client src/global_localization_client.cpp)
ament_target_dependencies(global_localization_client rclcpp std_srvs)

install(TARGETS
  global_localization_client
  DESTINATION lib/${PROJECT_NAME}
)

```

---

### 📂 프로젝트 구조
```
global_localization_client/
├── CMakeLists.txt
├── package.xml
└── src/
    └── global_localization_client.cpp
```

---
## 🚀  빌드 및 실행


```bash
cd ~/ros2_ws
colcon build --packages-select global_localization_client
source install/setup.bash

ros2 run global_localization_client global_localization_client 

```
<img src="global localization command.png" alt="global localization command" width="400"/>

- teleop_twist_keyboard를 이용하여 로봇을 수동 이동
- global localiztion이 수행되는지 확인
- 수행 완료 :

<img src="complete global localization.png" alt="complete global localization" width="400"/>


---


## ✅  동작 설명

| 항목 | 설명 |
|------|------|
| 서비스 이름 | `/reinitialize_global_localization` |
| 서비스 타입 | `std_srvs/srv/Empty` |
| 동작 | 로봇의 위치를 지도 전체에서 랜덤하게 다시 추정하도록 파티클을 재분포함. |

---

