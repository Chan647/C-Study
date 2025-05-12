
# 📚 ROS 2 : RQt 실습 

---

## 🧨 Tiago 시뮬레이션 환경 실행

```bash
source ~/tiago_public_ws/install/setup.bash 
ros2 launch pal_gazebo tiago_gazebo.launch.py
```

---

## 🎍 RQt 실행

```bash
rqt
```

---

## 🎇 Rqt - Plugins

- Configuration - Dynamic Reconfigure
   - RQt 상단 메뉴 → Plugins → Configuration → Dynamic Reconfigure
   - Tiago 로봇에서 동적 파라미터 조정 (예: PID 게인, 속도 제한)  
   - 실시간으로 로봇 반응성 테스트 및 조정  

- Introspection - Node Graph
  - RQt 상단 메뉴 → Plugins → Introspection → Node Graph
  - Tiago 로봇의 현재 실행 중인 노드 구조와 관계 시각화  
  - 토픽, 서비스, 액션 인터페이스를 직관적으로 파악  

- Services - Service Caller
  - RQt 상단 메뉴 → Plugins → Services → Service Caller
  - 예시: `/controller_manager/switch_controller` 서비스 호출  
  - GUI를 통해 서비스 요청과 응답을 직관적으로 테스트  

- Topics - Message Publisher
  - RQt 상단 메뉴 → Plugins → Topics → Message Publisher 
  - 예시: `/cmd_vel` 토픽에 직접 속도 명령 퍼블리시  
  - Tiago 로봇을 직접 움직여 주행 테스트 가능  

- Topics - Topic Monitor
  - RQt 상단 메뉴 → Plugins → Topics → Topic Monitor
  - 관심 있는 토픽 데이터 모니터링 (예: `/scan`, `/odom`, `/joint_states`)  
  - 데이터 주기, 퍼블리시 상태, 값 변화를 실시간 확인  

- Visualization - Image View
  - RQt 상단 메뉴 → Plugins → Visualization → Image View  
  - 카메라 토픽 (`/camera/image_raw`) 데이터 실시간 확인  
  - 영상 데이터가 정상적으로 퍼블리시 되는지 검증  

- Visualization - Plot
  -  RQt 상단 메뉴 → Plugins → Visualization → Plot
  - 예시: `/scan/ranges[0]` 라이다 데이터 실시간 그래프 플롯  
  - 센서 데이터의 노이즈, 변화 패턴 확인  
---

- 예시(Plot) 

<img src="rqt plot.png" alt="rqt plot" width="400"/>

---

- 예시(Image View)

<img src="rqt robot.png" alt="rqt robot" width="400"/>


<img src="rqt image.png" alt="rqt image" width="400"/>