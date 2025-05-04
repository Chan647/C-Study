
# 🧮 ROS 2 : Package, Node, Launch 


---

## 📦  Package (패키지)란?

- ROS 2에서 소프트웨어 구성의 기본 단위
- 특정 ROS2 프로그램에 포함된 모든 파일(즉 모든 CPP 파일, Python 파일, 설정 파일, 파라미터 파일)
- ROS2 프로그램을 패키지로 구성하면 다른 개발자/사용자와 훨씬쉽게 공유 가능
- 패키지 유형
  - Python Package
  - C++ Package

---

### 🔹 역할

- 노드(Node), 메시지(msg), 서비스(srv), 실행 스크립트 등 포함
- `CMakeLists.txt`, `package.xml` 파일로 메타정보 정의

---

### 🔹 생성 명령어

```bash
ros2 pkg create --build-type ament_cmake my_package
```
또는 Python일 경우:
```bash
ros2 pkg create --build-type ament_python my_package
```

---

## 📦 Python Package VS C++ Package

| 항목           | Python 패키지 구조             | C++ 패키지 구조                         | 특징 요약                          |
| ------------ | ----------------------------- | ---------------------------------------- | ------------------------------ |
| 설정 파일    | `setup.py` – Python 패키지 설정    | `CMakeLists.txt` – CMake 빌드 설정           | Python은 실행 시 해석, C++은 빌드 필요    |
| 공통 메타데이터 | `package.xml` – ROS 2 메타데이터   | `package.xml` – ROS 2 메타데이터              | ROS 2의 공통 구성요소                 |
|소스 코드 위치 | `<패키지명>/` 디렉토리 – Python 소스 코드 | `src/` 디렉토리 – C++ 소스, `include/` – 헤더 파일 | Python은 단순, C++은 구조 분리와 복잡도 존재 |
| 언어적 특징   | 인터프리터 언어, 빠른 개발, 프로토타이핑에 강함   | 컴파일 언어, 하드웨어 제어/실시간성/최적화 유리              | 목적에 따라 언어 선택 필요                |


## 🧩  Node (노드)란 ?

- ROS2에서 연산을 수행하는 최소 단위의 실행 프로세스
- 전체 로봇 시스템은 많은 노드로 구성됨
- ROS2에서는 단일 launch 파일에 하나 이상의 노드(C++ 또는 Python 프로그램 등)가 포함될 수 있음
- 각 노드는 특정 작업을 담당하며, 여러 노드가 서로 통신하며 복잡한 로봇 시스템을 구성
- 통신 방식
  - 토픽 (Topics): 발행/구독 모델을 사용한 비동기 통신
  - 서비스 (Services): 요청/응답 모델을 사용한 동기 통신
  - 액션 (Actions): 장기 실행 작업을 위한 비동기 통신
  - 파라미터 (Parameters): 노드의 구성 값을 저장하고 공유

---

### 🔹 특징

- 퍼블리셔, 서브스크라이버, 서비스, 액션 등 기능을 담당
- 하나의 패키지에는 여러 개의 노드 포함 가능

---

### 🔹 실행 예시
```bash
ros2 run my_package my_node
```

---

## 🚀  Launch (런치) 란?

- 여러 ROS2 노드와 그 매개변수를 정의하고 실행하는 스크립트
- 목적
  - 복잡한 로봇 시스템의 여러 컴포넌트를 쉽게 시작
  - 노드 실행 순서 관리
  - 실행 시 매개변수 설정
  - 조건부 실행 및 이벤트 처리
- 파일 형식
  - Python (.py)
  - XML (.xml)
  - YAML (.yaml)

---

### 🔹 특징

- ROS 2에서는 Python 기반의 launch 파일을 사용
- `.launch.py` 확장자를 가짐

---

### 🔹 기본 구조 예시

```python
from launch import LaunchDescription
from launch_ros.actions import Node

def generate_launch_description():
    return LaunchDescription([
        Node(
            package='my_package',
            executable='talker',
            name='my_talker',
            output='screen'
        ),
        Node(
            package='my_package',
            executable='listener',
            name='my_listener',
            output='screen'
        )
    ])
```

### 🔹 실행 명령어
```bash
ros2 launch my_package my_launch.py
```

---

## 🔄  요약

```text
[Package]
 ├── 여러 개의 [Node]를 포함할 수 있음
 ├── 메시지(msg), 서비스(srv) 등도 포함 가능
 └── [Launch] 파일로 여러 노드를 동시에 실행할 수 있음
```

---

