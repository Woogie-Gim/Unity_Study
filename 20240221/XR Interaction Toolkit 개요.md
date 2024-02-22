# VR Basic

## XR Interaction Toolkit 개요

### VR 플러그인

- Vive Input Utility (공식 바이브 연동 플러그인 / 다른 VR 장비 연동 가능, 업데이트 속도 느림)
- Oculus Integration (공식 오큘러스 연동 플러그인 / 주요 오큘러스 기능들을 활용하기 위해 반드시 Oculus Integration 활용)
- SteamVR Plugin (공식 스팀 VR 연동 플러그인 / Steam에서 VR 장비 연동을 위한 플러그인 / 스팀에 출시하기 위한 / 오큘러스를 사용하기 위해선 오큘러스 설정 프로그램과 스팀 VR 프로그램 모두 실행해야 한다)
- XR Interaction Toolkit (유니티에서 제공하는 기본적인 VR 기능을 스크립트 없이 편하게 구현 / 다양한 VR 장비 손쉽게 연동 가능)

### XR Interaction Toolkit 주요 기능

- HMD, Controller의 위치 / 방향 연동
- 오브젝트와 컨트롤러의 직접적인 상호작용
- 오브젝트와 컨트롤러의 광선을 이용한 간접적인 상호작용
- 가능한 상호작용을 나타내는 시각적인 피드백
- Unity UI와의 인터랙션
  - Button, Dropdown, Slider 등
- 상황에 맞는 오디오 재생 및 햅틱 (진동)
- Unity Evenet 기반의 이벤트 연결
  - Hover, Select, Active 등
- AR Foundation 연동을 통해 AR 오브젝트 배치 및 조작
  - Translate, Rotate, Scale 등

## 유니티 프로젝트 생성 & 설정

### 프로젝트 생성

- 3D (UPR) 템플릿으로 생성

![Alt text](<Images/project 1.PNG>)

- Window - Package Manger - Unity Registry 에서 Input System, XR Interaction Toolkit, XR Plugin Management, Oculus XR Plugin 설치 

- Package Manager - In project 에서 설치 확인

### 프로젝트 설정

- Edit - Project Settings - XR Plug-in Management 에서 Oculus 체크

![Alt text](<Images/project 2.PNG>)

- Player 탭에서 Resolution and Presentation 탭에 Run In Background 체크
  
![Alt text](<Images/project 3.PNG>)

- Package Manager - XR Interaction Toolkit 패키지 - Samples Import

![Alt text](<Images/project 4.PNG>)

- Start Assets - XRI Default Actions 파일 HMD와 왼손, 오른손 컨트롤러의 기본적인 액션이 설정되어 있음

![Alt text](<Images/project 5.PNG>)

- Start Assets의 프리셋 파일들을 모두 Add 하여 컴포넌트를 사용할 때 자동으로 연결되게 설정

![Alt text](<Images/project 6.PNG>)

- Edit - Project Settings - Preset Manager
- Action Based Controller 등에 왼손, 오른손 구분을 위해 오른손 컨트롤러에는 Right, 왼손에는 Left를 입력 하여 각각의 이름에 맞는 게임 오브젝트에서 해당 Component를 사용할 때 자동으로 이름에 맡게 붙도록 설정해놓도록 함

![Alt text](<Images/project 7.PNG>)

- Hierachy 추가에 XR 창이 나오면 알맞게 설정