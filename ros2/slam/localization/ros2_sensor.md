
# 📚 SLAM : 자율주행에 사용되는 센서 

## 📌 Proprioceptive Sensors 
- 로봇 내부 상태(자기 상태)를 측정하는 센서
- 주요 센서:
  - IMU (Inertial Measurement Unit)
    - 설명: 가속도계와 자이로스코프를 사용하여 가속도, 회전율 측정
    - 장점: 고속 반응, 짧은 시간 내 정확한 자세 추정
    - 단점: 장시간 사용 시 드리프트 발생 (누적 오차)
    - 활용 예: Wheel-Inertial Odometry (WIO), LiDAR Inertial Odometry & SLAM 등

  - Encoder (엔코더)
    - 설명: 바퀴 회전수 측정을 통해 이동 거리 계산
    - 장점: 저렴하고 구현이 간단
    - 단점: 슬립 현상, 지면 상태 영향 받음
    - 활용 예: Dead Reckoning을 통해 단일 엔코더 데이터로 로봇 위치 추정
      
  - Wheel Odometry (오도메트리)
    - 설명: 엔코더 데이터를 통해 로봇 위치 추정
    - 장점: 별도 센서 필요 없음, 실시간 위치 추정
    - 단점: 누적 오차 발생, 슬립 시 부정확
    - 활용 예: ROS 2 Navigation Stack에서 초기 위치 추정 및 짧은 거리 내 경로 추적에 활용
---

## 📌 Exteroceptive Sensors 
- 로봇 외부 환경 정보를 인식하는 센서
- 주요 센서:
  - LiDAR (Light Detection and Ranging)
    - 설명: 레이저를 사용해 거리 측정, 2D/3D 맵 생성
    - 장점: 높은 정확도, 긴 거리 탐지, 안정적인 성능
    - 단점: 고가, 악천후에 취약 (비, 안개)
    - 활용 예 : 3D Lidar Odometry & Slam
    
  - Camera (카메라)
    - 설명: 시각 정보를 이용한 특징 추출 및 매핑 (RGB, Stereo, Depth)
    - 장점: 비용 저렴, 풍부한 정보 제공 (색상, 패턴)
    - 단점: 조명, 날씨, 장애물에 민감, 계산량 많음
    -활용 예 : Streo Visual Odometry & Slam , RGB-D Visual Odometry & SLAM 등
    
  - Radar
    - 설명: 전파를 이용해 거리 및 속도 측정
    - 장점: 날씨 영향 적음, 긴 거리 측정
    - 단점: 낮은 해상도, 가까운 거리 측정 성능 낮음
    - 활용 예 : Radar Slam
    
  - Ultrasonic Sensor (초음파 센서)
    - 설명: 초음파를 이용해 거리 측정
    - 장점: 저렴, 간단한 장애물 감지
    - 단점: 짧은 측정 거리, 낮은 정확도
    - 활용 예: LiDAR 기반 SLAM (Cartographer, Hector SLAM), 
      Camera 기반 SLAM (ORB-SLAM, VINS-Fusion), Ultrasonic slam 등


  - GNSS (Global Navigation Satellite System)
    - 설명: GPS, GLONASS, Galileo 등의 위성 신호를 이용해 전 지구적인 위치 정보 제공
    - 장점: 절대 위치 제공, 넓은 지역 커버 가능
    - 단점: 실내, 터널, 도심 캐니언 등에서 신호 불량, 오차 발생 가능
    - 활용 예 : Outdoor Navigation 등 
---

## 📌 Interoceptive Sensors 
- 정의: 로봇 시스템 내부 상태나 자율주행 소프트웨어 상태 측정
- 주요 센서 (주로 소프트웨어 센서):

  - Battery Monitor (배터리 모니터링)
    - 설명: 배터리 잔량, 전압, 온도 등의 내부 상태 측정
    - 장점: 에너지 관리 가능, 시스템 안전성 확보
    - 단점: 센서 고장 시 오작동 가능
    
  - Temperature Sensors (온도 센서)
    - 설명: 전자 부품의 온도를 측정하여 과열 방지
    - 장점: 시스템 보호, 열 관리 가능
    - 단점: 오작동 시 보호 실패


