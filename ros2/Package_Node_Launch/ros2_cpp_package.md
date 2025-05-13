# 🧮 ROS 2 : C++ 패키지 실습 



## 📁 1. 워크스페이스 생성 및 초기화

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build         # 초기 빌드
source install/setup.bash
```

---

## 📦 2. 패키지 생성

```bash
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake cpp_test_pkg
```

옵션 설명:
- `--build-type ament_cmake`: C++용 CMake 빌드 시스템 사용
- `cpp_test_pkg`: 생성할 패키지 이름

---

## 📂 3. 생성된 패키지 확인

```bash
cd ~/ros2_ws/src/cpp_test_pkg
tree
```

출력 결과:
```
cpp_test_pkg/
├── CMakeLists.txt
├── package.xml
└── src/
```

---

## 🔨 4. 워크스페이스 빌드

```bash
cd ~/ros2_ws
colcon build --packages-select cpp_test_pkg
```

빌드 성공 시 출력 결과:
```
Starting >>> cpp_test_pkg
Finished <<< cpp_test_pkg
```

---

## 🔄 5. 설치된 패키지를 환경에 반영

```bash
source install/setup.bash
```

---

## 🔍 6. 패키지 설치 여부 확인

```bash
ros2 pkg list | grep cpp_test_pkg
```

출력 결과:
```
cpp_test_pkg
```

---

## 🧨 특정 패키지만 빌드

```
colcon build --symlink-install --packages-select <package_name>

```
