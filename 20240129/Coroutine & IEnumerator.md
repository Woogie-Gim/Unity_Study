# 코루틴 (Coroutine)과 IEnumerator

## 코루틴 (Coroutine)
- 코루틴은 시간의 경과에 따른 절차적 단계를 수행하는 로직을 구현하는 데 사용되는 함수
  
- 시간의 경과에 따른 절차적 단계에 대한 로직을 구현하는 것은 Update() 함수들에서도 가능
  
- 매 프레임마다 호출되는 로직은 Update()에서 구현하면 된다. 하지만 초당 호출이나, 매 프레임마다 호출이 필요하지 않은 부분을 매 프레임마다 호출 하는 것은 바람직한 로직이 아님

- 코루틴은 함수를 호출 한다. 함수는 한 프레임에 호출되어 완료가 된다

- 이에 IEnumerator 형식을 반환 값으로 가지는 함수를 사용

- IEnumaerator는 함수 내부에 실행을 중지하고 다음 프레임에서 실행을 재개할 수 있는 yeild return 구문을 사용한다

## yeild return
- yeild return 구문에는 다음과 같은 YieldInstruction 클래스를 사용한다

- yeild return null : 다음 프레임에 실행을 재개
- yeild return new WaitForSeconds : 지정된 시간 후에 재개한다
- yeild return new WaitForSecondsRealtime : Time.timescale 값에 영향을 받지 않고 지정된 시간 후에 재개한다
- yeild return new WaitForFixedUpdate : 모든 스크립트에서 모든 FixedUpdate가 호출된 후에 재개한다.
- yeild return new WaitForEndOfFrame : 모든 카메라와 GUI가 렌더링을 완료하고 스크린에 프레임을 표시하기 전에 호출된다
- yeild return StartCoroutine() : 코루틴을 연결하고 코루틴이 완료된 후에 재개

## StartCoroutine()와 StopCoroutine()
- Coroutine은 3개의 전달 인자를 사용한다

- StartCoroutine() : string MethodName을 사용하는 경우, 두 번째 매개변수로 전달 인자를 사용한다

```C#
Coroutine StartCoroutine(string MethodName, object = null);

Coroutine StartCoroutine(IEnumerate routine);

Coroutine StartCoroutine(Coroutine routine);
```

- StopCoroutine()

```C#
StopCoroutine(string MethodName);
StopCoroutine(IEnumerator routine);
StopCoroutine(Coroutine routine);
```
- 유니티는 코루틴을 사용할 때 전달 인자를 혼하밯여 사용하지 말 것을 권장한다
  
- 만약 StartCoroutine(stringMethodName)을 사용했다면, StopCoroutine(stringMethodName)을 사용하여 중지한다. 실제 사용해 보면, 대상 코루틴을 찾지 못한다.

## Coroutine 예제

### StartCorutine

```C#
using System.Collections;
using UnityEngine;

public class CoroutineExample : MonoBehaviour 
{
    float time;
    IEnumerator myCoroutine;

    // Start is called before the first frame update
    void Start() 
    {
        myCoroutine = MyCoroutine(1.0f);
        StartCoroutine(myCoroutine);
        time = 3.0f;
    }

    // Update is called once per frame
    void Update()
    {
        time -= Time.deltaTime;
        if (time < 0)
        {
            StopCoroutine(myCoroutine);
        }
    }

    IEnumerator MyCoroutine(float t)
    {
        Debug.Log("MyCoroutine;" + t);
        yeild return StartCoroutine(MySecondCoroutine(.1f));

        while (true)
        {
            Debug.Log("MyCoroutine");
            yield return new WaitForSeconds(0.2f);
        }

        IEnumerator MySecondCoroutine(float t)
        {
            DebugLog("MySecondCoroutine;" + t);
            yield return new WaitForSeconds(0.1f);
        }
    }
}
```

### StopCoroutine
- 코루틴을 정지하는 방법은 몇 가지 방법이 있으며 확실한 방법은 코루틴에 대한 인스턴스를 가지고 있는 것이다

- StartCoroutine(MyCoroutine()) → StopCoroutine(MyCoroutine())은 동작하지 않는다.

- StopCoroutine(string Name)

```C#
using System.Collecitons;
using UnityEngine;

public class CoroutineExample : MonoBehaviour
{
    float time;

    // Start is called before the first frame update
    void Start()
    {
        StratCoroutine("MyCoroutine", 0.1f);
        time = 3.0f;
    }

    // Update is called once per frame
    void Update()
    {
        time -= Time.deltaTime;
        if (time < 0)
        {
            StopCoroutine("MyCoroutine");
        }
    }

    IEnumerator MyCoroutine(float t)
    {
        Debug.Log("Coroutine;" + t);
        yeild return new WaitForSeconds(0.1f);

        while (true)
        {
            Debug.Log("Coroutine");
            yield return new WaitForSeconds(0.2f);
        }
    }
}
```

- IEnumerator 변수

```C#
using System.Collections;
using UnityEngine;

public class CoroutineExample : MonoBehaviour
{
    float time;
    IEnumerator myCoroutine;
    // Start is called before the first frame update
    void Start()
    {
        myCoroutine = MyCoroutine(1.0f);
         StartCoroutine(myCoroutine);
        time = 3.0f;
    }

    // Update is called once per frame
    void Update()
    {
        time -= Time.deltaTime;
        if (time < 0)
        {
            StopCoroutine(myCoroutine);
        }
    }

    IEnumerator MyCoroutine(float t)
    {
        Debug.Log("Coroutine;" + t);
        yield return new WaitForSeconds(0.1f);

        while (true)
        {
            Debug.Log("Coroutine");
            yield return new WaitForSeconds(0.2f);
        }
    }
}
```

- Coroutine 변수

```C#
using System.Collections;
using UnityEngine;

public class CoroutineExample : MonoBehaviour
{    
    float time;
    Coroutine myCoroutine;
    // Start is called before the first frame update
    void Start()
    {
        myCoroutine = StartCoroutine(MyCoroutine(1.0f));
        time = 3.0f;
    }

    // Update is called once per frame
    void Update()
    {
        time -= Time.deltaTime;
        if (time < 0)
        {
            StopCoroutine(myCoroutine);
        }
    }

    IEnumerator MyCoroutine(float t)
    {
        Debug.Log("Coroutine;" + t);
        yield return new WaitForSeconds(0.1f);

        while (true)
        {
            Debug.Log("Coroutine");
            yield return new WaitForSeconds(0.2f);
        }
    }
}
```