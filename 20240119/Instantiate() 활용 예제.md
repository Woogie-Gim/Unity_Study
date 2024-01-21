# Instantiate() 활용 예제

## 반복문을 이용해 원하는 개수만큼 오브젝트 생성
- 반복문은 중첩해서 사용할 수 잇기 때문에 맵의 x,y축으로 표현해 오브젝트를 격자 형태로 생성할 수 있다
- 또한 코드의 조건문이 없을 때는 온전하게 채워진 격자 맵을 생성하고 조건문이 있을 때는 조건에 만족하는 부분의 오브젝트가 비워진 형태로 격자 맵을 생성

![Alt text](<Images/Instantiate 활용/반복문 1.PNG>)

- 격자 맵의 y축을 나타내는 외부 반복을 작성하고 격자 맵의 x축을 나타내는 내부 반복을 작성

![Alt text](<Images/Instantiate 활용/반복문 2.PNG>)

- 오브젝트 생성 위치는 new Vector3(-4.5f + x, 4.5f - y, 0); 으로 설정해 x 값이 0부터 9까지 증가할 때 x 위치가 -4.5부터 4.5까지 1씩 증가하고 y값이 0부터 9까지 증가할 때 y위치가 4.5부터 -4.5까지 1씩 감소

![Alt text](<Images/Instantiate 활용/반복문 3.PNG>)

- Instantiate()로 squarePrefab 오브젝트를 position 위치에 생성하고 clone 변수에 방금 생성한 오브젝트 정보를 저장

![Alt text](<Images/Instantiate 활용/반복문 4.PNG>)

- clone.transform.localScale = Vector3.one * 0.95f; 로 생성한 오브젝트의 크기는 (0.95, 0.95, 0.95)로 설정해 오브젝트 사이에 0.05의 간격을 준다.

![Alt text](<Images/Instantiate 활용/반복문 5.PNG>)

- 게임을 실행하면 사각형 오브젝트로 채워진 10 x 10 크기의 격자 맵이 생성된다.

![Alt text](<Images/Instantiate 활용/반복문 6.PNG>)

- 조건문을 작성해 x, y의 특정 값에서는 오브젝트를 생성하지 않도록 한다.

![Alt text](<Images/Instantiate 활용/반복문 7.PNG>)

- 게임을 실행하면 조건에 따라 오브젝트가 비어 있는 10 x 10 크기의 격자 맵이 생성된다.

## 여러 종류의 프리팹 중 임의의 프리팹 생성
- 여러 종류의 프리팹이 필요하기 때문에 추가로 프리팹을 더 생성한다.

![Alt text](<Images/Instantiate 활용/prefab 1.png>)

- 프리팹으로 만들 2D Circle 오브젝트를 생성 ([GameObject - 2D Object - Sprites - Circle])

- Circle 오브젝트를 Project View로 드래그해서 프리팹을 생성하고, Hierarchy View의 Circle 오브젝트는 삭제

![Alt text](<Images/Instantiate 활용/prefab 2.PNG>)

- 프리팹으로 만들 2D Hexagon Flat-Top 오브젝트를 생성 ([GameObject - 2D Object - Sprites - Hexagon Flat-Top])

![Alt text](<Images/Instantiate 활용/prefab 3.PNG>)

- 배열 변수 arrayPrefabs를 선언

![Alt text](<Images/Instantiate 활용/prefab 4.PNG>)

```
== built-in method == 
int reuslt = Random.Rnage(int min, int max);
min ~ max - 1 사이의 정수 중 임의의 정수를 result에 반환

float result = Random.Range(float min, float max);
```

- Random.Range() 메소드를 이용해 0에서 arrayPrefabs.Length-1 중 임의의 숫자를 뽑아 prefabIndex 변수에 저장

![Alt text](<Images/Instantiate 활용/prefab 5.PNG>)

- 위치는 (-4.5f + i, 0, 0)으로 설정

![Alt text](<Images/Instantiate 활용/prefab 6.PNG>)

- Instantiate() 메소드를 이용해 오브젝트를 생성할 때 첫 번째 매개변수에 arrayPrefabs의 prefabIndex번째 방 오브젝트를 생성하도록 한다.

![Alt text](<Images/Instantiate 활용/prefab 7.PNG>)

