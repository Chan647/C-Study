
# 📚 ROS 2 : SLAM   

---

## 🚀 SLAM (Simultaneous Localization and Mapping) 이란?

- 로봇이 미지의 환경에서 지도를 생성하면서 동시에 자신의 위치를 추정하는 기술
- 다양한 센서 데이터를 활용해 Localization과 Mapping을 동시에 수행
---
### ✅ SLAM 주요 단계  

1. Sensor Data 수집: 라이다, 카메라, IMU, 휠 인코더 등 사용 
2. Feature Extraction: 환경에서 의미 있는 특징 추출 
3. Localization: 현재 위치 추정 (Particle Filter, EKF 등)
4. Mapping: 공간에 대한 지도를 동적으로 작성
5. Loop Closure Detection: 이미 방문한 위치인지 인식하고 맵을 수정
---
## 📐 Coordinates and Transformations  

### ✅ 개념  
-  로봇의 다양한 좌표계 간의 위치와 방향 관계를 정의하고 변환하는 개념
- 예시: `base_link`, `odom`, `map`, `camera_link`  
- 2D Coordinate Frmes, 3D Coordinate Frames 두 종류
  - 2D Coordinate Frame: 평면상에서 위치를 정의하며, x, y 좌표와 회전 각도 θ (theta)로 표현 (주로 map, odom 좌표계에서 사용)
  - 3D Coordinate Frame: 공간상에서 위치를 정의하며, x, y, z 좌표와 회전은 Roll, Pitch, Yaw 또는 Quaternion으로 표현 (주로 base_link, camer_link등에서 사용)
---
### ✅ 주요 좌표계  
| 좌표계 | 설명 |
|--------|------|
| `map` | 전역 좌표계 (Global Map Frame) |
| `odom` | 로봇의 추정 위치 (Local Odometry Frame) |
| `base_link` | 로봇 본체 중심 좌표계 |
| `camera_link` | 카메라 센서 위치 기준 좌표계 |
|`tool0`|	로봇 팔의 말단(엔드이펙터)|
---
## 🧩 2D Lidar Data
- 라이다 센서를 사용해 평면 상의 거리 정보를 측정한 데이터
---
## ✅ 2D Lidar Data 주요 특징
- 측정 방식: 레이저를 360도(또는 특정 각도 범위)로 스캔해, 주변 장애물까지의 거리를 측정.

- 출력 데이터:
  - 거리 (Range): 특정 각도에서의 거리 값 (보통 m 단위)
    - ranges[0] → angle_min 방향에서 측정한 거리 (가장 처음 방향)
    - ranges[1] → angle_min + angle_increment 방향에서 측정한 거리.
    - ranges[n] → angle_min + n × angle_increment 방향에서 측정한 거리
    - 예시 
  - 각도 (Angle): 측정한 방향 (보통 0° ~ 360°)

<img src="slam range.png" alt="slam range" width="400"/>

---
## 📦  동차 좌표계

- 기하학적 변환(이동, 회전, 스케일링)을 행렬 곱셈으로 통일해 표현하기 위한 좌표계
- 일반 3D 좌표에 추가로 w값을 도입해 (x, y, z, w) 형태로 표현하며, w=1이면 위치, w=0이면 방향 벡터를 의미
- 복잡한 변환 연산을 간단하게 행렬 하나로 처리할 수 있음
---
### 📡 변환 종류  
- Translation(이동 변환): x, y, z 방향으로 위치 이동 
- Rotation(회전 변환): Roll, Pitch, Yaw (RPY) 또는 Quaternion으로 표현  
- Combined Transformations(합성 변환) :여러 개의 기하학적 변환(이동, 회전, 스케일링 등)을 순차적으로 적용하여 하나의 최종 변환으로 결합하는 것
---
## 📄 예시

## 🧤 문제 상황

- base_link 프레임: 로봇 중심 좌표계
- base_scan 프레임: 라이다 센서가 장착된 위치, base_link로부터 앞으로 0.2m, 왼쪽으로 0.1m, 높이 0.5m 떨어져 있음
- 목표 지점 (Goal): base_scan 프레임 기준으로 앞쪽 3m, 오른쪽 1m, 높이 0m 위치
  
## 🏏 목표까지의 위치 계산 (base_link 기준)

1. base_scan 위치 (base_link 기준)
\[
\begin{bmatrix} 0.2 \\ 0.1 \\ 0.5 \\ 1 \end{bmatrix}
\]

2. 목표 위치 (base_scan 기준) 
\[
\begin{bmatrix} 3.0 \\ -1.0 \\ 0.0 \\ 1 \end{bmatrix}
\]

3. 변환 행렬 (base_scan → base_link)
\[
T = \begin{bmatrix} 
1 & 0 & 0 & 0.2 \\ 
0 & 1 & 0 & 0.1 \\ 
0 & 0 & 1 & 0.5 \\ 
0 & 0 & 0 & 1 
\end{bmatrix}
\]

4. 최종 계산 (행렬 곱)  
\[
\begin{bmatrix} 
x \\ y \\ z \\ 1 
\end{bmatrix} = T \times \begin{bmatrix} 3.0 \\ -1.0 \\ 0.0 \\ 1 \end{bmatrix} = \begin{bmatrix} 3.2 \\ -0.9 \\ 0.5 \\ 1 \end{bmatrix}
\]

---

## 📡 TF 란?

- ROS에서 로봇의 다양한 좌표계 간의 관계(변환 정보)를 실시간으로 관리하고 제공하는 프레임워크.
- 이를 통해 센서, 로봇 본체, 지도 등의 위치 관계를 쉽게 계산하고 추적할 수 있음

