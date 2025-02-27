# 13-19팀 시스템 설계도

#### 팀원 : 남궁민,남동진,남윤호,최영서,최유진,최재완,최제인,김현종

## 주제 : 자율주행

## 서비스 설명

자율주행 서비스란 운전자 또는 승객의 조작 없이 자동차 등의 물체가 스스로 운행이 가능하도록 해주는 서비스를 말한다. 이는 단순히 교통에 국한되는 서비스가 아닌 우리의 일상생활에도 지대한 영향을 끼치는 기술로 만약 무거운 캐리어가 내가 끌지않아도 옆에서 졸졸 따라온다면? 인건비가 걱정인 점주가 자동으로 서빙을 해주는 카트를 사용한다면 ? 이런 예시를 해결해주는것이 자율주행 서비스이다.

해당 서비스는 어느 영역에서는 완전한 자동화를 이루어내지 못했지만 기술에 발전에 따라 무궁무진한 활용처가 예상되는 서비스이다. 자율주행 서비스에 필요한 기술로는 '측위','인지','판단','제어' 에 관련된 기술들이 필요하다.

측위는 차가 도로 위 어디에 위치해 있는지를 계산하는 기술이다. 대중적으로 잘 알려진 GPS를 이용하는 기술이며 인지는 카메라, 레이더 등 정밀 센서로 차량 혹은 주행체의 주변 상황을 감지하는 기술이며 판단은 인지 기술로 취합된 데이터를 분석해 어디로 가야 하는지, 지금 멈춰야 하는지, 신호등 앞에서 어떻게 해야 하는지 등을 결정하는 기술이다. 측위와 인지를 거쳐 판단까지 내렸으면 주행체를 움직이게 하는 하드웨어에 명령을 내리게 되는데, 그게 마지막 기술인 제어이다.

## 유사 서비스 분석

자율주행 서비스는 광범위한 영역에 사용 가능하다. 자율 주행이 가장 기대받는 분야는 자동차와 관련되어 있지만 소소한 분야에서도 많은 활용이 가능하다. 실제로 현재 서비스되는 분야가 실내 음식점의 서빙이다. 술집이나 음식점 등에서 자동으로 움직이는 카트가 정해진 번호의 테이블에 가서 서빙을 해주고 제자리를 찾아가는 것도 자율주행 서비스의 일종이다. 이런 작은 분야의 서비스에도 '경로 설정','장애물 인지' 등의 기술들이 필요하며 이는 다른 자율주행 서비스에도 필수적인 기술들이다.

## Open Source

1. **차선 감지 오픈소스 - 최제인**

