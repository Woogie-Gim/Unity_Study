# 3D Movement

## Player 생성
- Player 역할을 하는 캡슐 생성
  
![Alt text](<Images/player 1.PNG>)

- 참고) 1인칭 시점을 만들고 싶을 때 카메라를 Player에 상속 시켜 원하는 시점으로 만들 경우 Main Camera의 시점이 1인칭 시점처럼 보일 수 있다

## Player Controller 스크립트

- 움직임 속도 설정 : [SerializeField] 로 private 변수 설정
- SerializeField (데이터 직렬화)를 사용할 경우 private 수준으로 보호가 가능하지만 inspector 창에서 수정이 가능해진다

```C#
[SerializeField]
private float walkSpeed;
```

- Rigidbody를 선언해서 플레이어의 실제 몸을 구현한다고 생각하면 된다
- 혹은 CharacterController 를 통해 움직일 수도 있다
- GetComponent를 통해 Rigidbody 컴포넌트를 내가 선언한 rigidbody에 넣어준다

```C#
// rigidbody를 통해 Player Control
private Rigidbody myRigid;

// Start is called before the first frame update
void Start()
{
    myRigid = GetComponent<Rigidbody>();
}
```

- Move() 함수 선언 후 움직임 구현
- Vertical, Horizontal 입력을 통해 이동 구현
- 3D 공간에선 X, Z축 활용해서 상하좌우 이동
- Y축을 통해 점프 등을 구현 가능

```C#
private void Move()
{
    // W, S, Up, Down 키 입력 => 위쪽 방향키 : 1, 아래쪽 방향키 : -1, 입력 X : 0 reutrn
    float _moveDirZ = Input.GetAxisRaw("Vertical");
    // A, D, Left, Right 키 입력 => 오른쪽 방향키 : 1, 왼쪽 방향키 : -1, 입력 X : 0 return
    float _moveDirX = Input.GetAxisRaw("Horizontal");
}
```

- right (1, 0, 0), forward (0, 0, 1)에 _moveDirZ, _moveDirX 값을 곱해 return 값들을 곱해준 값을 통해 transform position을 변경

```C#
Vector3 _moveHorizontal = transform.right * _moveDirX;
Vector3 _moveVertical = transform.forward * _moveDirZ;
```

- Vector3 _velocity를 선언 해서 한번에 좌표 계산하도록 하고 normalized를 통해 (0.5, 0, 0.5) 합을 1로 만들며 진행 방향은 같게 만든다
- 나중에 1초에 얼마나 이동시킬지 계산하는 등 후속 조치가 편해진다

```C#
Vector3 _velocity = (_moveHorizontal + _moveVertical).normalized * walkSpeed;
```

- rigidbody 를 통해 움직이게 만든다
- transform.position에 선언한 _velocity 값을 더해주는데 단순히 더해주게 될 경우 순간이동 하듯이 움직이는 문제점과 컴퓨터 성능 차이에 따라 움직임이 문제가 생기기 때문에 Time.deltatTime을 곱해줘야 한다
- Time.deltaTime 의 값은 약 0.016

```C#
myRigid.MovePosition(transform.position + _velocity * Time.deltaTime);
```

![Alt text](<Images/player 2.PNG>)

- Rigidbody에서 roatation을 막아 쓰러지는 것을 방지

![Alt text](<Images/player 3.PNG>)

## 달리기
- runSpeed 변수와 applySpeed를 선언하여 applySpeed를 통해 움직임을 제어
- 만약 applySpeed 가 없을 경우 walkSpeed 에 대한 메서드, runSpeed 에 대한 메서드가 따로 있어야 하지만 그냥 applySpeed 에 Speed 를 대입해주면 된다
- 걷는 상태, 뛰는 상태 구분을 위한 boolean 변수도 선언
  
```C#
// 스피드 조정 변수
[SerializeField]
private float walkSpeed = 10.0f;
[SerializeField]
private float runSpeed;
private float applySpeed;

// 상태 변수
private bool isRun = false;
```

