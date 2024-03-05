# Transform

## Player

![Alt text](<Images/transform 1.PNG>)

- Player 에셋 씬에 배치 후 Player Controller 스크립트 생성

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    void Start()
    {
        
    }
    void Update()
    {
        
    }
}
```
- 움직임을 주기 위해 Transform에 접근
- 컴포넌트 부모의 transform에 접근 하기 위해 찾는 과정이 필요하지만 transform의 경우 자주 사용하기 때문에 함수가 존재

![Alt text](<Images/transform 2.png>)

- Vector 값을 바꿔 위치 이동을 키 입력을 통해 위치 이동

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    void Start()
    {
        
    }
    void Update()
    {
        if (Input.GetKey(KeyCode.W))
        {
            transform.position += new Vector3(0.0f, 0.0f, 1.0f);
        }
        if (Input.GetKey(KeyCode.S))
        {
            transform.position -= new Vector3(0.0f, 0.0f, 1.0f);
        }
        if (Input.GetKey(KeyCode.A))
        {
            transform.position -= new Vector3(1.0f, 0.0f, 0.0f);
        }
        if (Input.GetKey(KeyCode.D))
        {
            transform.position += new Vector3(1.0f, 0.0f, 0.0f);
        }
    }
}
```

![Alt text](<Images/transform 3.PNG>)

- Update에 이동 동작을 입력하여 프레임 단위로 이동하기 때문에 비정상적으로 빠르게 이동한다
- 이전 프레임과 지금 프레임의 시간 차이를 구해서 동작을 하게 해야 한다.
- Time.deltatime을 곱해서 작성한다

![Alt text](<Images/transform 4.png>)

- 대신 속도를 처리해주지 않아 굉장히 느리게 움직인다
- float speed 변수를 통해 속도를 처리
- public으로 선언하여 컴포넌트 자체에서 수정 가능 혹은 speed 같은 값은 private로 선언 해야 하므로 [SerializeField]로 선언 해도 됨

```C#
public float _speed = 10.0f;

[SerializeField]
float _speed = 10.0f;
```

![Alt text](<Images/transform 5.PNG>)

- SerializeField 는 스크립트에서 private 필드를 직렬화하기 위해 사용

- 직렬화는 개체의 상태를 나중에 저장, 전송 또는 재구성할 수 있는 형식으로 변환하는 프로세스
- 유니티에서 직렬화는 게임 상태를 저장 및 로드하거나 에디터와 런타임 간에 데이터를 전송하는 데 사용

- Vector3 예약어를 통해서 포지션을 변경 할 수도 있다 (forward, back, left, right 등)

![Alt text](<Images/transform 6.png>)

![Alt text](<Images/transform 7.png>)

![Alt text](<Images/transform 8.png>)

![Alt text](<Images/transform 9.png>)

## Transform component

![Alt text](<Images/transform 10.PNG>)

### Scale

- 각 축으로 확대 혹은 축소를 시켜준다

![Alt text](<Images/transform 11.PNG>)

### Position

- X, Y, Z 좌표를 변경 시켜 오브젝트의 위치를 변경한다

### Rotation

- degree angle과 같다
- 예를 들어 Y 축의 값을 변경 시킬 떄 Y축을 고정 시키고 회전 시킨다

![Alt text](<Images/transform 12.PNG>)

- 단 로테이션을 돌리게 됐을 경우 플레이어 기준으로 바라본 로컬 좌표계에선 앞 방향이 바뀌지만 글로벌 좌표계에선 바뀌지 않는다
- X 키를 눌러 로컬 좌표계와 비교해가면서 사용하면 된다

- 로컬 좌표 : 오브젝트가 바라보는 좌표계

![Alt text](<Images/transform 14.PNG>)

- 글로벌 좌표 : 유니티의 가상 공간의 기준 좌표

![Alt text](<Images/transform 13.PNG>)

- 실제 오브젝트가 바라보는 좌표로 이동을 시키고자 할 때 TransformDirection을 활용하여 포지션을 변경 한다. (기본적으로 글로벌 좌표 기준으로 포지션을 변경한다)

![Alt text](<Images/transform 15.png>)

![Alt text](<Images/transform 16.PNG>)

- 혹은 Translate를 활용해서 오브젝트가 바라 보고 있는 좌표를 기준으로 연산을 할 수 있다

![Alt text](<Images/transform 17.png>)

## Vector3

![Alt text](<Images/vector 1.PNG>)

![Alt text](<Images/vector 3.PNG>)

### 위치 벡터

- 유클리드공간에서 위치벡터(position vector)는 좌표의 원점 O을 처음 점으로 공간 내의 임의의 한 P점을 끝 점으로 하는 벡터

![Alt text](<Images/vector 2.png>)

- Vector3의 일부를 가져와 구조체로 만들어 위치 이동 실습

