# Script Life Cycle

## Life Cycle
- 유니티에서 자신이 제작한 스크립트의 대부분은 "MonoBehaviour"를 상속 받아 만들어진다. (Object > Component > Behaviour > MonoBehaviour)
- MonoBehaviour가 Scene에서 일정한 흐름이 생기고 엔진에서 자동으로 호출해주는 함수들이 생기는 이 패턴의 흐름을 '생명 주기 (Life cycle)' 이라고 한다
- 생명 주기는 사용자가 호출하지 않아도 프로그램의 흐름에 따라 자동으로 호출 된다

![Alt text](<Images/Monobehaviour flow chart.jfif>)

![Alt text](<Images/life cycle 1.png>)

## 첫 번째 씬 로드

![Alt text](<Images/life cycle 2.png>)

- 다음 함수는 씬이 시작할 때 (씬에서 오브젝트마다 한 번)호출 된다

### Awake 
- 이 함수는 항상 Start 함수 전에 호출되며 프리팹이 인스턴화 된 직후에 호출. 게임 오브젝트가 시작하는 동안 비활성 상태인 경우 Awake 함수는 활성화될 때까지 호출되지 않는다.

### OnEnable 
- (오브젝트가 활성화된 경우에만) 오브젝트 활성화 직후 이 함수를 호출.
- 레벨이 로드되거나 스크립트 컴포넌트를 포함한 게임 오브젝트가 인스턴스화 될 때와 같이 MonoBehaviour를 생성할 때 이렇게 할 수 있다

- 씬에 추가된 모든 오브젝트에 대해 Start, Update 등 이전에 호출된 모든 스크립트를 위한 Awake 및 OnEnable 함수가 호출. 
- 따라서 게임플레이 도중 오브젝트를 인스턴스화될 때는 실행되지 않는다

## 에디터

![Alt text](<Images/life cycle 2.png>)

### Reset 
- 오브젝트에 처음 연결하거나 Reset 커맨드를 사용할 때 스크립트의 프로퍼티를 초기화하기 위해 Reset을 호출
  
### OnValidate 
- OnValidate는 오브젝트가 역직렬화될 때를 포함하여 스크립트의 프로퍼티가 설정될 때마다 호출되며 이는 에디터에서 씬을 열 때와 도메인을 다시 로드한 후와 같이 다양한 시기에 발생할 수 있다

## 첫 번째 프레임 업데이트 전에

![Alt text](<Images/life cycle 2.png>)

### Start 
- 스크립트 인스턴스가 활성화된 경우에만 첫 번째 프레임 업데이트 전에 호출

- 씬 에셋에 포함된 모든 오브젝트에 대해 Update 등 이전에 호출된 모든 스크립트를 위한 Start 함수가 호출
  
- 따라서 게임플레이 도중 오브젝트를 인스턴스화될 때는 실행되지 않는다

## 프레임 사이

### OnApplicationPause 
- 이 함수는 일시 정지가 감지된 프레임의 끝, 실질적으로 일반 프레임 업데이트 사이에 호출된다.
- 게임에 일시정지 상태를 가리키는 그래픽스를 표시하도록 OnApplicationPause 가 호출된 후에 한 프레임이 추가로 실행된다

## 업데이트 순서

![Alt text](<Images/life cycle 3.png>)

![Alt text](<Images/life cycle 3_.png>)

- 게임 로직, 상호작용, 애니메이션, 카메라 포지션의 트랙을 유지할 때, 사용 가능한 몇몇 다른 이벤트가 존재한다.
- 일반적인 패턴은 Update 함수에 대부분의 작업을 수행하는 것이지만 사용할 수 있는 다른 함수도 있다

### FixedUpdate
- FixedUpdate 는 종종 Update 보다 더 자주 호출된다
- 프레임 속도가 낮은 경우 프레임당 여러 번 호출 될 수 있으며 프레임 속도가 높은 경우 프레임 사이에 호출되지 않을 수 있다
- 모든 물리 계산 및 업데이트는 FixedUpdate 후 즉시 발생
- FixedUpdate의 움직임 계산을 적용할 때 Time.deltaTime 만큼 값을 곱할 필요가 없다
- FixedUpdate 가 프레임 속도와 관계없이 신뢰할 수 있는 타이머에서 호출되기 때문
- 그러므로 일정한 주기의 Update가 필요한 작업에선 Update 보다 FixedUpdate 가 더 유용하다

### OnTriggerXXX
- 게임 내 Trigger 이벤트 발생 시 호출
- OnTriggerEnter, OnTriggerStay, OnTriggerExit 함수들을 통해 이벤트를 감지할 수 있다

### OnCollisionXXX
- 게임 내 Collision 이벤트 발생 시 호출
- OnCollisionEnter, OnCollisionStay, OnCollisionExit 를 통해 이벤트를 감지할 수 있다

### Update
- Update가 끝난 후 프레임 당 한 번 호출된다.
- 프레임 업데이트를 위한 주요 작업 함수
- 호출시기가 프레임이 영향을 받기 때문에 컴퓨터 성능에 의해 결과가 바뀔 수 있다

### LateUpdate
- Update가 끝난 후 프레임당 한 번 호출
- Update에서 수행된 모든 계산은 LateUpdate가 시작할 때 완료
- LateUpdate는 일반적으로 다음의 3인칭 카메라에 사용한다
- 캐릭터를 움직이고 Update로 방향을 바꾸게 하는 경우 LateUpdate에서 모든 카메라 움직임과 로테이션 계산을 수행할 수 있다

## 오브젝트 파괴할 때

![Alt text](<Images/life cycle 4.png>)

### OnDestroy

- 오브젝트의 존재의 마지막 프레임에 대해 모든 프레임 업데이트를 마친 후 이 함수가 호출된다
- 오브젝트는 Object.Destroy 또는 씬 종료에 대한 응답으로 파괴될 수 있다

## 종료할 때

![Alt text](<Images/life cycle 4.png>)

### OnApplicationQuit
- 이 함수는 애플리케이션 종료 전 모든 게임 오브젝트에서 호출 된다
- 에디터에서 사용자가 플레이 모드를 중지할 때 호출

### OnDisable
- 동작이 비활성화되거나 비활성 상태일 때 이 함수 호출