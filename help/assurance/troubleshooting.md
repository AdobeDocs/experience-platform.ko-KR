---
title: Adobe Experience Platform Assurance 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform Assurance 사용 시 발생하는 일반적인 문제에 대한 해결 방법을 간략하게 설명합니다.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# Adobe Experience Platform Assurance 문제 해결

Assurance를 사용할 수 없는 경우 다음 문제 주제 아래의 제안을 참조하여 일반적으로 발생하는 문제를 해결하십시오.

더 원활한 구현을 활성화하고 잠재적인 문제를 검색하려면 다음과같이 SDK 로깅이 설정되어 있는지 확인하십시오. [디버그 로깅 활성화](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) ( 시작 섹션).

다음을 사용하여 SDK 로그 수준을 변경할 수 있습니다. [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## 온디바이스, 앱 문제

### QR 코드가 앱을 열지 않습니다.

* 링크에 직접 액세스합니다. 다음에서 링크 복사 **세션 세부 정보**. 장치의 브라우저 주소 표시줄에 붙여 넣어 엽니다. 열리지 않으면 섹션을 참조하십시오. [앱에서 링크가 열리지 않습니다.](#app-does-not-open-link).
* 다른 QR 리더를 사용하십시오. iOS 11 이상의 경우 사진 앱을 사용하여 QR 코드를 읽습니다.

### 앱에서 링크를 열지 않음

* 딥링크 구현이 앱에 올바르게 구성되었는지 확인합니다.
   * **Android:** 딥링크(앱 링크)
      * [앱 컨텍스트에 대한 딥링크 만들기](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** 사용자 지정 URL 체계 또는 범용 링크
      * [앱에 대한 사용자 지정 URL 체계 정의](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [앱에서 범용 링크 지원](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Android의 경우 `startSession` API를 명시적으로 호출할 필요가 없습니다. iOS의 경우에서 설명한 대로 API를 사용합니다 [Adobe Experience Platform 보증](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### 인증 오버레이가 표시되지만 앱이 연결되지 않음

* 장치 웹 브라우저를 통해 장치의 인터넷 연결을 확인합니다.
* 앱이 Assurance 서비스에 성공적으로 연결되지 않은 경우 Assurance가 제대로 설정되어 있는지 확인하십시오. 설치에 대한 지침 보기 [Adobe Experience Platform 보증](./tutorials/implement-assurance.md) SDK 라이브러리입니다.
* 세션이 링크와 일치하고 예상 세션에 대해 올바르게 입력되었는지 확인합니다. 다음을 참조하십시오 [로그 메시지 &quot;OrgID 정보를 사용할 수 없음&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (둘 이상의 조직 인스턴스에 액세스할 수 있는 경우에만 일반적이지 않으며 관련성이 있습니다.)

### Adobe Analytics 디버깅

**사후 처리 상태 - 디버그 플래그 없음**

Analytics 이벤트 보기에서 사후 처리 상태 &quot;디버그 플래그 없음&quot;으로 이벤트가 실패할 경우 현재 Adobe Analytics 또는 Assurance SDK 버전에서 Analytics 디버깅 기능을 지원하지 않을 수 있습니다.
이 문제를 해결하려면 Adobe Analytics 및 Assurance SDK 확장을 최신 버전으로 업그레이드하십시오.

| 최소 버전 요구 사항 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| 보증 | > 1.0.0 | > 1.0.0 |

### React 기본 MobileCore 및 AEPAsurance 호환성

| AEP Assurance 버전 | Mobile Core 버전 | 설치 지침 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

을 사용하는 경우 `react-native-acpcore` assurance를 사용하면 다음 오류 메시지 중 하나로 React Native 애플리케이션을 빌드하지 못할 수 있습니다.

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

또는

```
AppDelegate: AEPAssurance.h file not found
```

**솔루션**

이 경우 다운그레이드하십시오. `react-native-aepassurance` 다음 npm 명령 사용:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

이 오류는 다음과 같은 이유로 발생합니다. `react-native-acpcore` 확장명: **전용** 호환 가능 `react-native-aepassurance` 버전 2.x.x 이하.
