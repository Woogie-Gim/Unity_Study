# 게임 오브젝트 삭제 메소드 Destroy()

## Destroy(Component);

```
== built-in method ==
Destroty(object destroyObject);
destroyObject(게임 오브젝트 or 컴포넌트)를 삭제

Destroy(Object destroyObject, float time);
destroyObject(게임 오브젝트 or 컴포넌트)를 time 시간 뒤에 삭제
```

- Destroy()는 Instantiate()와 반대로 오브젝트를 삭제하는 메소드
- 오브젝트뿐만 아니라 오브젝트에 부착되어 있는 개별 컴포넌트도 삭제가 가능
- (Tip. 게임 진행하는 도중 플레이어의 공격을 받아 사망하는 적 오브젝트, 플레이어와 부딪혀 플레이어가 획득! 하게 되는 아이템 오브젝트와 같이 게임에서 영구적으로 사라져야 할 때 Destroy() 메소드를 이용해 삭제)

![Alt text](<Images/Destroy/destroy 1.PNG>)

- 오브젝트, 컴포넌트 삭제를 제어하는 ObjectDestroyer 스크립트를 생성

![Alt text](<Images/Destroy/destroy 2.PNG>)

- 삭제할 오브젝트를 저장하는 playerObject 변수를 선언하고 Awake() 메소드에서 Destroy(playerObject.GetComponent PlayerController()); 로 playerObject에 있는 PlayerController 컴포넌트를 삭제한다.
- (Tip. 컴포넌트를 삭제할 수 있다는 것을 보여주기 위해 썼지만 그 기능이 다시 필요할 수 도 있기 때문에 일반적으로 GetComponent PlayerController().enabled = false; 코드로 작성해 기능을 잠시 꺼두는 것을 더 권장한다.)

![Alt text](<Images/Destroy/destroy 3.PNG>)

- 빈 오브젝트를 생성하고 이름을 ObjectDestroyer로 설정한 후 ObjectDestroyer 컴포넌트를 추가
- PlayerObject 변수에 Player 오브젝트를 등록

![Alt text](<Images/Destroy/destroy 4.PNG>)

- 게임을 실행하면 Player 오브젝트에 있는 PlayerController 컴포넌트가 삭제된다.

![Alt text](<Images/Destroy/destroy 5_.PNG>)

![Alt text](<Images/Destroy/destroy 5.PNG>)

- ObjectDestroyer 스크립트로 가서 Destroy(playerObject);로 플레이어 오브젝트를 삭제
- 게임을 실행하면 Player 오브젝트가 삭제된다.

![Alt text](<Images/Destroy/destroy 6.PNG>)

- ObjectDestroyer 스크립트로 가서 Destroy() 메소드는 오브젝트를 바로 삭제하는 것도 가능하지만 특정 시간이 지난 후에 삭제하는 것도 가능
- 코드와 같이 매개변수를 두 개 사용해서 두 번째 매개변수에 실수형으로 시간을 작성하면 코드가 실행되고 해당 시간이 지난 후에 오브젝트가 삭제된다.

![Alt text](<Images/Destroy/destroy 7.PNG>)

![Alt text](<Images/Destroy/destroy 8.PNG>)

- 게임을 실행하면 Player 오브젝트가 2초 뒤에 삭제된다.

## 특정 위치에 도착했을 때 오브젝트 삭제
- 게임에서 등장했다가 화면 밖으로 사라지는 적, 장애물, 아이템과 같은 오브젝트 처럼 특정 위치에 도착했을 때 오브젝트가 사라지도록 제작

![Alt text](<Images/Destroy/tracker 1.PNG>)

- 특정 위치. 현재 예제에서는 화면을 벗어난 오브젝트를 삭제하는 PositionTracker 스크립트를 생성

![Alt text](<Images/Destroy/tracker 2.PNG>)

- 화면을 벗어나는 왼쪽 하단 위치 -9.5, -5.5를 min 변수에 오른쪽 상단 위치 9.5, 5.5를 max 변수에 저장