- ObjectSpawner 컴포넌트의 ArrayPrefabs 변수에 Square, Circle, Hexagon Flat-Top 프리팹을 등록한다.

![Alt text](<Images/Instantiate 활용/prefab 8.PNG>)

- 게임을 실행하면 등록한 세 종류의 프리팹이 랜덤하게 10개 생성된다.

## 임의의 위치에서 원하는 개수만큼 오브젝트 생성

![Alt text](<Images/Instantiate 활용/object 1.PNG>)

- 오브젝트 생성 개수를 나타내는 objectSpawnCount 변수 선언

![Alt text](<Images/Instantiate 활용/object 2.png>)  

- 반복문의 조건을 i < objectSpawnCount 보다 작을 때로 수정하고 x 위치는 Random.Range(-7.5f, 7.5f), y 위치는 Random.Range(-4.5f, 4.5f)로 화면 내부 임의의 위치로 설정

![Alt text](<Images/Instantiate 활용/object 3.png>)

- 게임을 실행하면 objectSpawnCount에 설정된 30개 만큼 오브젝트가 임의의 위치에서 생성된다

## 맵에 배치된 오브젝트의 위치에서 오브젝트 생성
- 게임을 하다보면 SpawnPoint라고 부르는 지정된 위치에서 적이나 아이템과 같은 오브젝트가 생성된다
- 이처럼 맵에 배치된 특정 위치에서 오브젝트를 생성 실습

![Alt text](<Images/Instantiate 활용/spawn 1.PNG>)

- 오브젝트 생성 위치로 사용할 2D Square 오브젝트를 생성하고, ([GameObject - 2D Object - Sprites - Square]) 이름을 SpawnPoint01로 설정

![Alt text](<Images/Instantiate 활용/spawn 2.PNG>)

- SpawnPont01 오브젝트를 Ctrl + D로 복제한 후 이름을 SpawnPoint02로 설정하고, 위치를 (-8, -4, 0)으로 설정

- 화면에 보이는 하얀 오브젝트가 생성 위치(SpawnPoint)로 활용된다 게임의 특성에 따라 생성 위치는 눈에 보일 수도 있고, 보이지 않을 수도 있다
- (Tip. 눈에 보이지 않는 생성 위치를 제작할 때도 개발자가 배치할 때는 위치를 판단해야 하기 때문에 눈에 보이는 오브젝트(2D/3D)를 이용해 배치하고, 배치가 완료되면 "Transform" 컴포넌트를 제외하고 모두 삭제하여 사용한다)

![Alt text](<Images/Instantiate 활용/spawn 3.PNG>)

- 오브젝트가 생성되는 위치 배열 arraySpawnPoints를 선언

![Alt text](<Images/Instantiate 활용/spawn 4.PNG>)

- 현재는 생성 위치가 2개 밖에 없지만 더 많을 수도 있기 때문에 Random.Range(0, arraySpawnPoints.Length)로 작성해 생성 위치가 늘어나더라도 코드는 수정하지 않도록 한다

![Alt text](<Images/Instantiate 활용/spawn 5.PNG>)

- 오브젝트의 생성 위치는 position이 아닌 arraySpawnPoints 배열의 spawnIndex번째 방에 있는 Transform position으로 설정

![Alt text](<Images/Instantiate 활용/spawn 6.PNG>)

- ObjectSpawner 컴포넌트의 ArraySpawnPoints 배열에 SpawnPoint01, SpawnPoint02 오브젝트를 등록한다

![Alt text](<Images/Instantiate 활용/spawn 7.PNG>)

- 게임을 실행하면 두 곳의 생성 위치에서 오브젝트가 생성된다

![Alt text](<Images/Instantiate 활용/spawn 8.PNG>)

- 다만 현재는 오브젝트가 이동하거나 하지 않기 때문에 생성위치에 모두 모여 있다

![Alt text](<Images/Instantiate 활용/spawn 9.PNG>)

- 오브젝트의 이동을 제어하는 Movement2D 스크립트를 생성

![Alt text](<Images/Instantiate 활용/spawn 10.PNG>)

- 이동방향과 이동속도 변수를 선언

![Alt text](<Images/Instantiate 활용/spawn 11.PNG>)

