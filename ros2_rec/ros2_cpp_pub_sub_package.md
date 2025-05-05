# ROS 2 C++ 퍼블리셔 & 서브스크라이버 패키지 예제

이 문서는 ROS 2에서 C++로 퍼블리셔(talker)와 서브스크라이버(listener) 노드를 포함한 패키지를 생성하는 실습 예제를 정리한 것입니다.

---

## 📦 패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake cpp_tutorial_pkg
```

---

## 📁 디렉토리 구조

```
cpp_tutorial_pkg/
├── CMakeLists.txt
├── package.xml
├── launch/
│   └── talker_listener_launch.py
├── src/
│   ├── talker.cpp
│   └── listener.cpp
```

---

## ✍️ talker.cpp (퍼블리셔)

```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"
#include <chrono>
#include <sstream>

using namespace std::chrono_literals;

class Talker : public rclcpp::Node {
public:
  Talker() : Node("talker_node"), count_(0) {
    publisher_ = this->create_publisher<std_msgs::msg::String>("chatter", 10);
    timer_ = this->create_wall_timer(
      1000ms, std::bind(&Talker::publish_msg, this));
  }

private:
  void publish_msg() {
    auto msg = std_msgs::msg::String();
    msg.data = "Message #" + std::to_string(count_++);
    RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", msg.data.c_str());
    publisher_->publish(msg);
  }

  rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
  rclcpp::TimerBase::SharedPtr timer_;
  int count_;
};

int main(int argc, char *argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<Talker>());
  rclcpp::shutdown();
  return 0;
}
```

---

## ✍️ listener.cpp (서브스크라이버)

```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

class Listener : public rclcpp::Node {
public:
  Listener() : Node("listener_node") {
    subscription_ = this->create_subscription<std_msgs::msg::String>(
      "chatter", 10,
      std::bind(&Listener::callback, this, std::placeholders::_1));
  }

private:
  void callback(const std_msgs::msg::String::SharedPtr msg) {
    RCLCPP_INFO(this->get_logger(), "Received: '%s'", msg->data.c_str());
  }

  rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
};

int main(int argc, char *argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<Listener>());
  rclcpp::shutdown();
  return 0;
}
```

---

## ⚙️ CMakeLists.txt 수정

```cmake
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(talker src/talker.cpp)
ament_target_dependencies(talker rclcpp std_msgs)

add_executable(listener src/listener.cpp)
ament_target_dependencies(listener rclcpp std_msgs)

install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME}
)

install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
```

---

## 🛠️ 빌드 및 실행

```bash
cd ~/ros2_ws
colcon build --packages-select cpp_tutorial_pkg --symlink-install
source install/setup.bash
```

---

## 🚀 실행 예시

### 터미널 1 (퍼블리셔)

```bash
ros2 run cpp_tutorial_pkg talker
```

### 터미널 2 (서브스크라이버)

```bash
ros2 run cpp_tutorial_pkg listener
```

또는 launch 파일로 실행:

```bash
ros2 launch cpp_tutorial_pkg talker_listener_launch.py
```

---

이 예제는 ROS 2 노드 통신의 가장 기본적인 구조로, 이후에 파라미터, QoS, 서비스 등으로 확장 가능합니다.