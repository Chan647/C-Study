# 🧮 ROS 2 :  Launch(C++,Python)

---

## ✅  전제 조건

- ROS 2 패키지 이름: `cpp_tutorial_pkg`
- 실행 가능한 노드:
  - `talker` (퍼블리셔)
  - `listener` (서브스크라이버)

---

- talker :

```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;

class TalkerNode : public rclcpp::Node {
public:
  TalkerNode() : Node("talker") {
    publisher_ = this->create_publisher<std_msgs::msg::String>("chatter", 10);
    timer_ = this->create_wall_timer(500ms, std::bind(&TalkerNode::publish_message, this));
  }

private:
  void publish_message() {
    auto message = std_msgs::msg::String();
    message.data = "Hello ROS 2!";
    RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
    publisher_->publish(message);
  }

  rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
  rclcpp::TimerBase::SharedPtr timer_;
};

int main(int argc, char *argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<TalkerNode>());
  rclcpp::shutdown();
  return 0;
}
```
- listener :

```cpp
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

class ListenerNode : public rclcpp::Node {
public:
  ListenerNode() : Node("listener_node") {
    subscription_ = this->create_subscription<std_msgs::msg::String>(
      "chatter", 10,
      std::bind(&ListenerNode::message_callback, this, std::placeholders::_1));
    RCLCPP_INFO(this->get_logger(), "Listener Node has been started.");
  }

private:
  void message_callback(const std_msgs::msg::String::SharedPtr msg) const {
    RCLCPP_INFO(this->get_logger(), "Received: '%s'", msg->data.c_str());
  }

  rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
};

int main(int argc, char *argv[]) {
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<ListenerNode>());
  rclcpp::shutdown();
  return 0;
}

```
---

## 📁  launch 디렉토리 생성

```bash
cd ~/ros2_ws/src/cpp_tutorial_pkg
mkdir launch
```

---

## 📝  launch 파일 작성

- 파일 이름 : `launch/talker_listener_launch.py`

```python
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='cpp_tutorial_pkg',
            executable='talker',
            name='talker_node',
            output='screen'
        ),
        Node(
            package='cpp_tutorial_pkg',
            executable='listener',
            name='listener_node',
            output='screen'
        ),
    ])
```

---

## ⚙️  CMakeLists.txt 수정

```cmake
install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
```

- `launch/` 폴더에 있는 파일들을 설치 시 공유 디렉토리로 복사

---

## 🛠️  패키지 빌드 및 환경 설정

```bash
cd ~/ros2_ws
colcon build --packages-select cpp_tutorial_pkg
source install/setup.bash
```

---

## 🚀  launch 파일 실행

```bash
ros2 launch cpp_tutorial_pkg talker_listener_launch.py
```

출력 결과:

<img src="런치 실습.png" alt="런치 파일 실행" width="400"/>

---

