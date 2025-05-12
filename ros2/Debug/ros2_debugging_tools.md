
# 📚 ROS 2 : 디버깅 도구 


---

## 🛠️  Logger (로거)

- 노드 내부에서 로그 메시지를 출력하는 디버깅 도구  
- DEBUG, INFO, WARN, ERROR, FATAL 단계로 구성
- 실행 중 출력되는 로그로 코드 상태와 오류를 쉽게 파악할 수 있음 
- 로그 레벨은 환경 변수나 코드로 조절할 수 있어 필터링이 가능 

---

## 🔨 RViz2

- ROS 2에서 센서 데이터, 로봇 모델, 경로 등을 시각화하는 툴  
- 로봇 상태와 환경 정보를 직관적으로 확인할 수 있음  
- 3D/2D 뷰를 제공, 디버깅과 개발 테스트에 활용
- 주요 Display Types

|---|---|
|Display Type|	설명|
|RobotModel|	URDF, Xacro로 정의된 로봇 모델을 3D로 시각화|
|TF|로봇의 좌표계 프레임 트리(tf2)를 시각화|
|LaserScan|	라이다, 거리 센서로 수집한 sensor_msgs/LaserScan 데이터를 보여줌|
|PointCloud2|	3D 포인트 클라우드 데이터를 시각화 (sensor_msgs/PointCloud2)|
|Image|	카메라 이미지 토픽(sensor_msgs/Image)을 표시|
|Path|	로봇의 경로 (nav_msgs/Path)를 선으로 표시|
|Marker / MarkerArray|	커스텀 시각적 표시를 위한 마커 데이터 표시 (visualization_msgs/Marker)|
|Map|	2D Occupancy Grid Map (nav_msgs/OccupancyGrid)을 표시|
|Odometry|	로봇의 위치와 방향 정보를 화살표로 시각화 (nav_msgs/Odometry)|
|Range	|초음파, 적외선 거리 센서 데이터를 원으로 표시|
|Wrench	|힘과 토크 데이터를 시각화 (geometry_msgs/Wrench)|
|Grid|	기준 평면 그리드를 표시하여 공간 감각을 제공|
|Axes|	좌표축을 표시해 위치와 방향을 쉽게 파악할 수 있게 함|
|InteractiveMarkers|	RViz에서 직접 마커를 조작할 수 있게 해줌 |

---

## 🎲 RQt

- ROS 2용 GUI 기반 플러그인 툴  
- 토픽, 서비스, 액션, 파라미터 등을 시각적으로 모니터링하고 조작할 수 있음  
- 다양한 플러그인을 통해 시스템 상태를 한눈에 파악할 수 있음
- 주요 플러그인
|------|-------|	
|플러그인 |	설명|
|rqt_graph|	노드와 토픽 간의 통신 구조를 그래프로 시각화|
|rqt_plot|	토픽에서 퍼블리시되는 수치 데이터를 실시간 그래프로 플롯|
|rqt_console|	ROS 로그 메시지를 실시간으로 모니터링하고 필터링할 수 있음|
|rqt_logger_level|	실행 중인 노드의 로깅 레벨을 동적으로 변경할 수 있음|
|rqt_reconfigure|	노드의 파라미터 값을 실시간으로 조정할 수 있음|
|rqt_tf_tree|	TF 프레임 트리를 트리 구조로 시각화|
|rqt_image_view|	토픽으로 퍼블리시되는 이미지 데이터를 확인할 수 있음|
|rqt_bag	|rosbag2로 저장된 데이터를 재생하고 분석할 수 있음|
|rqt_service_caller|	서비스 요청을 GUI로 전송하고 응답을 확인할 수 있음|
|rqt_topic|	토픽 정보를 모니터링하고 퍼블리시/서브스크라이브 테스트를 할 수 있음|

---

## 🎰 Rosbag2

- ROS 2에서 토픽 데이터를 기록(Record)하고 재생(Play)하는 도구  
- 로봇 동작 중 수집한 데이터를 나중에 재현하거나 분석할 수 있음  
- 시뮬레이션 반복 실험, 테스트 자동화, 디버깅에 유용  
- 다양한 스토리지 백엔드(SQLite3, YAML 등)을 지원함 
- ros 와  ros2 간 로깅 파일은 호환되지 않음(변환 과정 필요)
- 주요기능
  - 데이터 기록/재생
  - 데이터 필터링 

---

## 📣 ROS 2 Doctor (`ros2 doctor`)

- ROS 2 시스템 상태를 진단하고 문제를 확인하는 명령어  
- 네트워크 상태, 환경 변수, 노드 상태 등을 자동으로 검사 
- 시스템 설정 오류나 통신 문제를 빠르게 찾아낼 수 있음
- 문제 해결 가이드를 함께 제공해 디버깅을 쉽게 도와줌


