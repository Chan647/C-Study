# ROS 2 C++에서 많이 사용하는 패키지 목록

ROS 2에서 C++ 노드를 개발할 때 자주 사용하는 패키지들을 용도별로 정리한 문서입니다.

---

## ✅ 기본적으로 많이 사용하는 패키지

| 패키지 이름 | 용도 | 예시 사용 상황 |
|-------------|------|----------------|
| `rclcpp` | ROS 2 노드 생성 및 통신의 핵심 라이브러리 | `Node`, `Publisher`, `Subscription`, `Timer` 등 |
| `std_msgs` | 기본 메시지 타입 (String, Int32 등) | 텍스트, 숫자, 불린 등 단순 데이터 송수신 |
| `geometry_msgs` | 위치, 속도, 회전 정보 메시지 | `Twist`, `Pose`, `Vector3` 등 로봇 이동 제어 |
| `sensor_msgs` | 센서 데이터 메시지 타입 | `Image`, `LaserScan`, `Imu` 등 |
| `nav_msgs` | 내비게이션 관련 메시지 | `Odometry`, `Path` |
| `tf2`, `tf2_ros` | 좌표 변환 프레임 관리 | `TransformBroadcaster`, `TransformListener` |
| `action_msgs` | 액션 타입 사용 시 필요 | 로봇 팔 제어, 장기 작업 처리 등 |
| `example_interfaces` | 연습용 메시지/서비스 정의 | `AddTwoInts`, `Fibonacci` 액션 등 |
| `visualization_msgs` | RViz 시각화 메시지 | `Marker`, `MarkerArray` 등 3D 시각화 |
| `std_srvs` | 표준 서비스 타입 | `Trigger`, `SetBool` 등 간단한 서비스 호출 |

---

## 📦 의존성 선언 예시

### 📄 package.xml

```xml
<depend>rclcpp</depend>
<depend>std_msgs</depend>
<depend>geometry_msgs</depend>
<depend>sensor_msgs</depend>
```

### ⚙️ CMakeLists.txt

```cmake
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)

ament_target_dependencies(my_node rclcpp std_msgs geometry_msgs sensor_msgs)
```

---

## 🧠 상황별 자주 쓰는 패키지

| 상황 | 자주 쓰는 패키지 |
|------|------------------|
| 로봇 제어 | `geometry_msgs`, `nav_msgs`, `tf2_ros` |
| SLAM/내비게이션 | `nav2_msgs`, `tf2`, `geometry_msgs` |
| 센서 처리 | `sensor_msgs`, `image_transport`, `cv_bridge` |
| RViz 시각화 | `visualization_msgs`, `rviz_common` |
| 테스트용 | `example_interfaces`, `std_srvs` |

---



### 🔹 `cmake_minimum_required(VERSION 3.8)`

- CMake의 최소 버전을 지정합니다.
- ROS 2는 보통 3.8 이상을 요구합니다.

---

### 🔹 `project(<패키지이름>)`

- 현재 패키지의 이름을 설정합니다.
- `package.xml`의 `<name>`과 일치해야 합니다.

예시:
```cmake
project(cpp_tutorial_pkg)
```

---

### 🔹 `find_package(...)`

- 외부 패키지(라이브러리)를 찾고 포함합니다.
- `REQUIRED`를 붙이면 해당 패키지가 없을 경우 빌드 오류 발생.

예시:
```cmake
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
```

---

### 🔹 `add_executable(...)`

- 주어진 C++ 소스 파일을 빌드해서 실행 파일을 생성합니다.

예시:
```cmake
add_executable(talker src/talker.cpp)
```

---

### 🔹 `ament_target_dependencies(...)`

- `add_executable`로 만든 실행 파일에 ROS 2 라이브러리를 링크합니다.

예시:
```cmake
ament_target_dependencies(talker rclcpp std_msgs)
```

---

### 🔹 `install(TARGETS ...)`

- 빌드한 실행 파일을 설치 경로(`install/`)에 복사하여 `ros2 run`으로 실행 가능하게 합니다.

예시:
```cmake
install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME}
)
```

---

### 🔹 `install(DIRECTORY launch ...)`

- launch 디렉토리 내 파일을 설치 경로에 복사하여 `ros2 launch` 명령어로 실행 가능하게 합니다.

예시:
```cmake
install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
```

---

### 🔹 `ament_package()`

- ROS 2 빌드 시스템인 `ament`에 이 패키지를 등록합니다.
- 항상 파일의 마지막에 위치해야 합니다.

---

## ✅ 예시: 간단한 CMakeLists.txt 구조

```cmake
cmake_minimum_required(VERSION 3.8)
project(my_robot_pkg)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(talker src/talker.cpp)
ament_target_dependencies(talker rclcpp std_msgs)

install(TARGETS
  talker
  DESTINATION lib/${PROJECT_NAME}
)

install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)

ament_package()
```

---

## 📌 참고 요약

| 명령어 | 기능 |
|--------|------|
| `find_package` | 필요한 패키지 탐색 |
| `add_executable` | C++ 실행 파일 등록 |
| `ament_target_dependencies` | 실행 파일에 필요한 의존성 연결 |
| `install(TARGETS ...)` | 실행 파일 설치 |
| `install(DIRECTORY ...)` | launch 파일 설치 |
| `ament_package()` | 패키지 메타 정보 등록 |