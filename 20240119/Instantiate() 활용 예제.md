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