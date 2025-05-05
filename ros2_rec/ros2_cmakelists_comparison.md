# ROS 2 CMakeLists.txt 수정 비교

이 문서는 ROS 2 패키지를 생성했을 때 자동으로 생성되는 기본 CMakeLists.txt와, 퍼블리셔 및 서브스크라이버 노드를 추가한 후 수정된 CMakeLists.txt를 비교한 것입니다.

---

## ✅ 기본 CMakeLists.txt (생성 직후)

```cmake
cmake_minimum_required(VERSION 3.8)
project(cpp_tutorial_pkg)

find_package(ament_cmake REQUIRED)

ament_package()
```

---

## ✅ 수정 후 CMakeLists.txt (퍼블리셔 & 서브스크라이버 포함)

```cmake
cmake_minimum_required(VERSION 3.8)
project(cpp_tutorial_pkg)

find_package(ament_cmake REQUIRED)
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

ament_package()
```

---

## 🔍 주요 변경 항목 요약

| 항목 | 기본 | 수정 후 |
|------|------|---------|
| rclcpp, std_msgs 패키지 사용 | ❌ 없음 | ✅ 추가됨 |
| C++ 실행 파일 빌드 | ❌ 없음 | ✅ `add_executable(...)` |
| 실행 파일 의존성 등록 | ❌ 없음 | ✅ `ament_target_dependencies(...)` |
| 실행 파일 설치 경로 등록 | ❌ 없음 | ✅ `install(TARGETS ...)` |
| launch 폴더 설치 경로 등록 | ❌ 없음 | ✅ `install(DIRECTORY launch ...)` |

---

## 📌 정리

수정된 CMakeLists.txt는 ROS 2 C++ 노드를 빌드하고 실행 가능하게 만드는 데 필요한 모든 설정을 포함하고 있습니다. 이를 통해 `ros2 run` 및 `ros2 launch` 명령어를 사용할 수 있게 됩니다.