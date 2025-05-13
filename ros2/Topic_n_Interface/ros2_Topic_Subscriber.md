# 🧮 ROS 2 : Subscriber 



---

## 🧨 실습 목표

- `/mobile_base_controller/odom` 토픽 구독
- 메시지 타입: `nav_msgs/msg/Odometry`
- TIAGo 시뮬레이터에서 실제 위치와 속도 출력

---

## 📦  패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake cpp_tutorial_pkg --dependencies rclcpp nav_msgs
```

---

## 📄  노드 작성

```bash
cd ~/ros2_ws/src/cpp_tutorial_pkg/src
touch odom_listener.cpp
```

### ✍️예제 코드

```cpp
#include "rclcpp/rclcpp.hpp"
#include "nav_msgs/msg/odometry.hpp"

class OdomListener : public rclcpp::Node {
public:
  OdomListener() : Node("odom_listener") {
    subscription_ = this->create_subscription<nav_msgs::msg::Odometry>(
      "/mobile_base_controller/odom", 10,
      std::bind(&OdomListener::callback, this, std::placeholders::_1));
  }

private:
  void callback(const nav_msgs::msg::Odometry::SharedPtr msg) {
    RCLCPP_INFO(this->get_logger(),
      "Pose: (%.2f, %.2f), Linear Vel: %.2f m/s",
      msg->pose.pose.position.x,
      msg->pose.pose.position.y,
      msg->twist.twist.linear.x
    );
  }

  rclcpp::Subscription<nav_msgs::msg::Odometry>::SharedPtr subscription_;
};

int main(int argc, char *argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<OdomListener>());
  rclcpp::shutdown();
  return 0;
}
```

---

## ⚙️  CMakeLists.txt 수정


```cmake
find_package(nav_msgs REQUIRED)

add_executable(odom_listener src/odom_listener.cpp)
ament_target_dependencies(odom_listener rclcpp nav_msgs)

install(TARGETS
  odom_listener
  DESTINATION lib/${PROJECT_NAME}
)
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

TIAGo 시뮬레이터를 먼저 실행한 후:  

<img src="robot simulator.png" alt="robot simulator" width="400"/>


```bash
ros2 run cpp_tutorial_pkg odom_listener
```

출력 결과:

<img src="topic subscriber.png" alt="topic subscriber" width="400"/>

- teleop_twist_keyboard를 이용하여 로봇 조작 시, 위치와 속도 출력
---

## 📁 디렉토리 구조

```
~/ros2_ws/
└── src/
    └── cpp_tutorial_pkg/
        ├── src/
        │   └── odom_listener.cpp
        ├── CMakeLists.txt
        └── package.xml
```

---


