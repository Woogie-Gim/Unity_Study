# Renderer Pipe Line

## Renderer Pipe Line 개념
- 그래픽스 파이프라인 (graphics pipeline) 이라고도 불림
- 렌더 파이프라인은 씬의 콘텐츠를 가져와 화면에 표시하는 일련의 작업을 수행
- 3차원의 도형 또는 이미지를 2차원의 이미지로 표현하기 위한 단계적 방법

![Alt text](<Images/렌더 파이프라인 1.PNG>)

## 렌더 파이프 라인의 종류
- 빌트인 렌더 파이프 라인 (기본 설정) : Unity의 기본 렌더 파이프라인, 범용적으로 사용되는 렌더 파이프라인이므로 커스터마이즈 옵션이 제한적
- 유니버설 렌더 파이프라인 (URP) : 쉽고 빠르게 커스터마이즈할 수 있는 스크립터블 렌더 
-  고해상도 렌더 파이프라인 (HDRP) : 스크립터블 렌더 파이프라인으로 고사양 플랫폼을 위한 최신 고해상도 그래픽스를 구현하도록 지원
- 커스텀 렌더 파이프라인 : Unity의 스크립터블 렌더 파이프라인 API를 사용하여 커스텀 렌더 파이프라인을 생성 할 수 있다.
  
## URP (Universal Render Pipeline)
- URP는 Unity에서 제작한 사전 빌드된 스크립터블 렌더 파이프 라인
- URP는 아티스트 친화적 워크플로를 통해 모바일, 고사양 콘솔, PC 등 다양한 플랫폼에서 최적화된 그래픽스를 쉽고 빠르게 구현하도록 돕는다

## URP 특징
- 다양한 조명과 그림자 효과, 그리고 후처리 효과를 지원
- 기존 렌더 파이프라인을 사용했을 때보다 효율적으로 고퀄리티의 이미지를 구현
- 모바일 환경이나 저사양 pc에서도 높은 품질의 이미지 구현 가능

## 3D vs 3D URP
- 유니티에서 3D 템플릿을 생성하면 유니티의 기본 랜더 파이프라인인 '빌트인 랜더 파이프라인'이 사용된다
- 3D URP 템플릿을 생성하면 '유니버설 랜더 파이프라인'이 사용된다
- 높은 성능을 요구하거나 고퀄리티의 이미지를 사용할 경우 URP가 게임제작에 적합할 수 있다