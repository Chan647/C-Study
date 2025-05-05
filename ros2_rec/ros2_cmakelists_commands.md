# ROS 2 C++에서 사용하는 CMakeLists.txt 명령어 정리

ROS 2 패키지의 CMakeLists.txt 파일에서 자주 사용하는 명령어들과 그 역할을 정리한 문서입니다.

---

## ✅ 주요 명령어 및 역할

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