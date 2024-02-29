# Component 패턴

## 컴포넌트 패턴

- 게임 디자인 패턴의 일종
- 한 개체가 여러 분야를 서로 커플링 없이 다룰 수 있게 하는 방식
- 탈부착이 가능한 클래스
- 비유 : 부품을 만들어 관리하는 방식

### 컴포넌트 패턴을 사용하는 이유

- 만약 한 클래스 안에 모든 코드들이 섞여 있을 경우 협업에 개발 속도가 늦춰지고 디버깅에 많은 어려움을 겪게 된다
- 이러한 상황을 피하기 위해 분야별로 담당하는 파트를 나눠 설계할 필요가 있다

### 컴포넌트 패턴의 특성

1. 분야 나누기
2. 독자적인 컴포넌트

### 예시

![Alt text](<Images/component 1.PNG>)

- 큐브의 경우 Transform, Mesh Renderer, Collider 등 다양한 컴포넌트로 이루어져 있음
- 컴포넌트들을 종합하여 사용

![Alt text](<Images/component 2.PNG>)

![Alt text](<Images/component 3.PNG>)

![Alt text](<Images/component 4.PNG>)

- Empty Object에 큐브와 같은 컴포넌트를 추가했을 때 큐브와 똑같은 모습을 한걸 볼 수 있다
  
![Alt text](<Images/component 5.PNG>)

- 스크립트 또한 컴포넌트의 일종으로 사용할 수 있다
- 스크립트 경우 생성 후 이름을 입력하면 클래스명 또한 스크립트 파일의 이름과 같아진다

![Alt text](<Images/component 7.PNG>)

![Alt text](<Images/component 6.PNG>)

- 스크립트 컴포넌트를 추가 하면 스크립트에 입력한 메서드들이 오브젝트에서 수행 되는 것을 볼 수 있다