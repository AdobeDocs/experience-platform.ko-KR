---
title: Adobe Experience Platform Web SDK 구성
description: Adobe Experience Platform Web SDK를 구성하는 방법을 알아봅니다.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: 구성;구성;SDK;Edge;Web SDK;구성;EdgeConfigId;컨텍스트;웹;장치;환경;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;웹 sdk 설정;사전 숨김Style;불투명도;쿠키DestinationsEnabled;urlDestinationsEnabled;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: a192a746fa227b658fcdb8caa07ea6fb4ac1a944
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 9%

---

# Platform Web SDK 구성

SDK에 대한 구성은 `configure` 명령.

>[!IMPORTANT]
>
>`configure` is *항상* 첫 번째 명령이 호출되었습니다.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

구성 중에 설정할 수 있는 다양한 옵션이 있습니다. 모든 옵션은 카테고리별로 그룹화된 아래에서 찾을 수 있습니다.

## 일반 옵션

### `edgeConfigId`

>[!NOTE]
>
>**Edge Configurations의 브랜드가 데이터 세트로 다시 지정되었습니다. 데이터 스트림 ID는 구성 ID와 동일합니다.**

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | None |

{style="table-layout:auto"}

SDK를 적절한 계정 및 구성에 연결하는 할당된 구성 ID입니다. 단일 페이지 내에서 여러 인스턴스를 구성할 때는 다른 인스턴스를 구성해야 합니다 `edgeConfigId` 참조하십시오.

### `context` {#context}

| **유형** | 필수 여부 | **기본값** |
| ---------------- | ------------ | -------------------------------------------------- |
| 문자열 배열 | 아니요 | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

에 설명된 대로 자동으로 수집할 컨텍스트 카테고리를 나타냅니다. [자동 정보](../data-collection/automatic-information.md). 이 구성을 지정하지 않으면 기본적으로 모든 카테고리가 사용됩니다.

>[!IMPORTANT]
>
>다음을 제외한 모든 컨텍스트 속성 `highEntropyUserAgentHints`은 기본적으로 활성화되어 있습니다. 웹 SDK 구성에서 컨텍스트 속성을 수동으로 지정한 경우 필요한 정보를 계속 수집하려면 모든 컨텍스트 속성을 활성화해야 합니다.

활성화하려면 [높은 엔트로피 클라이언트 힌트](user-agent-client-hints.md#enabling-high-entropy-client-hints) 웹 SDK 배포에서 추가 항목을 포함해야 합니다 `highEntropyUserAgentHints` 컨텍스트 선택 사항, 기존 구성과 함께 제공됩니다.

예를 들어 웹 속성에서 높은 엔트로피 클라이언트 힌트를 검색하려면 구성은 다음과 같습니다.

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `false` |

{style="table-layout:auto"}

디버깅을 활성화할지 여부를 나타냅니다. 이 구성을 로 설정 `true` 는 다음 기능을 활성화합니다.

| **기능** | **함수** |
| ---------------------- | ------------------ |
| 콘솔 로깅 | 브라우저의 JavaScript 콘솔에 디버깅 메시지가 표시되도록 합니다 |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

이 필드를 자사 도메인으로 채웁니다. 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=ko-KR).

도메인은 과 유사합니다 `data.{customerdomain.com}` www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Adobe 서비스와 통신하고 상호 작용하는 데 사용되는 edgeDomain 다음의 경로입니다.  종종 기본 프로덕션 환경을 사용하지 않을 때만 변경됩니다.

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 문자열 | 아니요 | ee |

{style="table-layout:auto"}

### `orgId`

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 문자열 | 예 | None |

{style="table-layout:auto"}

할당된 사용자 [!DNL Experience Cloud] 조직 ID. 페이지 내에서 여러 인스턴스를 구성할 때는 다른 인스턴스를 구성해야 합니다 `orgId` 참조하십시오.

## 데이터 수집

### `clickCollectionEnabled` {#clickCollectionEnabled}

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style="table-layout:auto"}

