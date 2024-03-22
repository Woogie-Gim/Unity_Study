# Abstract

## 추상 클래스란?
- 일반 클래스와 인터페이스의 중간 정도
  - 인터페이스 같은 면
    - 모든 자식들이 반드시 오버라이딩해야 하는 함수 껍데기 (프로토타입)을 가지고 있다
    - 따라서 추상클래스 스크립트는 컴포넌트로서 오브젝트에 붙일 수 없다
  
  - 일반 클래스 같은 면
    - 인터페이스와 다르게 어느 정도 실제 구현 부분도 포함할 수 있다
      - 멤버 변수도 가질 수 있고 멤버 함수를 바디까지 구현할 수 있다

## abstract 키워드
- `abstract` 키워드를 클래스 이름 앞에 붙이면 추상 클래스가 된다
- `abstract`를 함수 이름 앞에 붙이면 이 함수는 껍데기 뿐이므로 반드시 자식 클래스에서 오버라이딩 해야 한다는 의미이다.
  - 함수 프로토타입만 작성한다

```C#
public abstract class BaseMonster : MonoBehaviour
{
    public abstract void Attack();
}
```

## abstract와 virtual의 차이점
- `virtual` 은 `{}` 중괄호, 즉 함수의 바디를 가진다.
  - 자식 클래스가 이 함수를 오버라이딩 하도록 권장할 뿐
  - 자식 클래스가 이 함수를 오버라이딩 하지 않으면 부모가 정의한 바디 내용대로 실행된다

- `abstract`는 함수의 바디를 가지지 않는다. 프로토타입 뿐.
  - 모든 자식 클래스에서 이 함수를 반드시 오버라이딩 하도록 강제한다
  - 오버라이딩 하지 않으면 에러 남

## 예시

### BaseMonster.cs (추상클래스)

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public abstract class BaseMonster : MonoBehaviour
{
    public float damage = 100f;

    void Update()
    {
        if(Input.GetKeyDown(KeyCode.Space))
        {
            Attack();
        }
    }

    public abstract void Attack();
}
```

- 추상클래스는 보다시피 멤버 변수(damage)도 가질 수 있고 구현된 함수(void update())도 가질 수 있다.
- 자식 클래스에서 abstract함수인 Attack() 함수를 반드시 오버라이딩 해야한다.

### Goblin.cs

- BaseMonster를 상속 받는다.
  - public class Goblin : BaseMonster
  - 멤버 변수
    - public float damage = 100f; (상속 받음)
  - 멤버 함수
    - void Update() (상속 받음)
      - 스페이스바 누르면 공격
    - public abstract void Attack(); 오버라이딩

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Goblin : BaseMonster
{
    public override void Attack()  // 오버라이딩
    {
        Debug.Log("한 캐릭터를 공격했다. 공격력: " + damage);
    }
}
```

### Orc.cs

- BaseMonster를 상속 받는다.
  - public class Orc : BaseMonster
  - 멤버 변수
    - public float damage = 100f; (상속 받음)
  - 멤버 함수
    - void Update() (상속 받음)
      - 스페이스바 누르면 공격
    - public abstract void Attack(); 오버라이딩

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Orc : BaseMonster
{
    public override void Attack()
    {
        Debug.Log("광격 공격을 했다. 공격력: " + damage);
    }
}
```

- Goblin과 Orc를 각각 오브젝트에 붙여주면 같은 Attack()이라고 둘이 다르게 동작하는 것을 볼 수 있다.