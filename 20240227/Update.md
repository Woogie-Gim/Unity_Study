# Update

## Update()
- Update는 프레임마다 한번씩만 호출되는 기본적인 업데이트

## FixedUpdate()
- FixedUpdate는 Update보다 자주 호출이 되는 경우가 있다
- 프레임 속도가 낮을 경우 프레임 마다 여러번 호출이 가능하다
- 프레임 속도가 높을 경우 프레임마다 호출을 할 수 없다
- FixedUpdate 직후에 모든 물리적 특성 계산 및 업데이트가 발생하므로 이동 계산을 적용할 때 Time.DeltaTime 값을 곱할 필요가 없다.
- 독립된 업데이트 이므로 모두 영향을 받는 update와 달리 어떤 것이든 동일한 주기로 업데이트 영향을 받는다
- 물리 적용시 사용하면 효과적이다.

## LateUpdate()
- LateUpdate는 Update 후 프레임마다 한번씩 호출
- update에서 계산이 완료되면 해당 LateUpdate가 실행이 된다
- 특정 행동이 완전히 끝난 후 실행하고 싶은 행동이 있담녀 해당 LateUpdate를 이용하는 것이 좋다
- 예를 들어 3인칭 카메라가 캐릭터를 따라 움직일 시 update에서 캐릭터 이동 방향 계산이 끝난 후 카메라에 대한 계산은 LateUpdate에서 행동을 취하면 된다