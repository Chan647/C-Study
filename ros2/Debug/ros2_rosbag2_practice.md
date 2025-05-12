
# 📚 ROS : 2 Rosbag2 실습 

---

## 🧨 Rosbag2 기록 (Record)

```bash
ros2 bag record -o my_bag /topic1 /topic2
```

- `-o my_bag`: 기록 파일 이름을 `my_bag`으로 설정  
- `/topic1`, `/topic2`: 기록할 토픽 지정  
- 예시: Tiago 로봇에서 `/scan`과 `/odom` 토픽 기록

```bash
ros2 bag record -o tiago_bag /scan /odom
```

---

## ✨ Rosbag2 기록 중지

- `Ctrl + C`로 기록 종료  
- 결과 파일은 `my_bag` 폴더에 저장  

---

## 🎉 Rosbag2 재생 (Play)

```bash
ros2 bag play my_bag
```

- 기록된 데이터 재생  
- RViz2와 함께 실행하여 데이터 시각화 가능  

---

## 🎊 Rosbag2 저장 파일 정보 확인

```bash
ros2 bag info my_bag
```

- 저장된 토픽 목록, 메시지 수, 시간 정보 확인  

---

## 🎃 Rosbag2 고급 옵션 예시

### ▶ 반복 재생 (Loop)

```bash
ros2 bag play my_bag --loop
```

### ▶ 속도 조정 (2배속)

```bash
ros2 bag play my_bag -r 2.0
```

### ▶ 특정 시간부터 재생 (초 단위)

```bash
ros2 bag play my_bag --start-offset 5
```
---

- 예시
<img src="rosbag record.png" alt="rosbag record" width="400"/>

