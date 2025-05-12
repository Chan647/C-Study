
# 📚 ROS 2 : 지도 수정 및 사용


---

## 🔔지도 수정

## 🌞 이미지 파일 직접 수정 
- 저장된 지도는 보통 .pgm 이미지로 저장됨,이 파일을 그래픽 툴로 직접 편집할 수 있음
  - 사용 툴: GIMP, Photoshop, Paint 등
- 색상 기준:
  - 검은색(0): 장애물
  - 흰색(255): 자유 공간
  - 회색: 확률적 미확정 

---
## 🌝 ROS 2에서 지도 재작성 

- 기존 지도를 로드하고 추가 매핑을 진행할 수 있음
- slam_toolbox의 continue mapping 기능 사용

```bash
ros2 launch slam_toolbox online_async_launch.py \
    params_file:=<path_to_params.yaml> \
    slam_toolbox/initial_state_file:=/path/to/existing_map.pgm
```
---

## 🎓 지도를 다른 프로세스에서 사용하는 방법

## 📼 Map Server 
- 역할: 저장된 맵 파일(.yaml, .pgm)을 읽어 ROS 2 시스템에 /map 토픽으로 퍼블리시
- 실행 예시:

```bash
ros2 run nav2_map_server map_server --ros-args -p yaml_filename:=/home/chan/map/my_map.yaml
```
- 노드 이름: map_server
- /map 토픽을 퍼블리시해 Localization 노드가 맵 데이터를 활용할 수 있도록 함
---
## 💽 Lifecycle Manager
- 역할: Navigation 관련 노드들의 생명주기 상태 관리를 담당
- ROS 2에서는 Managed Lifecycle을 사용하여 노드 상태를 unconfigured → inactive → active로 명시적으로 전환해야 함
- Lifecycle Manager가 없으면 map_server 같은 노드가 inactive 상태에 머물러 있어 맵 퍼블리시가 되지 않음
- 실행 예시:

```bash
ros2 run nav2_lifecycle_manager lifecycle_manager --ros-args \
    -p autostart:=true -p node_names:="[map_server]"
```
- 위 명령으로 map_server 노드를 자동으로 active 상태로 전환
---
## 🔮 Lifecycle 이란??
- ROS 2 노드의 상태를 체계적으로 관리하는 기능
- 노드는 unconfigured → inactive → active → finalized 등의 상태로 전이하며, 각 상태에서 수행할 작업을 명확히 구분할 수 있음
- 이를 통해 시스템 안정성, 자원 관리, 노드 제어를 효율적으로 수행할 수 있음

