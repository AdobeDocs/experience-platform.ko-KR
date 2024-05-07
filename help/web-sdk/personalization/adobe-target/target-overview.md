---
title: 개인화에 Web SDK와 함께 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform Web SDK를 사용하여 개인화된 콘텐츠를 렌더링하는 방법에 대해 알아봅니다
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: a34204eb58ed935831d26caf062ebb486039669f
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 4%

---

# 사용 [!DNL Adobe Target] 및 [!DNL Web SDK] 개인화용

[!DNL Adobe Experience Platform] [!DNL Web SDK] 에서 관리되는 개인화된 경험을 제공하고 렌더링할 수 있습니다. [!DNL Adobe Target] 웹 채널에 연결합니다. 라는 WYSIWYG 편집기를 사용할 수 있습니다. [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) 또는 비시각적 인터페이스인 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)을 추가하여 활동 및 개인화 경험을 만들고, 활성화하고, 제공할 수 있습니다.

>[!IMPORTANT]
>
>를 사용하여 Target 구현을 Platform Web SDK로 마이그레이션하는 방법에 대해 알아봅니다. [Target을 at.js 2.x에서 Platform Web SDK로 마이그레이션](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) 튜토리얼.
>
>를 사용하여 처음으로 Target을 구현하는 방법을 알아봅니다. [Web SDK를 사용하여 Adobe Experience Cloud 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR) 튜토리얼. Target에 대한 자세한 내용은 다음 제목의 자습서 섹션을 참조하십시오 [Platform Web SDK를 사용하여 Target 설정](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


다음 기능이 테스트되었으며 현재 지원됨 [!DNL Target]:

* [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [경험 타깃팅 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [다변량 테스트(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations 활동](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [기본 타겟 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC 지원](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] 시스템 다이어그램

다음 다이어그램은 의 워크플로를 이해하는 데 도움이 됩니다 [!DNL Target] 및 [!DNL Web SDK] edge decisioning

![Platform Web SDK를 사용한 Adobe Target Edge Decisioning 다이어그램](assets/target-platform-web-sdk-new.png)

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 장치가 를 로드합니다 [!DNL Web SDK]. 다음 [!DNL Web SDK] xdm 데이터, 데이터스트림 환경 ID, 전달된 매개 변수 및 고객 ID(선택 사항)가 있는 Edge Network에 요청을 보냅니다. 페이지(또는 컨테이너)가 미리 숨겨져 있습니다. |
| 2 | Edge Network은 Edge Services에 요청을 전송하여 방문자 ID, 동의 및 지리적 위치 및 장치에 친숙한 이름과 같은 기타 방문자 컨텍스트 정보로 보강합니다. |
| 3 | Edge Network이 보강된 개인화 요청을 로 보냅니다. [!DNL Target] 방문자 ID 및 전달된 매개 변수를 사용하는 edge. |
| 4 | 프로필 스크립트가 실행된 다음 로 피드 [!DNL Target] 프로필 스토리지. 프로필 스토리지는 [!UICONTROL 대상 라이브러리] (예:에서 공유된 세그먼트) [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | URL 요청 매개 변수 및 프로필 데이터를 기반으로 [!DNL Target] 현재 페이지 보기 및 향후 프리페치된 보기에 대해 방문자에게 표시할 활동 및 경험을 결정합니다. [!DNL Target] 그런 다음 이 파일을 다시 Edge Network으로 보냅니다. |
| 6 | a. Edge Network은 추가적인 개인화를 위한 프로필 값을 선택적으로 포함하여 개인화 응답을 다시 페이지로 전송합니다. 현재 페이지의 개인화된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br>b. SPA(단일 페이지 애플리케이션)에서 사용자 작업의 결과로 표시되는 보기를 위한 개인화된 컨텐츠는 캐시되므로 보기가 트리거될 때 추가적인 서버 호출 없이 즉시 적용할 수 있습니다. <br>c. Edge Network이 방문자 ID와 동의, 세션 ID, ID, 쿠키 확인, 개인화와 같은 쿠키의 다른 값을 보냅니다. |
| 7 | Web SDK는 디바이스에서 Edge Network으로 알림을 전송합니다. |
| 8 | Edge Network 전달 [!UICONTROL Analytics for Target] (A4T) 세부 사항(활동, 경험 및 전환 메타데이터) [!DNL Analytics] edge. |

## 활성화 중 [!DNL Adobe Target]

활성화하려면 [!DNL Target]를 사용하여 다음을 수행합니다.

1. 사용 [!DNL Target] (으)로 [데이터스트림](../../../datastreams/overview.md) 적절한 클라이언트 코드로 만듭니다.
1. 추가 `renderDecisions` 이벤트 옵션

그런 다음 선택적으로 다음 옵션을 추가할 수도 있습니다.

* **`decisionScopes`**: 이 옵션을 이벤트에 추가하여 특정 활동(양식 기반 작성기로 만든 활동에 유용함)을 검색합니다.
* **[코드 조각 사전 숨김](../manage-flicker.md)**: 페이지의 특정 부분만 숨깁니다.

## Adobe Target VEC 사용

에 VEC를 사용하려면 [!DNL Web SDK] 구현, 설치 및 활성화 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [크롬](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper 확장 프로그램.

자세한 내용은 [시각적 경험 작성기 Helper 확장 프로그램](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 다음에서 *Adobe Target 안내서*.

## 개인화된 콘텐츠 렌더링

다음을 참조하십시오 [개인화 콘텐츠 렌더링](../rendering-personalization-content.md) 추가 정보.

## XDM의 대상

다음에 대한 대상자를 정의할 때 [!DNL Target] 를 통해 제공되는 활동 [!DNL Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR) 을(를) 정의하고 사용해야 합니다. XDM 스키마, 클래스 및 스키마 필드 그룹을 정의한 후 [!DNL Target] 타깃팅용 XDM 데이터로 정의된 대상 규칙. 다음 범위 내 [!DNL Target], XDM 데이터가에 표시됨 [!UICONTROL Audience Builder] 를 사용자 지정 매개 변수로 사용하십시오. XDM은 점 표기법을 사용하여 serialize됩니다(예: `web.webPageDetails.name`).

다음을 보유한 경우: [!DNL Target] 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 사전 정의된 대상이 있는 활동은 SDK를 통해 올바르게 전달되지 않습니다. 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 대신 XDM을 사용해야 합니다. 하지만 를 통해 지원되는 기본 대상자 타겟팅 필드가 있습니다. [!DNL Web SDK] XDM이 필요하지 않습니다. 다음 필드는 [!DNL Target] XDM이 필요하지 않은 UI:

* 타겟 라이브러리
* 지역
* 네트워크
* 운영 체제
* 사이트 페이지
* 브라우저
* 트래픽 소스
* 시간대

자세한 내용은 [대상의 카테고리](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) 다음에서 *Adobe Target 안내서*.

### 응답 토큰

응답 토큰은 Google 또는 Facebook과 같은 서드파티로 메타데이터를 전송하는 데 사용됩니다. 응답 토큰은에서 반환됩니다. `meta` 다음 범위 내의 필드 `propositions` -> `items`. 다음은 샘플입니다.

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

응답 토큰을 수집하려면에 가입해야 합니다. `alloy.sendEvent` 약속, 반복 `propositions`및 세부 정보를 추출할 위치: `items` -> `meta`.

매 `proposition` 다음 포함 `renderAttempted` 다음 여부를 나타내는 부울 필드 `proposition` 렌더링되었는지 여부입니다. 아래 샘플을 참조하십시오.

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

자동 렌더링이 활성화된 경우 제안 배열에 다음이 포함됩니다.

#### 페이지 로드 시:

* 양식 기반 작성기 기반 `propositions` 포함 `renderAttempted` 플래그가 로 설정됨 `false`
* 다음을 포함하는 시각적 경험 작성기 기반 제안 `renderAttempted` 플래그가 로 설정됨 `true`
* 을 사용하는 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안 `renderAttempted` 플래그가 로 설정됨 `true`

#### 보기 - 변경(캐시된 보기):

* 을 사용하는 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안 `renderAttempted` 플래그가 로 설정됨 `true`

자동 렌더링이 비활성화되면 제안 배열에 다음이 포함됩니다.

#### 페이지 로드 시:

* [!DNL Form-based Composer]기반 `propositions` 포함 `renderAttempted` 플래그가 로 설정됨 `false`
* [!DNL Visual Experience Composer]다음을 포함한 기반 제안 `renderAttempted` 플래그가 로 설정됨 `false`
* [!DNL Visual Experience Composer]를 사용하는 단일 페이지 애플리케이션 보기에 대한 기반 제안 `renderAttempted` 플래그가 로 설정됨 `false`

#### 보기 - 변경(캐시된 보기):

* 을 사용하는 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안 `renderAttempted` 플래그가 로 설정됨 `false`

### 단일 프로필 업데이트

다음 [!DNL Web SDK] 프로필을 로 업데이트할 수 있습니다. [!DNL Target] 프로필 및 대상 [!DNL Web SDK] 경험 이벤트.

를 업데이트하려면 [!DNL Target] 프로필, 프로필 데이터가 다음과 함께 전달되는지 확인합니다.

* 아래 `"data {"`
* 아래 `"__adobe.target"`
* 접두사 `"profile."`

| 키 | 유형 | 설명 |
| --- | --- | --- |
| `renderDecisions` | 부울 | DOM 작업을 해석해야 하는지 여부를 개인화 구성 요소에 지시합니다. |
| `decisionScopes` | 배열 `<String>` | 결정을 검색할 범위 목록 |
| `xdm` | 오브젝트 | 웹 SDK에 경험 이벤트로 전송되는 XDM 형식의 데이터 |
| `data` | 오브젝트 | 에 전송된 임의 키/값 쌍 [!DNL Target] target 클래스 아래에 있는 솔루션. |

일반 [!DNL Web SDK] 이 명령을 사용하는 코드는 다음과 같습니다.

**콘텐츠가 최종 사용자에게 표시될 때까지 프로필 또는 엔티티 매개 변수 저장 지연**

콘텐츠가 표시될 때까지 프로필의 기록 속성을 지연하려면 을 설정합니다 `data.adobe.target._save=false` 을 참조하십시오.

예를 들어 웹 사이트에는 웹 사이트의 세 범주 링크(남성, 여성 및 아동)에 해당하는 세 가지 결정 범위가 포함되어 있으며 사용자가 최종적으로 방문한 범주를 추적하려고 합니다. 이 요청을 (으)로 보내기 `__save` 플래그가 로 설정됨 `false` 콘텐츠가 요청된 시간에 범주가 유지되지 않도록 합니다. 콘텐츠가 시각화되면 적절한 페이로드(포함)를 `eventToken` 및 `stateToken`)를 입력하여 해당 속성을 기록합니다.

<!--Save profile or entity attributes by default with:

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "__save" : true // Optional. __save=true is the default 
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt",
        "entity.id" : "1234",
      }
    }
  }
} ) ; 
```
-->

아래 예제에서는 trackEvent 스타일 메시지를 보내고, 프로필 스크립트를 실행하고, 속성을 저장하고, 이벤트를 즉시 기록합니다.

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt" ,
        "entity.id" : "1234" ,
        "track": {
          "scopes": [ "mbox1", "mbox2"],
          "type": "display|click|..."
        }
      }
    }
  }
} ) ;
```

>[!NOTE]
>
>다음과 같은 경우 `__save` 지시문이 생략되어 프로필 및 엔티티 속성을 저장하는 것은 요청이 실행된 것처럼, 요청의 나머지 부분이 개인화의 미리 가져오기인 경우에도 즉시 수행됩니다. 다음 `__save` 지시어는 프로필 및 엔티티 속성에만 관련이 있습니다. 추적 개체가 있으면 `__save` 지시문이 무시됩니다. 데이터가 즉시 저장되고 알림이 기록됩니다.

**`sendEvent`프로필 데이터 포함**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Adobe Target에 프로필 속성을 보내는 방법:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 권장 사항 요청

다음 표에는 [!DNL Recommendations] 속성 및 다음을 통해 각 속성 지원 여부 [!DNL Web SDK]:

| 카테고리 | 속성 | 지원 상태 |
| --- | --- | --- |
| Recommendations - 기본 엔티티 속성 | entity.id | 지원됨 |
|  | entity.name | 지원됨 |
|  | entity.categoryId | 지원됨 |
|  | entity.pageUrl | 지원됨 |
|  | entity.thumbnailUrl | 지원됨 |
|  | entity.message | 지원됨 |
|  | entity.value | 지원됨 |
|  | entity.inventory | 지원됨 |
|  | entity.brand | 지원됨 |
|  | entity.margin | 지원됨 |
|  | entity.event.detailsOnly | 지원됨 |
| Recommendations - 사용자 지정 엔티티 속성 | entity.yourCustomAttributeName | 지원됨 |
| Recommendations - 예약된 mbox/페이지 매개 변수 | excludedIds | 지원됨 |
|  | cartIds | 지원됨 |
|  | productPurchasedId | 지원됨 |
| 카테고리 관심도에 대한 페이지 또는 항목 카테고리 | user.categoryId | 지원됨 |

**Recommendations 속성을 Adobe Target으로 보내는 방법:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## 디버깅

mboxTrace 및 mboxDebug는 더 이상 사용되지 않습니다. 의 메서드 사용 [Web SDK 디버깅](/help/web-sdk/use-cases/debugging.md) 대신,

## 용어

__제안:__ 위치 [!DNL Adobe Target], propositions는 활동에서 선택한 경험과 관련이 있습니다.

__스키마:__ 의사 결정 스키마는 의 오퍼 유형입니다. [!DNL Adobe Target].

__범위:__ 결정의 범위. 위치 [!DNL Adobe Target], 범위는 mBox입니다. 글로벌 mBox는 `__view__` 범위.

__XDM:__ XDM은 점 표기법으로 일련화된 다음 로 입력됩니다. [!DNL Adobe Target] 를 mBox 매개 변수로 사용합니다.
