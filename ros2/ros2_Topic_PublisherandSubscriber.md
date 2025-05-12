# 🧮 ROS 2 : Publisher & Subscriber 


---

## 🧨 실습 목표

- 전진 중 장애물 발견 시: 후진 1초 → 우회전 3초 → 다시 전진
- 구독 토픽: `/scan_raw` (`LaserScan`)
- 퍼블리시 토픽: `/cmd_vel`
- 전진 중 `"Move Forward"` 로그 출력
- 장애물 발견 시 `"Obstacle Discovery"` 로그 출력

---

## ✍️ 예제 코드 

```cpp
#include "rclcpp/rclcpp.hpp"
#include "sensor_msgs/msg/laser_scan.hpp"
#include "geometry_msgs/msg/twist.hpp"
#include <chrono>

using namespace std::chrono_literals;

class ScanAvoidNode : public rclcpp::Node {
public:
  ScanAvoidNode() : Node("scan_avoid_node") {
    ros_clock_ = this->get_clock();
    state_ = FORWARD;
    state_start_time_ = ros_clock_->now();

    subscription_ = this->create_subscription<sensor_msgs::msg::LaserScan>(
      "/scan_raw", 10, std::bind(&ScanAvoidNode::scanCallback, this, std::placeholders::_1));

    publisher_ = this->create_publisher<geometry_msgs::msg::Twist>("/cmd_vel", 10);
    timer_ = this->create_wall_timer(100ms, std::bind(&ScanAvoidNode::controlLoop, this));
  }

private:
  enum State { FORWARD, BACKWARD, TURNING };
  State state_;
  rclcpp::Time state_start_time_;
  rclcpp::Clock::SharedPtr ros_clock_;
  rclcpp::Subscription<sensor_msgs::msg::LaserScan>::SharedPtr subscription_;
  rclcpp::Publisher<geometry_msgs::msg::Twist>::SharedPtr publisher_;
  rclcpp::TimerBase::SharedPtr timer_;

  bool isObstacleClose(const sensor_msgs::msg::LaserScan::SharedPtr msg) {
    int center_index = msg->ranges.size() / 2;
    float distance = msg->ranges[center_index];
    return (distance < 0.5 && distance > msg->range_min);
  }

  void scanCallback(const sensor_msgs::msg::LaserScan::SharedPtr msg) {
    if (state_ != FORWARD) return;
    if (isObstacleClose(msg)) {
      RCLCPP_WARN(this->get_logger(), "Obstacle Discovery");
      state_ = BACKWARD;
      state_start_time_ = ros_clock_->now();
    }
  }

  void controlLoop() {
    geometry_msgs::msg::Twist cmd;
    auto now = ros_clock_->now();
    auto elapsed = now - state_start_time_;

    switch (state_) {
      case FORWARD:
        cmd.linear.x = 0.2;
        RCLCPP_INFO_THROTTLE(this->get_logger(), *ros_clock_, 2000, "Move Forward");
        break;
      case BACKWARD:
        cmd.linear.x = -0.2;
        if (elapsed > rclcpp::Duration::from_seconds(1.0)) {
          RCLCPP_INFO(this->get_logger(), "Switching to TURNING.");
          state_ = TURNING;
          state_start_time_ = ros_clock_->now();
        }
        break;
      case TURNING:
        cmd.angular.z = -0.5;
        if (elapsed > rclcpp::Duration::from_seconds(3.0)) {
          RCLCPP_INFO(this->get_logger(), "Switching to FORWARD.");
          state_ = FORWARD;
          state_start_time_ = ros_clock_->now();
        }
        break;
    }

    publisher_->publish(cmd);
  }
};

int main(int argc, char *argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<ScanAvoidNode>());
  rclcpp::shutdown();
  return 0;
}
```

---

## ⚙️ CMakeLists.txt 수정

```cmake
find_package(sensor_msgs REQUIRED)
add_executable(scan_avoid_turn src/scan_avoid_turn.cpp)
ament_target_dependencies(scan_avoid_turn rclcpp sensor_msgs geometry_msgs)
install(TARGETS scan_avoid_turn DESTINATION lib/${PROJECT_NAME})
```

---

## 🔧  빌드

```bash
cd ~/ros2_ws
colcon build --packages-select cpp_tutorial_pkg
source install/setup.bash
```

---

## 🚀  실행

```bash
ros2 run cpp_tutorial_pkg scan_avoid_turn
```

출력 결과 :

<img src="토픽 pub n sub.png" alt="토픽 pub n sub" width="400"/>

<img src="토픽 회전.png" alt="토픽 회전" width="400"/>


---





