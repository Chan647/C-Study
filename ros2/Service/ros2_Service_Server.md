
# 📚 ROS 2 서비스(Service) : 서버(Server) 


---


## 🧨 실습 목표

- Gazebo 상에서 Tiago 로봇을 ROS 2 서비스 호출을 통해 전진하도록 제어
- 서비스 요청 시 주어진 거리만큼 로봇이 앞으로 이동

---

## 🎀 서버(Server) 역할

- 서비스 요청을 받아 Tiago 로봇에 이동 명령을 전달
- 요청된 거리에 따라 로봇을 전진시키고, 동작 완료 후 성공 여부를 반환

---

## 📂 프로젝트 구조
```
tiago_service_examples/
├── CMakeLists.txt
├── package.xml
├── srv/
│   └── MoveForward.srv
└── src/
    └── move_forward_server.cpp
```

---


## 📄 예제 코드

```cpp
#include "rclcpp/rclcpp.hpp"
#include "geometry_msgs/msg/twist.hpp"
#include "tiago_service_examples/srv/move_forward.hpp"
#include <chrono>

using namespace std::chrono_literals;

class MoveForwardServer : public rclcpp::Node {
public:
    MoveForwardServer() : Node("move_forward_server") {
        service_ = this->create_service<tiago_service_examples::srv::MoveForward>(
            "move_forward",
            std::bind(&MoveForwardServer::handle_service, this, std::placeholders::_1, std::placeholders::_2)
        );
        publisher_ = this->create_publisher<geometry_msgs::msg::Twist>("/cmd_vel", 10);
        RCLCPP_INFO(this->get_logger(), "Move Forward Service Ready...");
    }

private:
    void handle_service(
        const std::shared_ptr<tiago_service_examples::srv::MoveForward::Request> request,
        std::shared_ptr<tiago_service_examples::srv::MoveForward::Response> response) {

        double speed = 0.2; // m/s
        double duration = request->distance / speed;

        geometry_msgs::msg::Twist msg;
        msg.linear.x = speed;

        rclcpp::Rate rate(10);
        auto start_time = this->now();

        while ((this->now() - start_time).seconds() < duration) {
            publisher_->publish(msg);
            rate.sleep();
        }

        // Stop the robot
        msg.linear.x = 0.0;
        publisher_->publish(msg);

        response->success = true;
        RCLCPP_INFO(this->get_logger(), "Move Forward Completed.");
    }

    rclcpp::Service<tiago_service_examples::srv::MoveForward>::SharedPtr service_;
    rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr publisher_;
};

int main(int argc, char **argv) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<MoveForwardServer>());
    rclcpp::shutdown();
    return 0;
}
```
---

## ⚙️ CMakeLists.txt 수정

```bash
add_executable(move_forward_server src/move_forward_server.cpp)
ament_target_dependencies(move_forward_server rclcpp geometry_msgs tiago_service_examples)
```
---

## 🚀 빌드 및 실행 

```bash
cd ~/ros2_ws
colcon build --packages-select tiago_service_examples
source install/setup.bash

ros2 run tiago_service_examples move_forward_server
```

출력 결과 :

<img src="서비스 서버.png" alt="서비스 서버" width="400"/>

<img src="서비스 로봇.png" alt="서비스 로봇" width="400"/>

- Move Forward Service Ready... 출력, 클라이언트 측에서 명령을 받으면  로봇이 1m 전진
- Move Forward Completed 출력

---