- Update() 메소드에서 transform.position += moveDirection * moveSpeed * Time.deltaTime; 으로 오브젝트를 moveDirection 방향, moveSpeed 속도로 이동하도록 제어

![Alt text](<Images/Instantiate 활용/spawn 12.PNG>)

- 외부에서 호출하는 MoveTo() 메소드는 매개변수로 받아온 direction으로 방향을 설정

![Alt text](<Images/Instantiate 활용/spawn 13.PNG>)

- Square, Circle, Hexagon Flat-Top "프리팹"에서 Movement2D 컴포넌트를 추가

![Alt text](<Images/Instantiate 활용/spawn 14.PNG>)

- ObjectSpawn 스크립트로 가서 Instantiate()로 생성한 오브젝트 정보를 clone 변수에 저장

![Alt text](<Images/Instantiate 활용/spawn 15.PNG>)

- spawnIndex가 0이면 direction을 왼쪽, 0이 아니면 direction을 오른쪽으로 설정

```
삼항 연산자 (?:)
D = A ? B : C;
위의 문장은 아래의 if-else와 동일
if (A) 
{
    D = B;
}
else
{
    D = C;
}
```

![Alt text](<Images/Instantiate 활용/spawn 16.PNG>)

- clone.GetComponent Movement2D ().MoveTo(direction)으로 방금 생성한 오브젝트의 이동 방향을 direction으로 설정

![Alt text](<Images/Instantiate 활용/spawn 17.PNG>)

- 게임을 실행하면 30개의 오브젝트가 동시에 이동하기 때문에 하나의 오브젝트가 움직이는 것 처럼 보인다.

![Alt text](<Images/Instantiate 활용/spawn 18.PNG>)

- 오브젝트를 동시에 생성하지 않고 일정 시간마다 주기적으로 생성 / 기존 Awake() 메소드에 작성했던 오브젝트 생성 코드를 Update() 메소드로 옮겨 수정

![Alt text](<Images/Instantiate 활용/spawn 19.PNG>)

- 이대로 게임을 실행하면 매 프레임마다 오브젝트가 생성되기 때문에 코드를 조금 수정
- 기존과 같이 오브젝트를 objectSpawnCount 개수만큼만 생성할 수 있도록 게임 실행 후 오브젝트를 생성한 개수를 저장하는 currentObjectCount 변수를 선언

![Alt text](<Images/Instantiate 활용/spawn 20.PNG>)

- if 조건문으로 게임 실행 후 오브젝트를 생성한 개수 currentObjectCount + 1이 objectSpawnCount보다 크면 return해서 Update() 메소드를 더 이상 실행하지 않도록 한다.

![Alt text](<Images/Instantiate 활용/spawn 21.PNG>)

- 코드 하단에서 오브젝트가 생성될 때마다 currentObjectCount를 1 증가시킨다.

![Alt text](<Images/Instantiate 활용/spawn 22.PNG>)

- 오브젝트가 너무 빨리 생성되기 때문에 생성 주기를 설정한다.
- 오브젝트의 생성 주기를 계산하는 currentSpawnTime 변수를 선언

![Alt text](<Images/Instantiate 활용/spawn 23.PNG>)

- currentSpawnTime은 매 프레임마다 Time.deltaTime 만큼 더한다.
- 즉, currentSpawnTime 값이 0.5면 0.5초, 1이면 1초가 흘렀다는 뜻

![Alt text](<Images/Instantiate 활용/spawn 24.PNG>)

- if 조건문으로 currentSpawnTime이 0.5f 이상이면 오브젝트 생성 코드를 실행하도록 한다

![Alt text](<Images/Instantiate 활용/spawn 25.PNG>)

- 그리고 오브젝트를 생성했을 때 currentSpawnTime을 0으로 초기화
- 즉, 0.5초마다 한번씩 오브젝트를 생성

![Alt text](<Images/Instantiate 활용/spawn 26.PNG>)

- 게임을 실행하면 0.5초마다 오브젝트가 하나씩 생성되고 생성된 오브젝트가 이동한다.

### 코루틴 메소드를 이용해 주기적으로 오브젝트 생성
- ObjectSpawner Script 수정

![Alt text](<Images/Instantiate 활용/spawn 27.PNG>)

![Alt text](<Images/Instantiate 활용/spawn 28.PNG>)

