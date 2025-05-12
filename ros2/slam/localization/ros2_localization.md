
# 📚 ROS 2 : Localization 

---

## 📣 Localization이란?

- 로봇이 자신이 지도 상에서 어디에 위치하고 있는지 추정하는 과정  
- 주로 AMCL (Adaptive Monte Carlo Localization)등의 알고리즘 사용

---

## 🔎 필수 Frame 개념

| Frame Name         | 설명 |
|--------------------|------|
| map            | - 세계 기준 고정 좌표계로, 로봇의 절대적인 위치를 표현<br> - 일반적으로 localization 알고리즘이 이 프레임을 기준으로 로봇의 위치를 추정<br> - 고정된 세계 좌표계로 변하지 않음|
| odom           | - 로봇의 오도메트리 데이터를 기준으로 한 상대 위치를 표현<br> - 로봇이 시작한 지점에서의 상대적인 움직임을 추적<br> - 시간이 지날수록 오차 누적(드리프트)이 발생할 수 있음|
| base_footprint | - 로봇의 바닥면과 맞닿은 지점을 기준으로 한 2D 평면 좌표계<br> - 주로 로봇의 움직임을 2D 공간에서 계산할 때 사용<br> - 일반적으로 Z축은 0으로 설정되며, 회전 정보는 포함되지 않음|
| base_link      | - 로봇 본체의 중심 좌표계<br> - 로봇에 장착된 센서나 링크들은 이 프레임을 기준으로 위치와 방향이 정의됨<br> - 3D 위치와 회전 정보를 모두 포함 |
| laser          | - LiDAR 센서의 좌표계<br> - 센서가 장착된 정확한 위치와 방향을 표현<br> - 보통 `base_link` 또는 `base_footprint`에 대해 고정된 변환으로 정의됨 |

### 📌 Frame 간 관계

### 🔹 map → odom
- `map`은 로봇이 세계 기준 좌표계에서 어디에 있는지를 나타냄
- `odom`은 오도메트리 센서 기반으로 로봇의 상대적 위치를 나타냄
- `map → odom` 변환은 localization 노드(예: `amcl`)가 계산하고 브로드캐스트함
- 이 변환은 로봇의 위치 추정이 얼마나 오도메트리로부터 벗어났는지를 나타냄
- localization이 담당

---
### 🔹 odom → base_link

- 로봇이 오도메트리 기준으로 얼마나 이동했는지 알려줌
- 절대 위치를 보장하지 않으며, 상대적인 단기 이동 추적에 사용
- 고정된 변환이 아니고, 주기적으로 갱신됨

---

### 🔹 base_footprint → base_link

- 로봇의 바닥면 위치와 본체 중심(base_link) 간의 고정된 변환
- 대부분 Z축 방향으로 약간 올라가 있으며 회전은 없음
- 로봇 URDF 파일에 고정 transform으로 정의됨


---

## 📫 ROS 2 Localization에 필요한 노드

| 노드 이름         | 역할 |
|-------------------|------|
| amcl         | Localization 주 알고리즘 (입력: Laser, Map) |
| map_server   | 정적 맵 제공 (지도 로드) |
| robot_state_publisher | URDF 기반 TF 브로드캐스트 |
| tf2_ros      | Frame 간 변환 관리 |
| rviz2        | 시각화 도구 (Localization 결과 확인) |
| Lifecycle Manager | 노드 상태 관리 (Nav2 사용 시) |

---

## 📥 2D LiDAR 기반 Localization 패키지

### 📌 AMCL (Adaptive Monte Carlo Localization)

- 파티클 필터 기반 위치 추정 알고리즘
- Monte Carlo Localization(MCL)기반, 로봇이 지도에서 자신의 위치를 찾을 수 있도록 도와줌
- 입력:
  - `/scan` (2D LiDAR 데이터)
  - `/map` (정적 맵)
  - `/tf` (Frame 변환 정보)
- 출력:
  - `/amcl_pose` (로봇 위치 추정 Pose)
  - `/tf` (`map → odom` 변환 브로드캐스트)
- 장점:
  - 적은 계산 비용으로 실시간 Localization 가능
  - 움직임에 따라 파티클 분포를 적응적으로 조정