![Alt text](<Images/Destroy/tracker 3.PNG>)

![Alt text](<Images/Destroy/tracker 4.PNG>)

- Update() 메소드에서 이 스크립트를 컴포넌트로 가지고 있는 게임 오브젝트의 x 위치가 min.x 보다 작거나 max.x 보다 크거나 y 위치가 min.y 보다 작거나 max.y 보다 클 때 Destroy(gameObject);로 오브젝트를 삭제

![Alt text](<Images/Destroy/tracker 5.PNG>)

- Square, Circle, Hexagon Flat-Top 프리팹에 PositionTracker 컴포넌트를 추가

![Alt text](<Images/Destroy/tracker 6.PNG>)

- 게임을 실행하면 우리가 설정한 min, max 범위를 벗어나 화면 밖으로 나가는 오브젝트들은 삭제된다.

## 특정 오브젝트와 충돌했을 때 오브젝트 삭제
- 게임에서 플레이어가 아이템을 획득하거나 적에게 발사체를 발사해 피격될 때와 같이 다른 오브젝트와 충돌했을 때 오브젝트가 사라지도록 제작
  
![Alt text](<Images/Destroy/wall 1.PNG>)

- 벽 오브젝트로 사용할 2D Square 오브젝트를 생성하고 이름을 Wall로 설정 ([GameObject - 2D Object -Sprites Square])

![Alt text](<Images/Destroy/wall 2.PNG>)

- 벽과 충돌한 오브젝트를 삭제하는 Wall 스크립트 생성

![Alt text](<Images/Destroy/wall 3.PNG>)

- 게임에서 적이 피격되었을 때 피격되었다는 표시로 색상이 잠깐 변하는 것처럼 벽 오브젝트도 발사체와 충돌했을 때 색상을 잠시 바꿈
- 벽의 색상을 변경하기 위해 spriteRenderer 변수를 선언하고 Awake() 메소드에서 GetComponent로 컴포넌트 정보를 얻어와 저장

![Alt text](<Images/Destroy/wall 4.PNG>)

- 충돌했을 때 1회 호출되는 OnTriggerEnter2D() 메소드에서 Destroy(collision.gameObject);로 발사체 오브젝트를 삭제

![Alt text](<Images/Destroy/wall 5.PNG>)

- 벽에 색상이 잠깐 바뀌는 HitAnimation 코루틴 메소드를 호출

![Alt text](<Images/Destroy/wall 6.PNG>)

- HitAnimation() 코루틴 메소드는 spriteRenderer.color = Color.red; 로 벽의 색상을 빨간색으로 변경하고 yield return new WaitForSeconds(0.1f); 로 0.1초 동안 대기한 후 spriteRednerer.color = Color.white;로 벽의 색상을 다시 하얀색으로 변경

![Alt text](<Images/Destroy/wall 7.PNG>)

- Circle 프리팹에 CircleCollider2D 컴포넌트를 추가해 충돌이 가능하도록 설정

![Alt text](<Images/Destroy/wall 8.PNG>)

- Wall 오브젝트에 Wall 컴포넌트를 추가하고 충돌이 가능하도록 BoxCollider2D, Rigidbody2D 컴포넌트를 추가

![Alt text](<Images/Destroy/wall 9.PNG>)

![Alt text](<Images/Destroy/wall 10.PNG>)

- 중력을 받아 아래로 떨어지지 않도록 Rigidbody2D의 Gravity Scale을 0으로 설정하고 충돌했을 때 OnTriggerEnter2D() 메소드가 호출되도록 BoxCollider2D 컴포넌트의 IsTrigger를 체크

![Alt text](<Images/Destroy/wall 11.png>)

- 게임을 실행하면 발사체가 벽과 충돌하면 발사체 오브젝트는 삭제되고 벽은 잠깐 빨간색으로 바뀌었다가 흰색으로 돌아온다