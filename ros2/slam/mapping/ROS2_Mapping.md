
# 📚 ROS 2 : Mapping 

---

## 📣 Mapping 이란?

- 매핑은 로봇이 센서 데이터를 이용해 주행 환경의 지도를 생성하는 과정
- SLAM 기술을 통해 위치 추정과 지도 생성을 동시에 수행할 수 있음
- 생성된 지도는 로봇의 자율 주행 및 경로 계획에 활용됨

---
## 🎐 2D Lidar 기반 Map - 점유 격자형 지도(Occupancy Grid Map)

- 공간을 2D 격자로 분할해 표현
- 센서 데이터 (LiDAR, 초음파 등)를 기반으로 지도 생성
- 로봇의 경로 계획(Navigation), 충돌 방지, 지도 시각화에 활용
- ROS 2에서는 /map 토픽으로 주로 사용
- 각 셀은 점유 확률을 가짐
---
|------|-------|------|
|상태|	셀 값 (맵 파일)|	확률적 의미|
|Free|	0	|0.0 (장애물 없음)|
|Occupied|	100	|1.0 (장애물 있음)|
|Unknown|	-1	|0.5 (정보 없음)|

---

## 💾 주요 Mapping 패키지
| 패키지          | 설명                        | ROS 2 지원 여부  |
|----------------|----------------------------|----------------|
| `gmapping`     | 2D SLAM, Particle Filter 사용 | ❌ (ROS 1 전용) |
| `slam_toolbox` | 2D SLAM, 지속적인 Mapping 지원 | ✅ (ROS 2 지원) |
| `cartographer` | 2D/3D SLAM 지원, 고성능       | ✅ (Partial)    |

---

## 🎒 2D Lidar 기반 ros2 패키지

## 🔦 slam_toolbox

- ROS 2에서 사용되는 고급 2D SLAM 패키지로, 실시간 지도 작성과 위치 추정을 지원
- 온라인 및 오프라인 모드 모두 가능, 장기적인 맵 관리와 저장 기능을 제공
- LiDAR 센서와 오도메트리 데이터를 활용해 정밀한 Occupancy Grid Map을 생성
- rviz2와 연동해 지도 시각화가 가능, 네비게이션 스택과도 쉽게 통합됨
---
## 🔈cartographer_ros

- Cartographer 로봇 지도 작성 및 위치 추정 시스템을 ROS환경에 통합하기 위한 패키지
- 라이다, IMU, 오도메트리 데이터를 융합해 정밀한 실내외 지도를 빠르게 작성할 수 있음
- Loop Closure와 그래프 최적화로 긴 주행 거리에서도 높은 정확도를 유지
- 주로 자율주행, 로봇 탐사 등에서 고정밀 Mapping과 Localization에 사용