- Update() 메소드가 아닌 코루틴 메소드를 이용해 주기적으로 오브젝트를 생성할 수도 있다.

## 키 입력으로 원하는 순간에 오브젝트 생성

![Alt text](<Images/Instantiate 활용/키 입력 1.PNG>)

- 비행 슈팅 게임과 같이 플레이어가 원하는 방향으로 오브젝트가 이동하고 플레이어가 원하는 순간에 발사체와 같은 오브젝트를 생성하도록 제작 실습

![Alt text](<Images/Instantiate 활용/키 입력 2.PNG>)

- 플레이어 오브젝트 역할을 하는 2D Capsule 오브젝트를 생성하고 이름을 Player로 설정 ([GameObject - 2D object -Sprites - Capsule])

![Alt text](<Images/Instantiate 활용/키 입력 3.PNG>)

- 플레이어의 이동과 오브젝트 생성을 제어하는 PlayerController 스크립트 생성

![Alt text](<Images/Instantiate 활용/키 입력 4.PNG>)

- 키를 눌렀을 때 생성할 오브젝트 projectilePrefab 변수를 선언하고 플레이어의 이동속도 moveSpeed 변수를 선언

![Alt text](<Images/Instantiate 활용/키 입력 5.PNG>)

- Update() 메소드에서 Input.GetAxisRaw("Horizontal");로 좌/우 이동 값을 받아 x에 저장하고 Input.GetAxisRaw("Vertical");로 위/아래 이동 값을 받아 y에 저장

![Alt text](<Images/Instantiate 활용/키 입력 6.PNG>)

- transform.position += new Vector3(x, y, 0) * moveSpeed * Time.deltaTime; 으로 플레이어 오브젝트를 이동

![Alt text](<Images/Instantiate 활용/키 입력 7.PNG>)

- if ( Input.GetKeyDown(KeyCode.Space) )로 스페이스 키를 눌렀을 때 Instantiate(projectilePrefab);으로 발사체 오브젝트를 생성하고 발사체 오브젝트의 이름을 "Porjectile"로 설정하고, 크기는 0.5, 색상은 빨간색으로 설정

![Alt text](<Images/Instantiate 활용/키 입력 8.PNG>)

- Player 오브젝트에 PlayerControlloer 컴포넌트를 추가하고 ProjectilePrefab 변수에 Circle 프리팹을 등록

![Alt text](<Images/Instantiate 활용/키 입력 9.PNG>)

- 게임을 실행하면 현재 발사체의 생성 위치, 방향 등은 설정하지 않았기 떄문에 스페이스 키를 누를 때마다 발사체가 화면의 중앙에 생성되어 제자리에 있다.

![Alt text](<Images/Instantiate 활용/키 입력 10.PNG>)

- PlayerController 스크립트로 가서 Instantiate()의 두 번째 매개변수로 플레이어 오브젝트 위치인 transform.position을 세 번째 매개변수로 (0, 0, 0) 회전 값을 설정

![Alt text](<Images/Instantiate 활용/키 입력 11.PNG>)

- 게임을 실행하면 이제 플레이어의 현재 위치에 발사체가 생성된다

![Alt text](<Images/Instantiate 활용/키 입력 12.PNG>)

- PlayerController 스크립트로 가서 플레이어의 마지막 이동 방향을 저장하는 lastMoveDirection 변수를 선언

![Alt text](<Images/Instantiate 활용/키 입력 13.PNG>)

- x 또는 y가 0이 아니면 즉, 4방향 중 어떤 방향으로든 움직였다면 lastMoveDirection 변수에 입력한 방향 값을 저장
- 이 값을 저장하기 때문에 마지막에 움직인 방향으로 발사체가 발사된다.

![Alt text](<Images/Instantiate 활용/키 입력 14.PNG>)

- 스페이스 키를 눌러 발사체를 생성할 때 clone.GetComponent Movement2D ().MoveTo(lastMoveDirection); 으로 마지막에 움직인 방향을 발사체의 이동방향으로 설정

![Alt text](<Images/Instantiate 활용/키 입력 16.PNG>)

- 게임을 실행하면 최초 한번도 움직이지 않았을 때는 발사체가 오른쪽 방향으로 이동하고 플레이어가 조금이라도 움직였다면 마지막에 움직인 방향으로 발사체가 이동한다.