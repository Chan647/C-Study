
# 📚 ros 2 : Costmap & Layer 실습

---

## 🧨 실습 목표

- 저장된 지도를 활용하여 Navigation2 Stack에서  
  - Global Costmap  
  - Local Costmap  
  - Layer 설정  

---


##  🔔 시뮬레이션 실행

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

---

## 🔬 Navigation2 Stack 실행 

```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py 
use_sim_time:=true map:=/home/chan/map/my_map.yaml
```

---
### 📌 RViz2 Display 추가
- Global Costmap
- Local Costmap
- Map
- LaserScan
- TF

---

## 📢 RViz2에서 Costmap 확인

- glboal costmap :

<img src="global costmap.png" alt="global costmap" width="400"/>

- local costmap :

<img src="local costmap.png" alt="local costmap" width="400"/>


## 🎉 RQt를 사용한 Layer 설정 실시간 수정

### 📌 RQt 실행

```bash
rqt
```

### 📌 Dynamic Reconfigure 플러그인 사용

- RQt 메뉴 → Plugins → Configuration → Dynamic Reconfigure 선택  
- 목록에서 global_costmap, local_costmap 선택
- Costmap 및 Layer 관련 파라미터 실시간 수정:
    - `obstacle_layer` 활성/비활성화  
    - `inflation_layer` 활성/비활성화  

- 예시(inflation_layer 비활성화)

<img src="rqt plugin.png" alt="rqt plugin" width="400"/>

- 결과 :

<img src="layer unable.png" alt="layer unable" width="400"/>



