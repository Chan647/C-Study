
# 📚 ROS 2 액션(Action) : 서버(Server)
---

## 🧨 실습 목표

- Tiago 시뮬레이션에서 액션 서버를 구현하여 팔을 원하는 위치로 이동하도록 제어
- 팔 동작 상태에 대한 피드백 제공과 결과 반환을 구현

---

## 📂 패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake tiago_arm_action_server --dependencies rclcpp rclcpp_action control_msgs trajectory_msgs
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

class MoveArmServer : public rclcpp::Node {
public:
    using GoalHandle = rclcpp_action::ServerGoalHandle<FollowJointTrajectory>;

    MoveArmServer() : Node("move_arm_server") {
        server_ = rclcpp_action::create_server<FollowJointTrajectory>(
            this,
            "/arm_controller/follow_joint_trajectory",
            std::bind(&MoveArmServer::handle_goal, this, std::placeholders::_1, std::placeholders::_2),
            std::bind(&MoveArmServer::handle_cancel, this, std::placeholders::_1),
            std::bind(&MoveArmServer::handle_accepted, this, std::placeholders::_1)
        );

        publisher_ = this->create_publisher<trajectory_msgs::msg::JointTrajectory>("/arm_controller/command", 10);
        RCLCPP_INFO(this->get_logger(), "Action Server Ready...");
    }

private:
    rclcpp_action::Server<FollowJointTrajectory>::SharedPtr server_;
    rclcpp::Publisher<trajectory_msgs::msg::JointTrajectory>::SharedPtr publisher_;

    rclcpp_action::GoalResponse handle_goal(
        const rclcpp_action::GoalUUID & uuid,
        std::shared_ptr<const FollowJointTrajectory::Goal> goal) {
        RCLCPP_INFO(this->get_logger(), "Received goal request");
        (void)uuid;
        return rclcpp_action::GoalResponse::ACCEPT_AND_EXECUTE;
    }

    rclcpp_action::CancelResponse handle_cancel(const std::shared_ptr<GoalHandle> goal_handle) {
        RCLCPP_INFO(this->get_logger(), "Received cancel request");
        (void)goal_handle;
        return rclcpp_action::CancelResponse::ACCEPT;
    }

    void handle_accepted(const std::shared_ptr<GoalHandle> goal_handle) {
        std::thread{std::bind(&MoveArmServer::execute, this, goal_handle)}.detach();
    }

    void execute(const std::shared_ptr<GoalHandle> goal_handle) {
        const auto goal = goal_handle->get_goal();

        trajectory_msgs::msg::JointTrajectory traj_msg;
        traj_msg.joint_names = goal->trajectory.joint_names;
        traj_msg.points = goal->trajectory.points;

        publisher_->publish(traj_msg);

        auto feedback = std::make_shared<FollowJointTrajectory::Feedback>();
        auto result = std::make_shared<FollowJointTrajectory::Result>();

        rclcpp::Rate rate(1);
        for (int i = 0; i <= 5; ++i) {
            if (goal_handle->is_canceling()) {
                result->error_code = control_msgs::action::FollowJointTrajectory_Result::SUCCESSFUL;
                goal_handle->canceled(result);
                RCLCPP_INFO(this->get_logger(), "Goal canceled.");
                return;
            }
            feedback->joint_names = traj_msg.joint_names;
            feedback->actual.time_from_start = rclcpp::Duration::from_seconds(i);
            goal_handle->publish_feedback(feedback);
            rate.sleep();
        }

        result->error_code = control_msgs::action::FollowJointTrajectory_Result::SUCCESSFUL;
        goal_handle->succeed(result);
        RCLCPP_INFO(this->get_logger(), "Goal execution complete.");
    }
};

int main(int argc, char **argv) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<MoveArmServer>());
    rclcpp::shutdown();
    return 0;
}
```

---

## 📄 CMakeLists.txt 수정

```cmake
add_executable(move_arm_server src/move_arm_server.cpp)
ament_target_dependencies(move_arm_server rclcpp rclcpp_action control_msgs trajectory_msgs)

install(TARGETS move_arm_server DESTINATION lib/${PROJECT_NAME})
```

---

## 🚀  빌드 및 실행

```bash
cd ~/ros2_ws
colcon build --packages-select tiago_arm_action_server
source install/setup.bash

ros2 run tiago_arm_action_server move_arm_server
```
---

## ✅ 로봇 동작을 위한 명령어 사용

```bash
ros2 action send_goal /arm_controller/follow_joint_trajectory control_msgs/action/FollowJointTrajectory "
trajectory:
  joint_names: ['arm_1_joint', 'arm_2_joint', 'arm_3_joint', 'arm_4_joint', 'arm_5_joint', 'arm_6_joint', 'arm_7_joint']
  points:
  - positions: [0.2, -0.5, 0.3, -1.0, 0.0, 0.5, 0.0]
    time_from_start: {sec: 3, nanosec: 0}
"
```

출력 결과 :

<img src="action server.png" alt="action server" width="400"/>

<img src="robot command.png" alt="robot command" width="400"/>

<img src="robot operation.png" alt="robot operation" width="400"/>

- Action Server Ready 출력 
- 목표 trajectory 요청
- 피드백 제공 및 로봇 동작
- 완료 시 , Goal execution complete 출력



