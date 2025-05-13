
# 📚 ROS 2 : Odometry 및 2D Lidar 기반 알고리즘

---

## 📣 Odometry 란?

- 로봇이 이동 중 자신이 얼마나, 어디로 움직였는지 추정하는 기술
- ROS 2에서는 주로 휠 인코더, IMU, LiDAR 센서를 이용해 상대적인 위치(Position)와 자세(Orientation)를 계산
- 주로 TF 트리의 odom → base_link 변환을 통해 로컬 위치 정보를 제공
- 오도메트리는 로봇의 이동을 기반으로 위치를 추정하지만, 시간이 지날수록 누적 오차(드리프트)가 증가하는 한계가 있음
이를 보완하기 위해 SLAM, GPS, LiDAR, 비전 센서 등 추가적인 센서 데이터를 활용한 보정이 함께 사용됨
  - Wheel Odometry, Wheel Inertial Odometry, GNSS Odometry 등
---



## 🎨 TF 좌표 변환 관계
- `map` → `odom` → `base_link`
- Odometry는 보통 `odom → base_link` 변환을 담당하여 로컬 위치 추정에 사용

---

## 🎮 2D Lidar 기반 알고리즘

## 📌 SLAM (Simultaneous Localization and Mapping)
- 설명: 2D LiDAR 스캔 데이터를 이용해 미지의 환경에서 로봇의 위치를 추정하고 지도를 동시 작성

- 대표 알고리즘:

  - GMapping (Particle Filter 기반 2D SLAM)
  - Hector SLAM (IMU 없이 LiDAR만 사용)
  - Cartographer (Google에서 개발, 루프 클로저 강력)
  
---
## 📌 Localization (위치 추정)
- 설명: 이미 만들어진 지도에서 2D LiDAR 스캔 데이터를 사용해 현재 위치 추정

- 대표 알고리즘:

  - AMCL (Adaptive Monte Carlo Localization) 
    - 파티클 필터를 이용해 위치 추정.
---

## 📌 Obstacle Detection & Avoidance (장애물 감지 및 회피)
- 설명: LiDAR 스캔 데이터를 이용해 근처 장애물을 탐지하고 충돌 방지

- 활용:
  - 범위 기반 장애물 감지 (e.g., 특정 거리 이하 값 필터링)
  - Artificial Potential Field, 벡터 필드 히스토그램(VFH) 같은 회피 알고리즘 적용
---
## 📌 Path Planning (경로 계획)
- 설명: 2D LiDAR로 인식한 장애물 정보를 기반으로 최적 경로 생성

- 대표 알고리즘:
  - Dijkstra, A*, DWA (Dynamic Window Approach)
  ---
  
## 🛠️ 2D Lidar 기반 알고리즘의 핵심

## 🎠 ICP(Iterative Closest Point)
- 두 점군(Point Clouds) 간의 최적의 정합(Alignment)을 찾는 알고리즘
- 2D LiDAR에서는 현재 스캔과 이전 스캔 데이터를 정렬해 로봇의 움직임(변환)을 계산
- Association, Transformation, Error Evaluation 3 단계를 반복적으로 수행
- 입력
  - Source Point Cloud: 현재 시점에서 수집된 LiDAR 스캔 데이터
  - Target Point Cloud: 기준이 되는 이전 시점의 LiDAR 스캔 데이터 
  - 초기 추정 변환 (Optional): 초기 위치 추정 값 
- 출력
  - 변환 행렬 (Transformation Matrix): 소스 포인트 클라우드를 Target에 정렬하기 위한 최적의 회전(R)과 이동(T) 정보
  - 정합 오차 (Fitness Score): 정합의 품질을 나타내는 값