- Start() 시 applySpeed = walkSpeed;
- Move() 함수에 applySpeed 적용
- Update() 에  TryRun() 함수를 작성하여 달리기 상태를 파악하고 Move();
- TryRun 에 Shift 키 클릭 시 달릴 수 있도록 설정
- GetKey 를 통해서 누르고 있는동안 달리기 / GetKeyUp을 통해 쉬프트 키를 떘을 때 달리기 해제

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    // 스피드 조정 변수
    [SerializeField]
    private float walkSpeed = 10.0f;
    [SerializeField]
    private float runSpeed = 20.0f;
    private float applySpeed;

    // 상태 변수
    private bool isRun = false;

    // rigidbody를 통해 Player Control
    private Rigidbody myRigid;

    // Start is called before the first frame update
    void Start()
    {
        myRigid = GetComponent<Rigidbody>();
        applySpeed = walkSpeed;
    }

    // Update is called once per frame
    void Update()
    {        
        TryRun();
        Move();
    }
    private void TryRun()
    {
        if (Input.GetKey(KeyCode.LeftShift))
        {
            Running();
        }
        if (Input.GetKeyUp(KeyCode.LeftShift))
        {
            RunningCancel();
        }
    }
    private void Running()
    {
        isRun = true;
        applySpeed = runSpeed;
    }
    private void RunningCancel()
    {
        isRun = false;
        applySpeed = walkSpeed;
    }
    private void Move()
    {
        // A, D, Left, Right 키 입력 => 오른쪽 방향키 : 1, 왼쪽 방향키 : -1, 입력 X : 0 return
        float _moveDirX = Input.GetAxisRaw("Horizontal");
        // W, S, Up, Down 키 입력 => 위쪽 방향키 : 1, 아래쪽 방향키 : -1, 입력 X : 0 reutrn
        float _moveDirZ = Input.GetAxisRaw("Vertical");

        Vector3 _moveHorizontal = transform.right * _moveDirX;
        Vector3 _moveVertical = transform.forward * _moveDirZ;

        Vector3 _velocity = (_moveHorizontal + _moveVertical).normalized * applySpeed;

        myRigid.MovePosition(transform.position + _velocity * Time.deltaTime);
    }

}
```

## 점프
- jumpForce를 선언, 땅에 붙어 있는지 상태확인 isGround 선언
- CapsuleCollider가 땅 meshCollider 가 맞닿아 있을 때 상태 확인을 통해 Jump 기능 구현
- 스페이스바 키를 누르고 (한번 누르면 점프이기 때문에 GetKeyDown) 땅에 닿았을 때 점프 하도록 조건문 작성
- Jump() 함수에서 myRigid 의 속도 rigidbody 자체 속성 값인 velocity를 통해 Y 축 값 이동
- 땅에 붙어있는지 확인하기 위해 IsGround() 함수 작성
- Raycast를 통해 레이저를 발사, Vector3.down을 통해 좌표 값 기준으로 아래로만 레이저 발사, capsuleCollider의 bounds (영역)의 y 값의 extents(반)
- Raycast를 통해서 레이저를 발사하고 땅에 닿아 있는지를 체크 (true를 return)
- 단, 캡슐의 정확히 절반을 줄 경우 계단이나 경사로에서 문제가 생길 수 있으므로 약간의 여유를 주기 위해 capsuleCollider.bounds.extents.y + 0.1f;

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [SerializeField]
    private float jumpForce;

    // 상태 변수
    private bool isGround = true;

    // 캡슐 콜라이더와 맵 meshCollider의 충돌 확인
    private CapsuleCollider capsuleCollider;

    // rigidbody를 통해 Player Control
    private Rigidbody myRigid;

    // Start is called before the first frame update
    void Start()
    {
        myRigid = GetComponent<Rigidbody>();
        capsuleCollider = GetComponent<CapsuleCollider>();
        applySpeed = walkSpeed;
    }

    // Update is called once per frame
    void Update()
    {
        IsGround();
        TryJump();
        TryRun();
        Move();
    }
    private void IsGround()
    {
        isGround = Physics.Raycast(transform.position, Vector3.down, capsuleCollider.bounds.extents.y + 0.1f);
    }
    private void TryJump()
    {
        if (Input.GetKeyDown(KeyCode.Space) && isGround)
        {
            Jump();
        }
    }
    private void Jump()
    {
        myRigid.velocity = transform.up * jumpForce;
    }
}
```