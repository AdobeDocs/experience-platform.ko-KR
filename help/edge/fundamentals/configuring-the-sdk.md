---
title: Adobe Experience Platform 웹 SDK 구성
description: Adobe Experience Platform 웹 SDK를 구성하는 방법을 알아봅니다.
seo-description: Experience Platform 웹 SDK를 구성하는 방법 알아보기
keywords: 구성;구성;구성;SDK;edge;웹 SDK;구성;EdgeConfigId;컨텍스트;웹;장치;환경;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConceptions;웹 sdk 설정;prehingStyle;cookieEnabled;urlEnabled;urlEnabled DestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
translation-type: tm+mt
source-git-commit: 2895975b9c103e6afba7db221223b4ef2116caf3
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 8%

---

# 플랫폼 웹 SDK 구성

SDK 구성은 `configure` 명령으로 수행됩니다.

>[!IMPORTANT]
>
>`configure` 은  ** 항상 첫 번째 명령이 호출된 경우입니다.

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
| 문자열 | 예 | None |

{style=&quot;table-layout:auto&quot;}

SDK를 적절한 계정 및 구성에 연결하는 할당된 구성 ID입니다. 단일 페이지 내에서 여러 인스턴스를 구성할 때는 각 인스턴스에 대해 다른 `edgeConfigId`을 구성해야 합니다.

### `context`

| **유형** | **필수 여부** | **기본값** |
| ---------------- | ------------ | -------------------------------------------------- |
| 문자열 배열 | 아니요 | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

[자동 정보](../data-collection/automatic-information.md)에 설명된 대로 자동으로 수집할 컨텍스트 범주를 나타냅니다. 이 구성을 지정하지 않으면 기본적으로 모든 카테고리가 사용됩니다.

### `debugEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `false` |

{style=&quot;table-layout:auto&quot;}

디버깅을 사용할지 여부를 나타냅니다. 이 구성을 `true`으로 설정하면 다음 기능이 활성화됩니다.

| **기능** | **함수** |
| ---------------------- | ------------------ |
| 동기 유효성 검사 | 스키마에 대해 수집 중인 데이터를 검증하고 다음 레이블 아래의 응답에서 오류를 반환합니다.`collect:error OR success` |
| 콘솔 로깅 | 브라우저의 JavaScript 콘솔에 표시할 디버깅 메시지를 활성화합니다. |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

자사 도메인에 이 필드를 채웁니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html)를 참조하십시오.

도메인은 www.`data.{customerdomain.com}`{customerdomain.com}.

### `orgId`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | 없음 |

{style=&quot;table-layout:auto&quot;}

할당된 [!DNL Experience Cloud] 조직 ID. 페이지 내에서 여러 인스턴스를 구성할 때는 각 인스턴스에 대해 다른 `orgId`을 구성해야 합니다.

## 데이터 수집

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style=&quot;table-layout:auto&quot;}

링크 클릭과 연관된 데이터가 자동으로 수집되는지 여부를 나타냅니다. 자세한 내용은 [자동 링크 추적](../data-collection/track-links.md#automaticLinkTracking)을 참조하십시오.

### `onBeforeEventSend`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 함수 | 아니요 | () => 정의되지 않음 |

{style=&quot;table-layout:auto&quot;}

전송되기 직전에 모든 이벤트에 대해 호출되는 콜백을 구성합니다. 필드가 `xdm`인 객체가 콜백으로 전송됩니다. 전송된 내용을 변경하려면 `xdm` 개체를 수정합니다. 콜백 내에서 `xdm` 개체는 이벤트 명령에서 전달된 데이터와 자동으로 수집된 정보를 이미 가지고 있습니다. 이 콜백 시간 및 예제에 대한 자세한 내용은 [전역 이벤트 수정](tracking-events.md#modifying-events-globally)을 참조하십시오.

## 개인 정보 옵션

### `defaultConsent` {#default-consent}

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 개체 | 아니요 | `"in"` |

{style=&quot;table-layout:auto&quot;}

사용자의 기본 동의를 설정합니다. 사용자에 대해 이미 저장된 동의 환경 설정이 없을 때 이 설정을 사용합니다. 다른 유효한 값은 `"pending"` 및 `"out"`입니다. 이 기본값은 사용자의 프로필에 지속되지 않습니다. 사용자의 프로필은 `setConsent`이(가) 호출될 때만 업데이트됩니다.
* `"in"`:이 설정을 지정하거나 값을 제공하지 않으면 사용자 동의 기본 설정 없이 작업을 진행합니다.
* `"pending"`:이 설정을 설정하면 사용자가 동의 환경 설정을 제공할 때까지 작업이 큐에 오르게 됩니다.
* `"out"`:이 설정을 설정하면 사용자가 동의 기본 설정을 제공할 때까지 작업이 무시됩니다.
사용자의 기본 설정이 제공되면 사용자의 기본 설정에 따라 작업이 진행되거나 취소됩니다. 자세한 내용은 [지원 동의](../consent/supporting-consent.md)를 참조하십시오.

## 개인화 옵션

### `prehidingStyle`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 문자열 | 아니요 | 없음 |

{style=&quot;table-layout:auto&quot;}

개인화된 컨텐츠가 서버에서 로드되는 동안 웹 페이지의 컨텐츠 영역을 숨기는 CSS 스타일 정의를 만드는 데 사용됩니다. 이 옵션을 제공하지 않으면 SDK는 개인화된 컨텐츠가 로드되는 동안 컨텐츠 영역을 숨기지 않으므로 &quot;깜박임&quot;이 발생할 수 있습니다.

예를 들어, 웹 페이지의 요소에 서버에서 맞춤형 컨텐츠를 로드하는 동안 숨기려는 기본 컨텐츠의 ID가 `container`인 경우 다음 사전 숨김 스타일을 사용하십시오.

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 대상 옵션

### `cookieDestinationsEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style=&quot;table-layout:auto&quot;}

세그먼트 자격 조건에 따라 쿠키 설정을 허용하는 [!DNL Audience Manager] 쿠키 대상을 활성화합니다.

### `urlDestinationsEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style=&quot;table-layout:auto&quot;}

세그먼트 자격에 따라 URL을 실행할 수 있는 [!DNL Audience Manager] URL 대상을 활성화합니다.

## ID 옵션

### `idMigrationEnabled` {#id-migration-enabled}

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style=&quot;table-layout:auto&quot;}

true인 경우 SDK는 이전 AMCV 쿠키를 읽고 설정합니다. 이 옵션은 사이트의 일부 부분에서는 여전히 Visitor.js를 사용할 수 있지만 Adobe Experience Platform 웹 SDK를 사용하여 전환하는 데 도움이 됩니다. 방문자 API가 페이지에 정의된 경우 SDK는 방문자 API에 ECID를 쿼리합니다. 이 옵션을 사용하면 Adobe Experience Platform 웹 SDK를 사용하여 이중 태그 페이지에 동일한 ECID를 둘 수 있습니다.

### `thirdPartyCookiesEnabled`

| **유형** | **필수 여부** | **기본값** |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style=&quot;table-layout:auto&quot;}

제3자 쿠키 Adobe 설정을 활성화합니다. SDK는 제3자 컨텍스트에서 방문자 ID를 유지하여 여러 사이트에서 동일한 방문자 ID를 사용할 수 있도록 할 수 있습니다. 여러 사이트가 있거나 파트너와 데이터를 공유하려는 경우 이 옵션을 사용합니다.그러나 개인정보 보호 이유로 이 옵션을 원하지 않는 경우도 있습니다.
