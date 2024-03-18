# Enum

- 열거형 ("enumeration"의 줄인말) 형식
- 열거형이란 이름이 지정된 상수 집합을 나타내는 값 형식
- 열거형은 enum 키워드를 사용하여 정의되며 상수는 쉼표로 구분된 값의 목록으로 지정된다.

```C#
public enum Days
{
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}
```

- 열거형은 일련의 지정된 상태(state) 또는 값의 집합을 나타내는 데 자주 사용
  
## Enum의 이점
- 열거형을 사용하면 일반 상수를 사용하는 것 보다 몇 가지 이점을 누릴 수 있다

### 읽기 쉽다
- 열거형은 숫자 상수보다 이해하기 쉬운 지정된 이름을 가진 상수를 사용한다
- 예를들어 Days.Sunday 라고 하면 이 값이 일요일을 나타낸다는 것을 직관적으로 알 수 있다

### 유지 관리가 쉽다
- 열거형은 유지 관리가 더 쉽다.
- 열거형에서 상수를 추가, 제거 또는 재정렬해야 하는 경우 상수 값을 변경하지 않고도 수행할 수 있다
- 이는 상수가 코드의 위치에서 사용되는 경우 특히 유용할 수 있다

### 안전하다 (type-safe)
- 열거형은 미리 지정된 type 이므로 열거형 변수에 실수로라도 잘못된 유형의 값을 할당할 수 없다
- 따라서 열거형을 사용하면 코드의 오류를 방지할 수 있다

## enum 사용의 예

```C#
using UnityEngine;

public class EnumExample : MonoBehaviour
{
    // 3개의 State 값을 열거형으로 지정
    public enum States
    {
        Idle,
        Walking,
        Running
    }

    // enum 타입의 변수를 선언
    public States currentState;

    void Update()
    {
        // switch 구문을 이용하여 열거형 변수를 사용
        switch (currentState)
        {
            case States.Idle:
                // state 가 idle 일 때 콘솔 화면에 상태를 표시
                Debug.Log("Idle");
                break;
            case States.Walking:
                // state 가 walking 일 때 콘솔 화면에 상태를 표시
                Debug.Log("Walking");
                break;
            case States.Running:
                // state 가 running 일 때 콘솔 화면에 상태를 표시
                Debug.Log("Running");
                break;
        }
    }
}
```

