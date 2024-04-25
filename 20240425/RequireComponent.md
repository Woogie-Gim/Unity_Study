# RequireComponent

- RequireComponent 속성은 요구되는 컴포넌트를 종속성으로 자동으로 추가해준다

- RequireComponent 를 사용하는 스크립트를 GameObject에 추가하면 필요한 component가 GameObject에 자동으로 추가된다

- RequireComponent는 설정 오류를 방지하는데 유용
- 예를 들어 RequireComponent가 있는 스크립트는 Rigidbody가 항상 같은 GameObject에 추가 되도록 요구할 수 있다
- 그래서 이를 통해 자동으로 수행되므로 설정이 잘못 될 수 없다
  
- 참고로 RequireComponent는 컴포넌트가 GameObject에 추가되는 순간에만 누락된 종속성을 확인
- 게임 오브젝트에 새 종속성이 없는 기존 구성 요소 인스턴스에는 이러한 종속성이 자동으로 추가되지 않는다