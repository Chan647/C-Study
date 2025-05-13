
# 📚 Nav2 : Path Planning 실습 

---

##  실습 목표

- TurtleBot3 + Nav2를 사용한 다양한 경로 계획 실습
- rviz2 - 2D Goal Pose
- Topic
- Action Server
- 프로그래밍

---

## 🎉 환경 준비

### 1️⃣ Gazebo 시뮬레이션 실행  
```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

### 2️⃣ Navigation2 실행  
```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py 
use_sim_time:=true map:=/home/chan/map/my_map.yaml
```

---

## 📌 RViz2 버튼을 통한 Path Planning

```bash
ros2 run rviz2 rviz2
```

- RViz2에서 `2D Nav Goal` 버튼 클릭  
- 원하는 위치와 방향 지정 → 자동 경로 계획 및 이동  
- 확인할 토픽:
   - `/plan`
   - `/cmd_vel`
   - `/amcl_pose`


<img src="rviz2 2d pose estimate.png" alt="2d pose estimate" width="400"/>

<img src="rviz2 2d goal pose.png" alt="2d goal pose" width="400"/>


---
## 📌 Topic을 통한 Path 요청 

```bash
ros2 topic pub -1 /goal_pose geometry_msgs/PoseStamped "{header: {stamp: {sec: 0}, frame_id: 'map'}, pose: {position: {x: 0.6, y: 1.9, z: 0.0}, orientation: {w: 1.0}}}"
```
- `ros2 topic echo /clicked_point`를 사용해 토픽을 구독
- rviz2 상단 툴바에서 'Publish Point' 클릭 후 원하는 위치에 마우스 클릭

<img src="clicked point.png" alt="clikced point" width="400"/>

- 원하는 위치 값 명령

<img src="topic move command.png" alt="topic move command" width="400"/>

- 결과 :

<img src="move robot topic.png" alt="move robot topic" width="400"/>


---
## 📌 Action Server를 통한 Path 요청

### 1️⃣ Action 서버 확인  
```bash
ros2 action list
ros2 action info /navigate_to_pose
```
<img src="action list n info.png" alt="action list n info" width="400"/>

### 2️⃣ 터미널에서 요청 
```bash
ros2 action send_goal /navigate_to_pose nav2_msgs/action/NavigateToPose \
    "{pose: {header: {frame_id: 'map'}, pose: {position: {x: 2.5, y: -1.4, z: 0.0}, orientation: {w: 1.0}}}}"
```
- `ros2 topic echo /clicked_point`를 사용해 토픽을 구독
- rviz2 상단 툴바에서 'Publish Point' 클릭 후 원하는 위치에 마우스 클릭

<img src="clicked point_action.png" alt="clicked point action" width="400"/>

- 원하는 위치값 명령

<img src="send goal cmd.png" alt="send goal cmd" width="400"/>

- 결과 :

<img src="move robot action.png" alt="move robot action" width="400"/>

---

## 📌 프로그래밍을 통한 Path Planning

### 📂 패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake navigate_to_pose_client --dependencies rclcpp rclcpp_action nav2_msgs
```
---

### 📂  디렉토리 구조

```
navigate_to_pose_client/
├── CMakeLists.txt
├── package.xml
└── src/
    └── navigate_to_pose_client.cpp
```

---

### 📄 예제코드

```cpp
#include "rclcpp/rclcpp.hpp"
#include "rclcpp_action/rclcpp_action.hpp"
#include "nav2_msgs/action/navigate_to_pose.hpp"

using namespace std::placeholders;
using NavigateToPose = nav2_msgs::action::NavigateToPose;

class NavigateClient : public rclcpp::Node
{
public:
    NavigateClient() : Node("navigate_to_pose_client") {
        client_ = rclcpp_action::create_client<NavigateToPose>(this, "/navigate_to_pose");
        send_goal();
    }

private:
    rclcpp_action::Client<NavigateToPose>::SharedPtr client_;

    void send_goal() {
        if (!client_->wait_for_action_server(std::chrono::seconds(5))) {
            RCLCPP_ERROR(this->get_logger(), "Action server not available.");
            return;
        }

        auto goal_msg = NavigateToPose::Goal();
        goal_msg.pose.header.frame_id = "map";
        goal_msg.pose.pose.position.x = 2.9;
        goal_msg.pose.pose.position.y = 2.5;
        goal_msg.pose.pose.orientation.w = 0.0;

        auto send_goal_options = rclcpp_action::Client<NavigateToPose>::SendGoalOptions();
        send_goal_options.result_callback = 
            std::bind(&NavigateClient::result_callback, this, _1);

        client_->async_send_goal(goal_msg, send_goal_options);
    }

    void result_callback(const rclcpp_action::ClientGoalHandle<NavigateToPose>::WrappedResult & result) {
        RCLCPP_INFO(this->get_logger(), "Navigation completed with status: %d", result.code);
        rclcpp::shutdown();
    }
};

int main(int argc, char **argv) {
    rclcpp::init(argc, argv);
    rclcpp::spin(std::make_shared<NavigateClient>());
    return 0;
}
```

---

### ⚙️ CMakeLists.txt 수정

```cmake

add_executable(navigate_to_pose_client src/navigate_to_pose_client.cpp)
ament_target_dependencies(navigate_to_pose_client rclcpp rclcpp_action nav2_msgs)

install(TARGETS
  navigate_to_pose_client
  DESTINATION lib/${PROJECT_NAME}
)

```

---

## 🚀 빌드 및 실행

```bash
cd ~/ros2_ws
colcon build --packages-select navigate_to_pose_client
source install/setup.bash

ros2 run navigate_to_pose_client navigate_to_pose_client
```
- 출력 결과 :

<img src="pkg run.png" alt="pkg run" width="400"/>

<img src="pgm robot move.png" alt="pgm robot move" width="400"/>