- 설명: tensorflow를 사용하여 IEEE IV 회의 논문 "Towards End-to-End Lane Detection: an Instance Segmentation Approach"를 기반으로 실시간 차선 감지를 위한 심층 신경망을 구현 (https://github.com/MaybeShewill-CV/lanenet-lane-detection)
  \*license : **Apache License Version 2.0**, January 2004 (http://www.apache.org/licenses/)

2. **장애물 인지 모듈(apollo) - 최재완**

- 설명

  - 라이다, 카메라 및 레이더와 같은 다양한 센서는 차량을 둘러싼 주변 데이터를 수집한다. 센서 융합 기술 인식 알고리즘을 사용하면 도로에 있는 물체의 유형, 위치, 속도 및 방향을 실시간으로 결정할 수 있다.
  - 인지 시스템은 바이두의 빅 데이터와 딥 러닝 기술뿐만 아니라 방대한 실제 운행 데이터에 근거한다. 대규모 딥 러닝 플랫폼과 GPU 클러스터는 대량의 데이터에 대한 학습 시간을 크게 단축한다.
  - 학습이 완료되면 클라우드를 통한 공중파 업데이트를 통해 새로운 모델이 차량에 적용된다.
  - 인공지능과 데이터 중심 솔루션이 결합되어 아폴로의 인지 시스템이 탐지 및 인지 능력을 지속적으로 향상시킬 수 있으며, 이는 다른 자율 시스템 모듈에 정확하고 안정적이며 신뢰할 수 있는 인풋 데이터를 제공한다.
    <br>

- 역할 : 인지

  - 인지 모듈은 여러 카메라, 레이더(전면 및 후면) 및 LiDAR를 사용하여 장애물을 인식하고 개별 트랙을 융합하여 최종 트랙 영상을 얻는 기능을 포함한다. 장애물 하위 모듈은 장애물을 감지, 분류 및 추적한다. 이 하위 모듈은 또한 장애물 움직임 및 위치 정보(예: 방향 및 속도)를 예측한다.
  - 카메라와 레이더, 라이다의 이미지, 영상 데이터를 받아 3D 장애물 트랙으로 출력이 가능하다.
    <br>

- 라이선스

  - **Apache License 2.0**
  - [라이선스 고지 사항](https://github.com/ApolloAuto/apollo/blob/master/LICENSE)
    <br>

3. **Autoware-남윤호**

- Autoware는 3차원 맵과 라이더 센서를 이용한 자차 위치 추정, 라이더 또는 카메라 기반 장애물 탐지, 벡터 맵 기반 경로 계획, 경로 추종 등 자율주행 S/W의 핵심 기능들을 제공한다.
- 자차 위치 추정은 GPS와 라이다 센서를 함께 사용함으로써 센티미터 수준의 정밀도를 제공한다.
- 장애물 탐지는 객체 탐지와 객체 추적으로 구성된다. 자차 주변에 존재하는 장애물들의 위치와 크기를 파악해야만 뒤에서 설명할 주행 상태 기계가 주행을 위해 계획된 후보 궤적들 중에서 어느 궤적을 선택할지 결정할 수 있다.
- 경로 계획은 전역적 계획과 지역적 계획으로 나뉜다. 전역적 계획은 벡터 맵, 시작 포즈, 목표 포즈를 입력받아 주행 기준이 되는 기준 경로를 계산한다. 지역적 계획은 기준 경로를 입력받아 기준 경로와 평행한 여러 개의 후보 궤적들을 미리 생성하는 것이다.
- 경로 추종은 경로 계획 모듈이 제공한 최종 궤적을 작은 시간 단위들로 나누어 차량이 안정적으로 추종하기 위한 타겟 속도와 타겟 조향 각속도를 계산한다.

- Autoware는 20개 이상의 차량 모델들에 이식 되었고, 30개 이상의 국가들, 100개 이상의 회사들에 의해서 폭넓게 사용되고 있다.
- 현재 Autoware 소스코드는 나고야 대학에서 TIER IV라는 회사를 거쳐 Autoware Foundation이라는 비영리 기관으로 이관해서 관리되고 있다.
- 이 오픈소스에서 사용되는 라이선스는 **Apache License 2.0**이다.

4. **비상 정지 신호 (Project Aslan)-김현종**

- 설명: 
- **로봇 운영체제(ROS)** 프레임 워크 기반 오프소스이며 **Gazebo**(물체 회피 및 컴퓨터 비전 테스트에 적합한 3D 시뮬레이션 환경)이 내장되어 있다
- **Ubuntu**와 **ROS Melodic** 사용환경이 갖춰져야 사용 가능하며 **비상정지 신호** 외에도 여러 개선사항에 대해 연구 개발이 진행 중이다.
- **Aslan**의 **비상정지 신호**는 지정 경로 주행 중 실행된다. 자동 주행 차량이 지정된 경로로 주행 중에는 항상 차량의 모션 카메라로 주변의 장애물을 탐지하며 **장애물 감지 소프트웨어**와 연계하여 장애물과의 거리가 빠르게 좁혀지거나 갑작스러운 장애물의 출현을 통해 반응하도록 설계되어 있다.
  **비상 정지 신호** 기능은 해당 기능이 동작할 경우 즉각적으로 차량 관제 시스템에 메시지를 보내 속력을 32.4 km/h로 제한되도록 한다.
- 역할 : 판단
  - 인지부에서 전달받게되는 정보(장애물 정보, 신호등 정보 등)를 분석하여 정지신호를 제어부에 보낼 지 판단 하게된다.
  - 전달되어지는 정보는 매우 빠른 속도록 계산에 들어가며 본 오픈소스는 이용자의 안전을 위한 안정성 향상을 최우선으로 생각해 빠른 정지신호를 발생하도록 한다. 

- 라이센스 : **Apachi License 2.0**

5. **DBSE-monitor-최유진**

- 설명:
- DBSE-monitor는 운전 중에 졸려서 졸음운전을 하거나 딴짓을 할때 경고해주는 시스템이다.
- Jetson Nano를 이용하여 카메라를 통해 운전자의 상태를 파악하고졸거나 운전에 집중하지 못하고 산만한 상태일 때 시각 또는 청각 신호를 통해 운전자에게 알린다. 이 시스템은 졸음 감지, 감정 감지, 드라이빙 모니터 모듈로 구성되어 있다.
- 졸음 및 감정 감지 모듈은 운전자의 얼굴 인식을 위해 OpenCV의 Haar Cascades방식을 사용한다. 시스템이 운전자의 얼굴을 감지하면 모듈은 Jetson Nano에서 실행되는 PyTorch 기반 신경망을 통해 운전자의 눈 상태와 감정 상태를 판단한다.
- altaga/DBSE-monitor(https://github.com/altaga/DBSE-monitor)
- 이 오픈소스에서 사용되는 라이선스는 MIT License이다.

6. **PACmod3 - 남동진**

- 설명: 자동차를 운행하기 위해서는 핸들을 돌리거나, 페달을 밟는 **유압 신호**를 이용하여 자동차를 제어해야 한다. 그러나 자율주행차의 운행을 위해서는 유압신호대신 **전기신호**를 통해 자동차를 이동시켜야한다. 이를 **drive-by-wire**라고 하는데, PACmod3는 이를 구현한 것이다. PACmod3는 로봇운영체제인 **ROS**로 drive-by-wire를 구현한다.
- 라이센스 : **MIT license**
- 주소: https://github.com/astuff/pacmod3

7. **적응식 정속주행 시스템(comma.ai openpilot) - 남궁민**

- 설명: 오픈파일럿은 콤마에이아이의 인공신경망 기반 ADAS 소프트웨어이다. 오픈 파일럿의 기능은 ACC(Adaptive Cruise Control), ALC(Automated Lane Centering), FCW(Forward Collision Warning), LDW(Lane Departure Warning) 및 DM(Driver Monitoring) 기능을 수행한다. 그 중 **ACC(Adaptive Cruise Control)**기능은 적응식 정속 주행 시스템으로 센서를 이용해 전방을 주행하는 자동차와 그 자동차의 주행 속도를 감지한다. 주행 모드로는 선행 주행모드(clear driving mode)와 추종 주행모드(following driving mode) 이 두가지 모드로 주행한다.
- 라이센스: **MIT License**
- https://github.com/commaai/openpilot

8. **객체 감지 알고리즘 모델(YOLO)-최영서**

- 설명: YOLO는 You only Look Once의 약자로 사람이 사진이나 풍경을 보고
  내가 관심있는 물체가 어디어디에 있는지를 단번에 파악해 내는데에 목적이 있다.
  우리가 눈으로 객체 종류, 위치나 갯수를 확인하는 데 필요한 모든 부분에 사용된다.
  주어진 이미지를 한번의 스캔으로 객체의 특징과 경계선을 계산한다.
  차량 교통신호 인식 성능을 비교 및 분석하였다. YOLO네트워크를 사용하여
  신호등을 감지하고 분류하고, 이후 부정확한 제안을 제거한 후 신후등 인식을 위해
  네트워크 결과를 조정하여 신호등 정보를 인식하였다.
- 라이센스 GNU General Public License v3.0
- 출처:https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002856505

## DFD

<img src="dfd.png">
