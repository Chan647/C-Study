
# 📚 ROS 2 액션(ACtion) : 클라이언트(Client)

---

## 🧨 실습 목표

- Gazebo 시뮬레이션에서 Tiago 로봇의 팔을 ROS 2 액션 클라이언트를 통해 제어
- FollowJointTrajectory 액션을 이용하여 팔을 원하는 위치로 이동

---

## 📂 패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake tiago_arm_control --dependencies rclcpp rclcpp_action control_msgs trajectory_msgs
```

---

## 🎇 액션 서버 확인

```bash
ros2 action list
ros2 action info /arm_controller/follow_joint_trajectory
```

---

## 📄 예제 코드

```cpp
#include "rclcpp/rclcpp.hpp"
#include "rclcpp_action/rclcpp_action.hpp"
#include "control_msgs/action/follow_joint_trajectory.hpp"
#include "trajectory_msgs/msg/joint_trajectory_point.hpp"

using namespace std::chrono_literals;
using FollowJointTrajectory = control_msgs::action::FollowJointTrajectory;

class MoveArmClient : public rclcpp::Node {
public:
    MoveArmClient() : Node("move_arm_client") {
        client_ = rclcpp_action::create_client<FollowJointTrajectory>(
            this, "/arm_controller/follow_joint_trajectory");

        while (!client_->wait_for_action_server(1s)) {
            RCLCPP_INFO(this->get_logger(), "Waiting for action server...");
        }

        auto goal_msg = FollowJointTrajectory::Goal();
        goal_msg.trajectory.joint_names = {
            "arm_1_joint", "arm_2_joint", "arm_3_joint",
            "arm_4_joint", "arm_5_joint", "arm_6_joint", "arm_7_joint"
        };

        trajectory_msgs::msg::JointTrajectoryPoint point;
        point.positions = {0.2, -0.5, 0.3, -1.0, 0.0, 0.5, 0.0};  // 목표 관절 각도 (라디안)
        point.time_from_start = rclcpp::Duration::from_seconds(3.0);

        goal_msg.trajectory.points.push_back(point);

        auto send_goal_options = rclcpp_action::Client<FollowJointTrajectory>::SendGoalOptions();
        send_goal_options.result_callback =
            [this](const rclcpp_action::ClientGoalHandle<FollowJointTrajectory>::WrappedResult & result) {
                RCLCPP_INFO(this->get_logger(), "Action completed with status: %d", static_cast<int>(result.code));
                rclcpp::shutdown();
            };

        client_->async_send_goal(goal_msg, send_goal_options);
    }

private:
    rclcpp_action::Client<FollowJointTrajectory>::SharedPtr client_;
};

int main(int argc, char **argv) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<MoveArmClient>());
    return 0;
}
```

---

## 📄 CMakeLists.txt 수정

```cmake

add_executable(move_arm_client src/move_arm_client.cpp)
ament_target_dependencies(move_arm_client rclcpp rclcpp_action control_msgs trajectory_msgs)

install(TARGETS move_arm_client DESTINATION lib/${PROJECT_NAME})
```

---

## 🚀 빌드 및 실행

```bash
cd ~/ros2_ws
colcon build --packages-select tiago_arm_control
source install/setup.bash

ros2 run tiago_arm_control move_arm_client
```
출력 결과 :

<img src="액션 클라이언트.png" alt="액션 클라이언트" width="400"/>

<img src="로봇 팔모션.png" alt="로봇 팔모션" width="400"/>

- 시뮬레이션에서 로봇 팔이 목표 위치로 움직임

---


