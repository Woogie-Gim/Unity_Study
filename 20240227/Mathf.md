# 유니티에서 쓰이는 수학함수

## Mathf.Abs(float f)
- 데이터 절대값 변환

```C#
Debug.Log(Mathf.Abs(-100))
// 100 (결과 값)
```

## Mathf.Clamp(float f, float min, float max)
- 최소값, 최대값 범위 내 데이터 반환
- 데이터가 1이고, 최소값 0, 최대값 10인 경우 1을 반환

```C#
for (int i = 0; i < 5; i++)
{
    Debug.Log(Mathf.Clamp(i, 1.0f, 3.0f));
}

// 1, 1, 2 ,3 , 3 (결과 값)
```

## Mathf.PingPong(float A, float B)
- A 값이 B 값에 도달하면 -가 되고, 0이 되면 다시 최대값까지 +

```C#
void Update()
{
    transform.position = new Vector3(Mathf.PingPong(Time.time, 3), transform.position.y, transform.position.z);
}

// x축으로 3만큼 이동 후 다시 0으로 이동 반복
// 누적 값은 Time 이다
```

## Mathf.Lerp(float A, float B, float T)
- 시작점과 종료점 사이 거리비율 반환 (거리 비율은 0 ~ 1 사이 값으로 고정되며 %를 의미)
- Vector3.Lerp도 동일하며, 파라미터만 차이가 있다

```C#
void Update()
{
    transform.position = new Vector3(transform.position.x, Mathf.Lerp(0f, 5f, Time.time), 0);
}

// 시간 값에 의해 0에서 5로 이동
```

## Mathf.SmoothStep(float A, float B, float T)
- Lerp와 유사하며, 시간이 흐를 수록 속도가 높아지고 종료점에 다다르면 속도가 줄어듬

## Mathf.Ceil(float f) / Mathf.CeilToInt(float f)
- 소수점 첫자리 올림

## Mathf.Floor(float f) / Mathf.FloorToInt(float f)
- 소수점 이하 버림

## Mathf.Round(float f) / Mathf.RoundToInt(float f)
- 소수점 첫자리 반올림
- 단, 0.5 까지 버림