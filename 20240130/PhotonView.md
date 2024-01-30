# PhotonView

## PhotonView 컴포넌트
- 포톤네트워크에서 player를 만들어서 동기화 시키기 위해서는 PhotonView 라는 컴포넌트가 필요
- player의 행동은 모두 photonView를 통해서 관찰된 후에 동기화 된다
- 즉 playerA가 이동했을 때 다른 세계(각 컴퓨터)에 있는 playerA 의 clone 들은 photonView를 통해서 이동 명령을 받는 것
- 동기화를 위해서는 photonView가 필수적으로 player의 component로 있어야 된다
- photonView.IsMine : 해당 프로퍼티를 통해 오브젝트가 실제 내(로컬)가 생성한 객체(오리지널)인지 아니면 다른 플레이어 객체인지 판단할 수 있다.

![Alt text](<Images/photon view 1.png>)

![Alt text](<Images/photon view 2.PNG>)

1. Syncronization (동기화 옵션)
   - 동기화 옵션에서는 어떻게 데이터를 동기화 할지를 정한다
   - Off : RPC만 사용할 경우
   - Relable Delta Compressed : 받은 데이터를 비교해 같으면 보내지 않음
   - Unreliable : 게속 보냄, 손실 가능성 있음
   - Unreliable On Change : 변경이 있을 때 계속 보냄
   - *off 이외에는 모두 observed components에 componet가 하나라도 있어야 함

2. Observed Components
   - 동기화 할 컴포넌트를 넣는 곳
   - 즉, 변경된 값 중 동기화할 것을 관찰해서 다른 클론들에게 보내는 곳


## RPC
- RPC (Remote Procedure Call)
- 원격 프로시저 호출은 별도의 원격 제어를 위한 코딩 없이 다른 주소 공간에서 함수나 프로시저를 실행할 수 있게하는 프로세스간 통신 기술
- 원격 프로시저 호출을 이용하면 프로그래머는 함수가 실행 프로그램에 로컬 위치에 있든 원격 위치에 있든 동일한 코드를 이용할 수 있다

![Alt text](<Images/photon view 3.png>)

## Photon Animator View

![Alt text](<Images/photon animator 1.PNG>)

- 애니메이션 네트워크 동기화 위한 컴포넌트
- Disabled : 사용 안함
- Dicrete : 사용

## Photon Transform View
- PhotonView, Photon Transform View를 추가하면 오브젝트의 Position, Rotation, Scale과 같은 값들을 동기화 할 수 있다.