```C#
struct MyVector
{
    public float x;
    public float y;
    public float z;

    public MyVector(float x, float y, float z) { this.x = x; this.y = y; this.z = z; }

    public static MyVector operator +(MyVector a, MyVector b)
    {
        return new MyVector(a.x + b.x, a.y + b.y, a.z + b.z);
    }

    public static MyVector operator -(MyVector a, MyVector b)
    {
        return new MyVector(a.x - b.x, a.y - b.y, a.z - b.z);
    }
}

public class PlayerController : MonoBehaviour
{
    void Start()
    {
        MyVector pos = new MyVector(0.0f, 10.0f, 0.0f);
        pos += new MyVector(0.0f, 2.0f, 0.0f);
    }
}
```

### 방향 벡터
- 주어진 직선 방향과 평행하는 벡터

![Alt text](<Images/vector 4.PNG>)

- 방향 값과 방향의 크기 또한 나타낸다

### Maginuted

- 벡터의 길이를 반환
- 벡터의 길이는 (x * x + y * y + z * z)의 제곱근
- 벡터의 거리 (크기)를 구할 때 사용

```C#
[MethodImpl(MethodImplOptions.AggressiveInlining)]
public static float Magnitude(Vector3 vector)
{
    return (float)Math.Sqrt(vector.x * vector.x + vector.y * vector.y + vector.z * vector.z);
}
```

### nomalized

```C#
[MethodImpl(MethodImplOptions.AggressiveInlining)]
public static Vector3 Normalize(Vector3 value)
{
    float num = Magnitude(value);
    if (num > 1E-05f)
    {
        return value / num;
    }

    return zero;
}
```
- 해당 벡터의 magnitude가 1인 벡터를 반환
- 벡터가 정규화 (normalized)되면, 벡터는 갖는 방향 값을 갖지만, 정규화 벡터의 길이는 1.0
- Vector3.Forward, Back, Left, Right와 같이 방향을 결정하여 해당 값에 속도 연산을 하거나 Deltatime과 같이 사용자의 프레임 률을 곱하여 적용 시킬 때 사용된다.

## Rotation

### 오일러 각 (Euler Angle)
- 강체가 놓인 방향을 3차원 공간에 표시하기 위해 오일러가 도입한 세 개의 각도
- 3개의 서로 수직인 X, Y, Z축 각도로 표현하는 일반적이고 직관적인 방법 중 하나
- 오일러 각도는 회전한 축을 기준으로 삼아 순차적으로 회전

![Alt text](<Images/rotation 1.png>)

- 짐벌락 Gimbal Lock
  - 같은 방향으로 두 회전 축이 겹친 다음부터 겹친 축이 서로 구분되지 않는 고정 상태가 된다
  - 오일러 각은 세 개의 축을 동시에 계산하지 않다보니 겹침 현상이 발생한다.

![Alt text](<Images/rotation 2.png>)

- 오일러 각으로 방향을 표현할 때는 문제가 되지 않지만 회전을 표현할 때는 문제가 된다
- 어느 방향으로 돌아갈지 중간 값을 결정할 수 없다
- 3D 게임은 쿼터니언으로 반드시 변환해야 한다

### 쿼터니언 (Quarternion)
- 쿼터니언은 x, y, z, w 4개의 성분으로 구성
- 각 성분은 x, y, z 벡터와 스칼라
- 쿼터니언은 모든 축을 한 번에 계산하기 때문에 짐벌락 문제가 생기지 않으며 방향과 회전을 모두 표현할 수 있다
- 쿼터니언의 회전은 A 방향에서 B 방향으로 측정하기 때문에 180도 이상은 환원된다
- 그래서 180도 이상의 큰 값을 표현할 수 없다

```C#
 float _yAngle = 0.0f;

 void Update()
 {
     _yAngle += Time.deltaTime * 100.0f;

     transform.rotation = Quaternion.Euler(new Vector3(0.0f, _yAngle, 0.0f));
 }
 ```

![Alt text](<Images/rotation 3.PNG>)

- 키 입력에 따라 바라보는 방향으로 회전 시키기

![Alt text](<Images/rotation 4.png>)

```C#
void Update()
{

    if (Input.GetKey(KeyCode.W))
    {
        transform.rotation = Quaternion.LookRotation(Vector3.forward);
    }
    if (Input.GetKey(KeyCode.S))
    {
        transform.rotation = Quaternion.LookRotation(Vector3.back);
    }
    if (Input.GetKey(KeyCode.A))
    {
        transform.rotation = Quaternion.LookRotation(Vector3.left);
    }
    if (Input.GetKey(KeyCode.D))
    {
        transform.rotation = Quaternion.LookRotation(Vector3.right);
    }
}
```

![Alt text](<Images/rotation 5.PNG>)

### Lerp vs Slerp

- Lerp
  - https://docs.unity3d.com/ScriptReference/Vector3.Lerp.html

- Slerp
  - https://docs.unity3d.com/ScriptReference/Vector3.Slerp.html

- 부드러운 움직임을 위해 Slerp를 사용