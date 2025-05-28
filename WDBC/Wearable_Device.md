# Wearable Device에서 API를 받아와서 사용하는 방법을 정리함.

갤럭시워치(Wear OS)에서 health connect 사용 시 : 기본적인 심박수나 수면 데이터를 가져올 수 있음

스마트폰(Android)에서 Samsung Health 어플 설치 시 : 그 외에 

수면 단계 분석 (얕은 수면, 깊은 수면, 렘 수면 등)
심박수 변화 추이
수면 중 코골이 감지
수면 중 산소 포화도 측정

같은 내용들을 알 수 있음 -> 있으면 정확도가 높아지고 좋지만 추가적으로 어플을 깔아야하는 귀찮음이 있음
-> 워치에 있는 데이터만 가져와서 졸음 운전 판단에 사용하는 것이 가장 간단하고 합리적인 방법으로 예상됌.

이제 갤럭시워치에서 health connect만 사용하여 API로 정보를 가져오는 방법을 찾아야함.

---


보통적으로

첫번째 방법 : 삼성 헬스 서비스 연동:
SDK 사용:
삼성에서 제공하는 SDK를 사용하여 갤럭시 워치 앱에서 심박수, 걸음 수, 수면 등 다양한 건강 데이터를 가져올 수 있습니다.
Health Services API:
Wear OS 기반 기기에서 건강 데이터를 접근하려면 Health Services API를 사용해야 합니다.
앱 개발:
삼성 헬스 서비스 연동을 통해 유용한 건강 앱을 개발할 수 있습니다.


2번째 방법 : Wear OS Data Layer API:
데이터 동기화:
Wear OS의 Data Layer API를 사용하면 스마트폰과 워치 간의 데이터 동기화를 효율적으로 처리할 수 있습니다.
메시지 전송:
이 API는 메시지 전송 기능도 제공하여 워치에서 스마트폰으로 데이터를 주고받을 수 있습니다.
백그라운드 서비스:
시스템은 WearableListenerService를 통해 Data Layer API를 관리하며, 데이터 전송이 필요한 경우 자동으로 서비스를 시작하고 종료합니다.


기타:
API KEY 관리:
API를 사용할 때는 API 키를 안전하게 관리해야 하며, 유출 시 문제가 발생할 수 있으므로 주의해야 합니다. 
Manifest 파일:
갤럭시 워치 앱의 manifest 파일에 필요한 권한을 추가해야 합니다. 
플러터 앱:
플러터 앱에서 건강 데이터를 가져오려면 AndroidManifest.xml 파일에 권한을 추가해야 합니다. 



https://developer.android.com/training/building-wearables.html
각종 API 소개 및 UI 구성하는 법이 소개된 사이트

Wear OS by Google에서는 사용자가 연결 상태를 유지하고, 건강/피트니스 목표를 추적하고, 작업을 실행하며, 자신을 표현하는 데 도움이 되는 앱을 작성할 수 있음.

https://demat.tistory.com/77
갤럭시워치 api 가져오는거 관련해서 정리된 블로그



---

API 참조
Tizen .NET API
Tizen .NET API는 Galaxy Watch용 .NET 애플리케이션을 만드는 데 필요한 풍부한 인터페이스를 제공합니다.

.NET 표준 API : .NET 표준
TizenFX API : Tizen 플랫폼별 API 세트
Xamarin Forms : 사용자 인터페이스 API
Tizen Circular UI API : Tizen 웨어러블을 위한 Xamarin.Forms 확장
Tizen 원형 UI API
Tizen Circular UI 는 Galaxy Watch용 Xamarin.Forms의 유용한 확장 기능입니다.

이 확장 기능은 Galaxy Watch에 완벽하게 어울리는 아름다운 원형 UI 컨트롤을 제공합니다.

가이드 와 API 참조를 확인 하고 무엇이 제공되는지 살펴보세요.

Tizen Circular UI API를 사용하면 Samsung UX를 따르는 UI 애플리케이션을 쉽게 만들 수 있습니다.


삼성 확장 API
C# 기반의 Tizen Samsung Extension API는 Galaxy Watch에 추가 기능을 제공합니다.

삼성 액세서리 프로토콜(SAP) API
SAP API를 사용하면 Samsung Access Protocol Framework를 통해 Android 스마트폰과 Galaxy Watch 간에 데이터를 교환할 수 있습니다. SAP 서비스를 검색하고, 액세서리 서비스를 연결하고, 데이터를 교환할 수 있습니다.

삼성 액세서리 프로토콜 소개
삼성 액세서리 프로토콜 API
원격 앱 제어 API
원격 애플리케이션 제어는 원격 호스트 장치에 설치된 원격 애플리케이션과 상호 작용하는 방법입니다. 원격 애플리케이션 제어는 작업, 애플리케이션 패키지 이름, URI와 같은 사용 가능한 정보를 기반으로 원격 애플리케이션을 명시적 또는 암시적으로 호출하거나 실행하고, 원격 장치에서 실행된 애플리케이션으로부터 응답을 받는 데 사용할 수 있습니다.

원격 앱 제어 가이드
원격 앱 제어 API
Tizen을 지원하는 .NET 및 Xamarin 3rd API
ElottieSharp : Bodymovin을 사용하여 JSON으로 내보낸 Adobe After Effects 애니메이션을 구문 분석하고 기본적으로 렌더링 할 수 있는 애니메이션 API
Xamarin.Essentials : 플랫폼별 기능에 액세스할 수 있는 단일 크로스 플랫폼 API
