# Prefab
- 프리팹 (Prefab)은 미리 만들어 놓은 게임 오브젝트, 템플릿
- 프리팹은 Asset에 저장되어 있으며 프리팹 인스턴스(Prefab Instance)를 생성하여 월드 상에서 동작한다
- 프리팹으로부터 원하는 만큼의 프리팹 인스턴스를 생성할 수 있다 생성된 프리팹 인스턴스는 서로 독립적으로 동작하며, 프리팹 인스턴스의 프로퍼티를 수정해도, 다른 프리팹 인스턴스에는 영향을 주지 않는다

## Game Object와 Prefab
- 게임 오브젝트는 월드상에 존재하며 프리팹은 Asset 폴더의 데이터로 존재한다
- 프리팹 기반으로 Instance를 생성하면 런타임 시점에서 월드 상의 게임 오브젝트로 존재하게 된다

## Prefab 생성 및 수정

### Prefab 생성
- 프리팹의 생성은 Scene에 만들어 둔 게임 오브젝트를 프로젝트로 드래그 하면 된다
- 생성된 프리팹은 Asset 폴더의 단일 파일로 저장되며, Scene view로 드래그를 통해 인스턴스를 생성할 수도 있으며, 런타임 시점에 스크립트에서 인스턴스를 생성할 수 있다

![Alt text](<Images/prefab 1.png>)

### Prefab 수정
- 프리팹을 더블클릭하면 프리팹 수정 화면으로 이동하게 되며, 수정이 가능하다. 수정화면은 Scene에 보이는 화면과 다르다
- 수정 화면이 불편하다면, 프리팹을 Scene에 드래그하여 등록하고, 수정을 한다.
- 수정이 끝난 프리팹은 Overrides를 클릭하여 적용한다. (아래 사진 참조, 노란색)
- 그렇지 않으면, 프리팹은 수정이 되지 않는다. 
- 여러개의 프리팹 인스터스가 Scene View 상에 있다면, 모든 프리팹 인스턴스의 프로퍼티는 수정된다. 

![Alt text](<Images/prefab 2.png>)

### Prefab Instance

- 프리팹은 미리 정의된 클래스로부터 new 키워드를 통해 클래스의 인스턴스를 생성하는 것과 같은 방식으로 동작한다.
- Object Class의 Instantiate(prefab) 함수를 사용해 인스턴스를 생성한다.
- Object Class는 Unity Class의 최상위 클래스이다. MonoBehaviour는 Object class로부터 상속되어 구현되어 있다. 

### Prefab 등록
- 필요한 상황에 따라 사용하면 된다. 
- 프리팹은 많은 장점을 가지고 있다. 
- 각 씬마다 동일한 게임오브젝트를 생성할 때에 사용하면 편리하다. 
- 또한, 각 프로퍼티 값이 변경되었을때 씬마다 일일이 수정을 하지않아도 된다. 
  
- Game Object
  - Script에 public GameObject 변수를 선언하고 프리팹을 등록한다. 3의 코드블럭은 게임 오브젝트로 프리팹에 접근하고 프리팹 인스턴스를 생성한다.
  - 게임 오브젝트로 등록한 프리팹은 프리팹에 추가한 스크립트를 불러오는 추가적인 로직이 요구된다. 

- Script (Class)
  - 프리팹에 추가되어 있는 Script(Class)로 접근이 가능하다. 
  - 스크립트를 사용한 생성은 프리팹 안에 해당 스크립트가 없다면, 등록할 수 없다. 
  - 대상 프리팹인지 아닌지를 판별하기에 편리하며, 직접 스크립트에 접근하기 때문에, 수정 및 접근이 용이하다. 

![Alt text](<Images/prefab 3.png>)

![Alt text](<Images/prefab 4.png>)