---
title: Adobe Experience Platform 웹 SDK 구성
description: Adobe Experience Platform 웹 SDK를 구성하는 방법을 알아봅니다.
seo-description: Experience Platform 웹 SDK를 구성하는 방법 알아보기
keywords: 구성;구성;구성;SDK;edge;웹 SDK;구성;EdgeConfigId;컨텍스트;웹;장치;환경;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConceptions;웹 sdk 설정;prehingStyle;cookieEnabled;urlEnabled;urlEnabled DestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: f78da58ba7a593d9c161030833d9b69e2ba57c9a
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 10%

---


# 플랫폼 웹 SDK 구성

SDK 구성은 `configure` 명령으로 수행됩니다.

>[!IMPORTANT]
>
>`configure` 항상  ** 첫 번째 명령을 호출해야 합니다.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

구성 중에 설정할 수 있는 여러 옵션이 있습니다. 모든 옵션은 아래에서 카테고리별로 그룹화할 수 있습니다.

## 일반 옵션

### `edgeConfigId`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | 없음 |

SDK를 적절한 계정 및 구성에 연결하는 할당된 구성 ID입니다.  단일 페이지 내에서 여러 인스턴스를 구성할 때는 각 인스턴스에 대해 다른 `edgeConfigId`을 구성해야 합니다.

### `context`

| **유형** | **필수 여부** | **기본값** |
| ---------------- | ------------ | -------------------------------------------------- |
| 문자열 배열 | 아니요 | `["web", "device", "environment", "placeContext"]` |

[자동 정보](../data-collection/automatic-information.md)에 설명된 대로 자동으로 수집할 컨텍스트 범주를 나타냅니다.  이 구성을 지정하지 않으면 기본적으로 모든 카테고리가 사용됩니다.

### `debugEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `false` |

디버깅을 사용할지 여부를 나타냅니다. 이 구성을 `true`으로 설정하면 다음 기능이 활성화됩니다.

| **기능** | **함수** |
| ---------------------- | ------------------ |
| 동기 유효성 검사 | 스키마에 대해 수집 중인 데이터를 검증하고 다음 레이블 아래의 응답에서 오류를 반환합니다.`collect:error OR success` |
| 콘솔 로깅 | 브라우저의 JavaScript 콘솔에 표시할 디버깅 메시지를 활성화합니다. |

### `edgeDomain` {#edge-domain}

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ------------------ |
| 문자열 | 아니요 | `beta.adobedc.net` |
| 문자열 | 아니요 | `omtrdc.net` |

Adobe 서비스와 상호 작용하는 데 사용되는 도메인입니다. Adobe 에지 인프라에 요청을 프록시하는 퍼스트 파티 도메인(CNAME)이 있는 경우에만 사용됩니다.

### `orgId`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | 없음 |

할당된 [!DNL Experience Cloud] 조직 ID.  페이지 내에서 여러 인스턴스를 구성할 때는 각 인스턴스에 대해 다른 `orgId`을 구성해야 합니다.

## 데이터 수집

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

링크 클릭과 관련된 데이터를 자동으로 수집할지 여부를 나타냅니다. 자세한 내용은 [자동 링크 추적](../data-collection/track-links.md#automaticLinkTracking)을 참조하십시오.

### `onBeforeEventSend`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 함수 | 아니요 | () => 정의되지 않음 |

수신자가 전송되기 직전에 모든 이벤트에 대해 호출되는 콜백을 구성하려면 이 설정을 설정하십시오.  필드가 `xdm`인 객체가 콜백으로 전송됩니다.  `xdm` 개체를 수정하여 보낸 내용을 변경합니다.  콜백 내에서 `xdm` 개체는 이벤트 명령에서 전달된 데이터와 자동으로 수집된 정보를 이미 갖습니다. 이 콜백 시간 및 예제에 대한 자세한 내용은 [전역 이벤트 수정](tracking-events.md#modifying-events-globally)을 참조하십시오.

## 개인 정보 옵션

### `defaultConsent` {#default-consent}

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 개체 | 아니요 | `"in"` |

사용자의 기본 동의를 설정합니다. 이 설정은 사용자에 대해 이미 저장된 동의 환경 설정이 없을 때 사용됩니다. 다른 유효한 값은 `"pending"` 및 `"out"`입니다. 이 기본값은 사용자의 프로필에 지속되지 않습니다. setConcepts가 호출될 때만 사용자의 프로필이 업데이트됩니다.
* `"in"`:이 설정이 되어 있거나 값을 제공하지 않으면 사용자 동의 기본 설정 없이 작업을 진행합니다.
* `"pending"`:이 설정이 지정되면 사용자가 동의 환경 설정을 제공할 때까지 작업은 큐에 오르게 됩니다.
* `"out"`:이 설정이 지정되면 사용자가 동의 기본 설정을 제공할 때까지 작업이 무시됩니다.
사용자의 기본 설정이 제공되면 사용자의 기본 설정에 따라 작업이 진행되거나 취소됩니다. 자세한 내용은 [지원 동의](../consent/supporting-consent.md)를 참조하십시오.

## 개인화 옵션

### `prehidingStyle`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 아니요 | 없음 |

개인화된 컨텐츠가 서버에서 로드되는 동안 웹 페이지의 컨텐츠 영역을 숨기는 CSS 스타일 정의를 만드는 데 사용됩니다. 이 옵션을 제공하지 않으면 SDK는 개인화된 컨텐츠가 로드되는 동안 컨텐츠 영역을 숨기지 않으므로 &quot;깜박임&quot;이 발생할 수 있습니다.

예를 들어, 개인화된 컨텐츠가 서버에서 로드되는 동안 숨기려는 기본 컨텐츠의 ID가 `container`인 웹 페이지에 요소가 있는 경우, 사전 숨김 스타일의 예는 다음과 같습니다.

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 대상 옵션

### `cookieDestinationsEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

세그먼트 자격 조건에 따라 쿠키 설정을 허용하는 [!DNL Audience Manager] 쿠키 대상을 활성화합니다.

### `urlDestinationsEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

세그먼트 자격에 따라 URL을 실행할 수 있는 [!DNL Audience Manager] URL 대상을 활성화합니다.

## ID 옵션

### `idMigrationEnabled` {#id-migration-enabled}

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | true |

true인 경우 SDK는 이전 AMCV 쿠키를 읽고 설정합니다. 이렇게 하면 사이트의 일부 부분이 여전히 Visitor.js를 사용하고 있을 수 있지만 Adobe Experience Platform 웹 SDK를 사용하는 것으로 전환할 수 있습니다. 또한 방문자 API가 페이지에 정의된 경우 SDK는 방문자 API에 대해 ECID를 쿼리합니다. 이를 통해 Adobe Experience Platform 웹 SDK를 사용하여 이중 태그 페이지에 동일한 ECID를 사용할 수 있습니다.

### `thirdPartyCookiesEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | true |

제3자 쿠키 Adobe 설정을 활성화합니다. SDK에는 여러 사이트에서 동일한 방문자 ID를 사용할 수 있도록 제3자 컨텍스트에서 방문자 ID를 유지하는 기능이 있습니다. 이 기능은 여러 사이트가 있거나 파트너와 데이터를 공유하려는 경우에 유용합니다.하지만 경우에 따라 이는 개인 정보 보호 이유로 필요하지 않습니다.
