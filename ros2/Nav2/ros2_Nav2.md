
# 📚 ROS 2 : Navigation 2(Nav2)

---

##  🧨 Navigation 2 란??

- ROS 2에서 로봇의 자율 주행, 경로 계획, 장애물 회피, 목표 지점 도달 등을 담당하는 패키지 모음
- 주요 역할
  - 전역 경로 계획 (Global Path Planning)  
  - 로컬 장애물 회피 및 주행 제어  
  - 행동 트리를 통한 목표 지점 도달 관리  

---

## 📌 ROS VS ROS 2 Navigtion Stack  

| 항목                | ROS   | ROS2  |
|---------------------|-------------------------|---------------------------|
| 지원 버전           | ROS Melodic, Noetic 등  | ROS 2 Dashing ~ Humble    |
| 통신 구조           | 주로 Topic, Service     | Topic, Service, Action |
| 아키텍처            | 단일 노드 구조          | 모듈화, 분산 아키텍처      |
| 상태 관리           | 없음                    |Lifecycle 관리 지원    |
| 플러그인 구조        | 제한적                  | 완전한 플러그인 구조    |
| 행동 제어            | 단순 상태 기계 (FSM)    | Behavior Tree (BT)     |
| 미들웨어            | ROS 1 커스텀            | DDS (FastRTPS, Cyclone DDS 등) |

---

## 📖 ROS 2에서 사용되는 주요 개념  

| 개념             | 설명 |
|------------------|------|
| Action Server | 장시간 실행 작업 관리 (예: 목표 지점 이동). 중간 피드백과 취소 가능 |
| Lifecycle Node | 노드의 상태(비활성, 활성, 종료 등) 관리로 안정적인 시스템 운영 지원|
| Behavior Tree | 복잡한 로봇 동작을 트리 구조로 정의하고 관리 |
| Pluginlib   | 다양한 알고리즘(플래너, 컨트롤러 등)을 플러그인으로 교체 가능|
| Costmap 2D    | 2D 그리드 맵으로 장애물과 주행 가능 구역을 관리 |

---

## 🔈 Action Server 란?

- 장시간 실행되는 작업(예: 목표 지점까지 이동)을 관리하는 ROS 2의 통신 메커니즘
- 작업 진행 중에도 피드백(Feedback)을 제공, 필요 시 취소 요청을 받을 수 있음
- 주로 로봇 제어, 네비게이션, 팔 제어 등 복잡하고 시간이 오래 걸리는 작업에 사용됨
- 관련 인터페이스로는 Goal, Feedback, Result가 있고, 클라이언트와 비동기적으로 통신
---
## 🔉 Lifecycle Node 란?

- ROS 2에서 노드의 상태를 명확하게 정의하고, 상태 전환을 제어하여 안정적이고 예측 가능한 시스템을 구현하는 데 사용됨
- 노드의 초기화, 활성화, 비활성화, 종료 과정을 체계적으로 관리할 수 있음
- 
|상태|	설명|
|---|---|
|Unconfigured|	아직 설정되지 않은 초기 상태|
|Inactive	|설정은 되었지만 실행 중이지 않음|
|Active	|정상적으로 실행 중인 상태|
|Finalized	|종료된 상태 (Shutdown)|
|ErrorProcessing	|오류 처리 중 상태|
---
## 🔉 Behavoir Tree 란?

- 로봇의 복잡한 동작과 결정을 트리 구조로 표현하여 유연하고 직관적으로 제어할 수 있는 기법
- Sequence, Fallback, Decorator 등의 노드를 조합해 다양한 상황에 따른 행동 흐름과 복구 전략을 정의
- Nav2에서는 목표 도달, 장애물 회피, 실패 복구 같은 행동을 XML 파일로 쉽게 설계하고 관리할 수 있음

----
## 🗂️ Nav2 : Navigation Servers
- Planner Server
  - Ros에서 Global Planner
  - 로봇이 목표 지점까지 이동할 최적 경로를 생성

- Controller Server
  - Ros에서 Local Planner
  - 로컬 장애물 회피 및 주행 제어 명령을 생성하여 로봇이 안전하게 목표 경로를 따르도록 함

- Smooth Server
  - 전역 플래너가 생성한 경로를 부드럽게 보정해 로봇이 자연스럽게 움직이도록 함
  - 곡선화된 경로로 급격한 방향 전환이나 불필요한 움직임을 최소화
  - 주행 효율성과 안정성을 높이기 위해 플러그인 형태로 다양한 보정 알고리즘을 사용할 수 있음

- Behavior Server
  - Behavior Tree를 이용해 로봇의 복잡한 행동 시퀀스를 관리하고 실행
  - 목표 도달, 장애물 회피, 복구 동작 등 다양한 상황에 맞는 행동을 트리 구조로 처리
  - XML 파일로 트리를 정의하고, 유연한 동작 흐름을 구현할 수 있음

----

## 🗂️ Nav2 : Environmental Representation(환경 표현)

- Costmap
  - 로봇 주행 환경을 격자(Grid) 형태로 모델링한 맵으로, 각 셀에 이동 가능 여부나 위험도를 수치화한 비용(Cost) 값을 저장하는 지도
  - 비용 값이 높을수록 로봇이 해당 영역을 피해야 하며, 장애물, 위험 지역, 안전 거리 등을 반영해 경로 계획과 장애물 회피에 활용됨
  - 주로 Global Costmap과 Local Costmap으로 구분되어 사용됨

- Layer
  - Costmap에서 환경 정보를 세분화하여 표현하는 계층
  - 각 Layer가 개별적으로 장애물, 정적 지도, 인플레이션 등의 정보를 담당
  - 여러 Layer를 조합해 로봇 주행에 필요한 종합적인 환경 정보를 생성

- Costmap Filter
  - Costmap 위에 추가적인 규칙이나 제한 조건을 적용해 로봇의 주행 경로와 동작을 제어하는 기능
  - 특정 구역에서 속도를 제한하거나 접근 금지 구역(Keepout Zone)을 설정할 때 사용됨

---

