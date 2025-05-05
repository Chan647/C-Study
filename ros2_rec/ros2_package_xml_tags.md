# ROS 2 C++에서 사용하는 package.xml 태그 정리

ROS 2 패키지의 package.xml 파일에서 자주 사용하는 태그들과 그 역할을 정리한 문서입니다.

---

## ✅ 주요 태그 및 역할

---

### 🔹 `<name>`

- 패키지의 이름을 정의합니다.
- CMakeLists.txt의 `project()`와 일치해야 합니다.

```xml
<name>cpp_tutorial_pkg</name>
```

---

### 🔹 `<version>`

- 패키지의 버전을 지정합니다.
- 일반적으로 `0.0.0`에서 시작해 프로젝트에 따라 증가시킵니다.

```xml
<version>0.0.0</version>
```

---

### 🔹 `<description>`

- 패키지에 대한 간단한 설명입니다.

```xml
<description>Basic ROS 2 C++ publisher and subscriber example</description>
```

---

### 🔹 `<maintainer>`

- 패키지를 관리하는 사람의 이름과 이메일입니다.
- `email=""` 속성은 필수입니다.

```xml
<maintainer email="you@example.com">Your Name</maintainer>
```

---

### 🔹 `<license>`

- 오픈소스 라이선스를 명시합니다.
- 예: Apache-2.0, MIT, BSD 등

```xml
<license>Apache License 2.0</license>
```

---

### 🔹 `<buildtool_depend>`

- 빌드 도구 의존성을 지정합니다.
- C++ 패키지는 보통 `ament_cmake`를 사용합니다.

```xml
<buildtool_depend>ament_cmake</buildtool_depend>
```

---

### 🔹 `<depend>`

- 일반적인 런타임 및 빌드 의존성을 지정합니다.
- 예: `rclcpp`, `std_msgs`, `geometry_msgs` 등

```xml
<depend>rclcpp</depend>
<depend>std_msgs</depend>
```

---

### 🔹 `<build_depend>`, `<exec_depend>`, `<test_depend>`

- 상황별로 의존성을 세분화합니다.

| 태그 | 의미 |
|------|------|
| `<build_depend>` | 빌드할 때만 필요 |
| `<exec_depend>` | 실행할 때만 필요 |
| `<test_depend>` | 테스트할 때만 필요 |

---

### 🔹 `<export>`

- 추가적인 빌드 정보나 설정을 export합니다.
- C++에서는 보통 `ament_cmake`의 타입을 명시합니다.

```xml
<export>
  <build_type>ament_cmake</build_type>
</export>
```

---

## 📌 전체 예시

```xml
<?xml version="1.0"?>
<package format="3">
  <name>cpp_tutorial_pkg</name>
  <version>0.0.0</version>
  <description>Basic ROS 2 C++ publisher and subscriber example</description>

  <maintainer email="you@example.com">Your Name</maintainer>
  <license>Apache License 2.0</license>

  <buildtool_depend>ament_cmake</buildtool_depend>
  <depend>rclcpp</depend>
  <depend>std_msgs</depend>

  <export>
    <build_type>ament_cmake</build_type>
  </export>
</package>
```

---

## ✅ 요약

| 태그 | 용도 |
|------|------|
| `<name>`, `<version>`, `<description>` | 패키지 식별 정보 |
| `<maintainer>`, `<license>` | 법적 정보 |
| `<buildtool_depend>` | 빌드 도구 지정 |
| `<depend>` | 실행 및 빌드 의존성 |
| `<export>` | 빌드 타입 명시 등 추가 정보 |