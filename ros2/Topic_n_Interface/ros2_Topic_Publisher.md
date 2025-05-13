#  🧮 ROS 2 : Topic - Publisher 



---

## 🧨 실습 목표

- TIAGo 로봇을 `/mobile_base_controller/cmd_vel` 토픽을 통해 제어
- 3초 동안 전진하고, 이후 3초 동안 후진
- 이 동작을 반복 수행

---

## 📦 패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake cpp_tutorial_pkg

```
---

## 🎀 디렉토리 이동 및 파일 작성

```bash
cd ~/ros2_ws/src/cpp_tutorial_pkg/src
touch robot_mover.cpp
```
---

## 📄 예제 코드

```cpp
#include "rclcpp/rclcpp.hpp"
#include "geometry_msgs/msg/twist.hpp"
#include <chrono>

using namespace std::chrono_literals;

class TiagoMover : public rclcpp::Node {
public:
  TiagoMover() : Node("tiago_mover"), forward_(true) {
    publisher_ = this->create_publisher<geometry_msgs::msg::Twist>("/mobile_base_controller/cmd_vel", 10);
    timer_ = this->create_wall_timer(3s, std::bind(&TiagoMover::switchDirection, this));
    control_timer_ = this->create_wall_timer(100ms, std::bind(&TiagoMover::publishCommand, this));
    RCLCPP_INFO(this->get_logger(), "TIAGo Mover Node Started");
  }

private:
  void switchDirection() {
    forward_ = !forward_;
    RCLCPP_INFO(this->get_logger(), forward_ ? "Switching to FORWARD" : "Switching to BACKWARD");
  }

  void publishCommand() {
    geometry_msgs::msg::Twist msg;
    msg.linear.x = forward_ ? 0.2 : -0.2;
    msg.angular.z = 0.0;
    publisher_->publish(msg);
  }

  rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr publisher_;
  rclcpp::TimerBase::SharedPtr timer_;
  rclcpp::TimerBase::SharedPtr control_timer_;
  bool forward_;
};

int main(int argc, char *argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<TiagoMover>());
  rclcpp::shutdown();
  return 0;
}
```

---
## ⚙️ CMakeLists 수정

```bash
add_executable(robot_mover src/robot_mover.cpp)
ament_target_dependencies(robot_mover rclcpp geometry_msgs)
install(TARGETS robot_mover DESTINATION lib/${PROJECT_NAME})
```
---

### 🎇  빌드 및 실행

```bash
colcon build --symlink-install --packages-select cpp_tutorial_pkg
source install/setup.bash
ros2 run cpp_tutorial_pkg robot_mover
```
---

## ✅ 결과

<img src="move print.png" alt="move print" width="400"/>

<img src="move robot.png" alt="move robot" width="400"/>