링크 클릭과 연관된 데이터가 자동으로 수집되는지 여부를 나타냅니다. 자세한 내용은 [자동 링크 추적](../data-collection/track-links.md#automaticLinkTracking) 추가 정보. 링크가 다운로드 속성을 포함하거나 링크가 파일 확장자로 끝나는 경우 링크가 다운로드 링크로 레이블이 지정됩니다. 다운로드 링크 한정자는 정규 표현식으로 구성할 수 있습니다. 기본값은 입니다.`"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 함수 | 아니요 | () => 정의되지 않음 |

{style="table-layout:auto"}

전송되기 바로 전에 모든 이벤트에 대해 호출되는 콜백을 구성합니다. 필드가 있는 개체 `xdm` 콜백으로 전송됩니다. 전송할 내용을 변경하려면 `xdm` 개체. 콜백 내에서 `xdm` 개체에는 이미 이벤트 명령에서 전달된 데이터와 자동으로 수집된 정보가 있습니다. 이 콜백의 시간 및 예제에 대한 자세한 내용은 [이벤트 전역 수정](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 함수 | 아니요 | () => 정의되지 않음 |

{style="table-layout:auto"}

전송되기 바로 전에 모든 링크 클릭 추적 이벤트에 대해 호출되는 콜백을 구성합니다. 콜백에서는 `xdm`, `clickedElement`, 및 `data` 필드.

DOM 요소 구조를 사용하여 링크 추적을 필터링할 때 `clickElement` 명령. `clickedElement` 은 클릭되고 상위 노드 트리를 캡슐화한 DOM 요소 노드입니다.

보내는 데이터를 변경하려면 `xdm` 및/또는 `data` 개체. 콜백 내에서 `xdm` 개체에는 이미 이벤트 명령에서 전달된 데이터와 자동으로 수집된 정보가 있습니다.

* 다음 이외의 값 `false` 은(는) 이벤트가 처리를 수행하고 콜백을 전송할 수 있도록 허용합니다.
* 콜백이 `false` 값, 이벤트 처리가 오류 없이 중지되고 이벤트가 전송되지 않습니다. 이 메커니즘을 사용하면 이벤트 데이터를 검사하고 재방문하여 특정 이벤트를 필터링할 수 있습니다 `false` 이벤트를 전송하지 않아야 하는 경우.
* 콜백에서 예외가 발생하면 이벤트에 대한 처리가 중지되고 이벤트가 전송되지 않습니다.


## 개인 정보 보호 옵션

### `defaultConsent` {#default-consent}

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 오브젝트 | 아니요 | `"in"` |

{style="table-layout:auto"}

사용자의 기본 동의를 설정합니다. 사용자에 대해 이미 저장된 동의 기본 설정이 없는 경우 이 설정을 사용합니다. 다른 유효한 값은 다음과 같습니다 `"pending"` 및 `"out"`. 이 기본값은 사용자 프로필에 지속되지 않습니다. 사용자의 프로필은 `setConsent` 가 호출됩니다.
* `"in"`: 이 설정을 지정하거나 값을 제공하지 않으면 사용자 동의 환경 설정 없이 작업을 계속 진행합니다.
* `"pending"`: 이 설정을 사용하면 사용자가 동의 환경 설정을 제공할 때까지 작업을 큐에 올릴 수 있습니다.
* `"out"`: 이 설정을 지정하면 사용자가 동의 환경 설정을 제공할 때까지 작업이 삭제됩니다.
사용자의 환경 설정이 제공되면 사용자의 환경 설정에 따라 작업이 진행되거나 중단됩니다. 자세한 내용은 [지원 동의](../consent/supporting-consent.md) 추가 정보.

## 개인화 옵션 {#personalization}

### `prehidingStyle` {#prehidingStyle}

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 문자열 | 아니요 | None |

{style="table-layout:auto"}

서버에서 개인화된 콘텐츠를 로드하는 동안 웹 페이지의 콘텐츠 영역을 숨기는 CSS 스타일 정의를 만드는 데 사용됩니다. 이 옵션을 제공하지 않으면 SDK는 개인화된 컨텐츠가 로드되는 동안 컨텐츠 영역을 숨기려 하지 않으므로 &quot;깜박임&quot;이 발생할 수 있습니다.

예를 들어, 웹 페이지의 요소에 `container`: 서버에서 개인화된 콘텐츠를 로드하는 동안 숨기려는 기본 콘텐츠의 사전 숨김 스타일을 사용합니다.

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

이 옵션은 에서 개별 페이지를 마이그레이션할 때 사용해야 합니다 [!DNL at.js] 추가 작업이 필요합니다.

이 옵션을 사용하여 웹 SDK에서 이전 항목을 읽고 쓸 수 있도록 합니다 `mbox` 및 `mboxEdgeCluster` 에서 사용하는 쿠키 [!DNL at.js]. 이렇게 하면 웹 SDK를 사용하는 페이지에서 를 사용하는 페이지로 이동하는 동안 방문자 프로필을 유지할 수 있습니다 [!DNL at.js] 라이브러리 및 그 반대의 경우도 마찬가지입니다.

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `false` |

## 대상 옵션

### `cookieDestinationsEnabled`

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style="table-layout:auto"}

사용 [!DNL Audience Manager] 쿠키 대상. 세그먼트 자격에 따라 쿠키를 설정할 수 있도록 해줍니다.

### `urlDestinationsEnabled`

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style="table-layout:auto"}

사용 [!DNL Audience Manager] 세그먼트 자격에 따라 URL을 실행할 수 있는 URL 대상.

## ID 옵션

### `idMigrationEnabled` {#id-migration-enabled}

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style="table-layout:auto"}

true인 경우 SDK는 이전 AMCV 쿠키를 읽고 설정합니다. 이 옵션은 사이트의 일부 부분이 여전히 Visitor.js를 사용할 수 있지만 Adobe Experience Platform Web SDK를 사용하여 로 전환하는 데 도움이 됩니다.

방문자 API가 페이지에 정의된 경우 SDK는 ECID에 대해 방문자 API를 쿼리합니다. 이 옵션을 사용하면 Adobe Experience Platform Web SDK를 사용하여 페이지를 이중 태깅하고 여전히 동일한 ECID를 가질 수 있습니다.

### `thirdPartyCookiesEnabled`

| 유형 | 필수 여부 | 기본값 |
| -------- | ------------ | ----------------- |
| 부울 | 아니요 | `true` |

{style="table-layout:auto"}

타사 쿠키 Adobe 설정을 활성화합니다. SDK는 타사 컨텍스트에서 방문자 ID를 유지하여 여러 사이트에서 동일한 방문자 ID를 사용할 수 있습니다. 여러 사이트가 있거나 파트너와 데이터를 공유하려는 경우 이 옵션을 사용합니다. 그러나 경우에 따라 이 옵션은 개인 정보용으로 필요하지 않습니다.
