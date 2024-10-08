---
title: Adobe Experience Platform Assurance 문제 해결 안내서
description: 이 문서는 Adobe Experience Platform Assurance를 사용할 때 발생하는 일반적인 문제에 대한 솔루션을 간략하게 설명합니다.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 100%

---

# Adobe Experience Platform Assurance 문제 해결

Assurance를 작동하는 데 문제가 있는 경우 다음 문제 항목에서 제안 사항을 참조하여 일반적으로 발생하는 문제를 해결하십시오.

수월하게 구현할 수 있고 잠재적인 문제를 발견하려면 시작하기 섹션의 [디버그 로깅 활성화](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/)에 따라 SDK 로깅을 설정해야 합니다.

[`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API를 사용하여 SDK 로그 수준을 변경할 수 있습니다.

## 온디바이스, 앱 문제

### QR 코드는 앱을 열지 않음

* 링크에 직접 액세스합니다. **세션 세부 정보**&#x200B;에서 링크를 복사합니다. 디바이스의 브라우저 주소 표시줄에 붙여넣어 엽니다. 열리지 않으면 [앱이 링크를 열지 않음](#app-does-not-open-link) 섹션을 참조하십시오.
* 다른 QR 리더를 사용하십시오. iOS 11 이상인 경우 Photo 앱을 사용하여 QR 코드를 읽습니다.

### 앱이 링크를 열지 않음

* 앱에서 딥 링크 구현이 올바르게 구성되었는지 확인합니다.
   * **Android:** 딥 링크(앱 링크)
      * [앱 컨텍스트에 대한 딥 링크 만들기](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** 사용자 정의 URL 체계 또는 범용 링크
      * [앱에 대한 사용자 정의 URL 체계 정의](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [앱에서 범용 링크 지원](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Android의 경우 `startSession` API는 명시적으로 호출하지 않아도 됩니다. iOS의 경우 [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core)에 설명된 대로 API를 사용합니다.

### 인증 오버레이가 나타나지만 앱이 연결되지 않음

* 디바이스 웹 브라우저를 통해 디바이스의 인터넷 연결을 확인합니다.
* 앱이 Assurance 서비스에 연결되지 않은 경우 Assurance에 대해 올바르게 설정되었는지 확인하십시오. [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) SDK 라이브러리의 설치 지침을 참조하십시오.
* 세션이 링크와 일치하고 예상 세션에 대해 올바르게 입력되었는지 확인합니다. [“OrgID 정보를 사용할 수 없음”이라는 로그 메시지](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available)를 참조하십시오(둘 이상의 ORG 인스턴스에 액세스할 수 있는 경우에만 이 문제가 일반적이지 않고 관련이 있음).

### Adobe Analytics 디버깅

**후처리 상태 - 디버그 플래그 없음**

Analytics 이벤트 보기에서 후처리 상태인 “디버그 플래그 없음”으로 이벤트가 실패하면 현재 Adobe Analytics 또는 Assurance SDK 버전이 Analytics 디버깅 기능을 지원하지 않을 수 있습니다.
이 문제를 해결하려면 Adobe Analytics 및 Assurance SDK 확장 기능을 최신 버전으로 업그레이드하십시오.

| 최소 버전 요구 사항 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| 보증 | > 1.0.0 | > 1.0.0 |

### React Native MobileCore 및 AEPAssurance 호환성

| AEP Assurance 버전 | 모바일 코어 버전 | 설치 지침 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Assurance에서 `react-native-acpcore`를 사용하는 경우 React Native 애플리케이션을 빌드하지 못하고 다음 오류 메시지 중 하나가 표시될 수 있습니다.

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

또는

```
AppDelegate: AEPAssurance.h file not found
```

**솔루션**

이 경우 다음 npm 명령을 사용하여 `react-native-aepassurance`를 다운그레이드하십시오.

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

이 오류는 `react-native-acpcore` 확장 기능이 2.x.x 이하의 `react-native-aepassurance` **버전과만** 호환되기 때문에 발생합니다.
