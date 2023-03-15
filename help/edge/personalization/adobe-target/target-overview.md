---
title: Platform Web SDK로 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform Web SDK를 사용하여 개인화된 콘텐츠를 렌더링하는 방법에 대해 알아봅니다
keywords: target;adobe target;activity.id;experience.id;renderDecisions;의사 결정 범위;코드 조각 사전 숨김;vec;양식 기반 경험 작성기;xdm;대상;의사 결정;범위;스키마;시스템 다이어그램;다이어그램
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 6%

---

# 사용 [!DNL Adobe Target] (으)로 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 에서 관리되는 개인화된 경험을 제공하고 렌더링할 수 있습니다. [!DNL Adobe Target] 웹 채널에 연결합니다. 라는 WYSIWYG 편집기를 사용할 수 있습니다. [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) 또는 비시각적 인터페이스인 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)을 추가하여 활동 및 개인화 경험을 만들고, 활성화하고, 제공할 수 있습니다.

>[!IMPORTANT]
>
>다음 [Adobe Target 설명서](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) Target 기능 및 기능과 관련된 Platform Web SDK에 대한 정보가 포함된 항목이 포함되어 있습니다.

다음 기능이 테스트되었으며 현재 지원됨 [!DNL Target]:

* [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [경험 타깃팅 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [다변량 테스트(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [권장 사항 활동](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [기본 Target 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC 지원](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 시스템 다이어그램

다음 다이어그램은 의 워크플로를 이해하는 데 도움이 됩니다 [!DNL Target] 및 [!DNL Platform Web SDK] edge decisioning

![Platform Web SDK를 사용한 Adobe Target Edge Decisioning 다이어그램](./assets/target-platform-web-sdk.png)

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 장치가 를 로드합니다 [!DNL Platform Web SDK]. 다음 [!DNL Platform Web SDK] xdm 데이터, 데이터스트림 환경 ID, 전달된 매개 변수 및 고객 ID(선택 사항)가 있는 Edge Network에 요청을 보냅니다. 페이지(또는 컨테이너)가 미리 숨겨져 있습니다. |
| 2 | Edge 네트워크는 Edge 서비스에 요청을 전송하여 방문자 ID, 동의와 지리적 위치 및 장치 친화적 이름과 같은 기타 방문자 컨텍스트 정보로 보강합니다. |
| 3 | Edge 네트워크는 보강된 개인화 요청을 로 보냅니다. [!DNL Target] 방문자 ID 및 전달된 매개 변수를 사용하는 edge. |
| 4 | 프로필 스크립트가 실행된 다음 로 피드 [!DNL Target] 프로필 스토리지. 프로필 스토리지는 [!UICONTROL 대상 라이브러리] (예:에서 공유된 세그먼트) [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | URL 요청 매개 변수 및 프로필 데이터를 기반으로 [!DNL Target] 현재 페이지 보기 및 향후 프리페치된 보기에 대해 방문자에게 표시할 활동 및 경험을 결정합니다. [!DNL Target] 그런 다음 이를 edge network로 다시 전송합니다. |
| 6 | a. 에지 네트워크는 추가적인 개인화를 위한 프로필 값을 선택적으로 포함하여 개인화 응답을 다시 페이지로 전송합니다. 현재 페이지의 개인화된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br>b. SPA(단일 페이지 애플리케이션)에서 사용자 작업의 결과로 표시되는 보기를 위한 개인화된 컨텐츠는 캐시되므로 보기가 트리거될 때 추가적인 서버 호출 없이 즉시 적용할 수 있습니다. <br>c. Edge 네트워크는 방문자 ID와 동의, 세션 ID, ID, 쿠키 확인, 개인화 등과 같은 쿠키의 다른 값을 전송합니다. |
| 7 | 에지 네트워크가 전달됩니다. [!UICONTROL Target 분석] (A4T) 세부 사항(활동, 경험 및 전환 메타데이터) [!DNL Analytics] edge. |

## 활성화 중 [!DNL Adobe Target]

활성화하려면 [!DNL Target]를 사용하여 다음을 수행합니다.

1. 사용 [!DNL Target] (으)로 [데이터스트림](../../datastreams/overview.md) 적절한 클라이언트 코드로 만듭니다.
1. 추가 `renderDecisions` 이벤트 옵션

그런 다음 선택적으로 다음 옵션을 추가할 수도 있습니다.

* **`decisionScopes`**: 이 옵션을 이벤트에 추가하여 특정 활동(양식 기반 작성기로 만든 활동에 유용함)을 검색합니다.
* **[코드 조각 사전 숨김](../manage-flicker.md)**: 페이지의 특정 부분만 숨깁니다.

## Adobe Target VEC 사용

에 VEC를 사용하려면 [!DNL Platform Web SDK] 구현, 설치 및 활성화 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [크롬](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper 확장 프로그램.

자세한 내용은 [시각적 경험 작성기 Helper 확장 프로그램](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 다음에서 *Adobe Target 안내서*.

## 개인화된 콘텐츠 렌더링

다음을 참조하십시오 [개인화 콘텐츠 렌더링](../rendering-personalization-content.md) 추가 정보.

## XDM의 대상

다음에 대한 대상자를 정의할 때 [!DNL Target] 를 통해 제공되는 활동 [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR) 을(를) 정의하고 사용해야 합니다. XDM 스키마, 클래스 및 스키마 필드 그룹을 정의한 후 [!DNL Target] 타깃팅용 XDM 데이터로 정의된 대상 규칙. 다음 범위 내 [!DNL Target], XDM 데이터가에 표시됨 [!UICONTROL Audience Builder] 를 사용자 지정 매개 변수로 사용하십시오. XDM은 점 표기법을 사용하여 serialize됩니다(예: `web.webPageDetails.name`).

다음을 보유한 경우: [!DNL Target] 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 사전 정의된 대상이 있는 활동은 SDK를 통해 올바르게 전달되지 않습니다. 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 대신 XDM을 사용해야 합니다. 하지만 를 통해 지원되는 기본 대상자 타겟팅 필드가 있습니다. [!DNL Platform Web SDK] XDM이 필요하지 않습니다. 다음 필드는 [!DNL Target] XDM이 필요하지 않은 UI:

* 타겟 라이브러리
* 지역
* 네트워크
* 운영 체제
* 사이트 페이지
* 브라우저
* 트래픽 소스
* 시간대

자세한 내용은 [대상의 카테고리](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) 다음에서 *Adobe Target 안내서*.

### 응답 토큰

응답 토큰은 주로 Google, Facebook 등과 같은 서드파티에 메타데이터를 전송하는 데 사용됩니다. 응답 토큰은에서 반환됩니다. `meta` 다음 범위 내의 필드 `propositions` -> `items`. 다음은 샘플입니다.

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

응답 토큰을 수집하려면에 가입해야 합니다. `alloy.sendEvent` 약속, 반복 `propositions`
및 세부 정보 추출 `items` -> `meta`. 매 `proposition` 다음 포함 `renderAttempted` 다음 여부를 나타내는 부울 필드 `proposition` 렌더링되었는지 여부입니다. 아래 샘플을 참조하십시오.

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
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

* 양식 기반 작성기 기반 `propositions` 포함 `renderAttempted` 플래그가 로 설정됨 `false`
* 다음을 포함하는 시각적 경험 작성기 기반 제안 `renderAttempted` 플래그가 로 설정됨 `false`
* 을 사용하는 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안 `renderAttempted` 플래그가 로 설정됨 `false`

#### 보기 - 변경(캐시된 보기):

* 을 사용하는 단일 페이지 애플리케이션 보기에 대한 시각적 경험 작성기 기반 제안 `renderAttempted` 플래그가 로 설정됨 `false`

### 단일 프로필 업데이트

다음 [!DNL Platform Web SDK] 프로필을 로 업데이트할 수 있습니다. [!DNL Target] 프로필 및 대상 [!DNL Platform Web SDK] 경험 이벤트.

를 업데이트하려면 [!DNL Target] 프로필, 프로필 데이터가 다음과 함께 전달되는지 확인합니다.

* `“data {“`
* `“__adobe.target”`
* 접두사 `“profile.”` 예: 아래와 같이

| 키 | 유형 | 설명 |
| --- | --- | --- |
| `renderDecisions` | 부울 | DOM 작업을 해석해야 하는지 여부를 개인화 구성 요소에 지시합니다. |
| `decisionScopes` | 배열 `<String>` | 결정을 검색할 범위 목록 |
| `xdm` | 오브젝트 | Platform Web SDK에 경험 이벤트로 전송되는 XDM 형식의 데이터 |
| `data` | 오브젝트 | 에 전송된 임의 키/값 쌍 [!DNL Target] target 클래스 아래에 있는 솔루션. |

일반 [!DNL Platform Web SDK] 이 명령을 사용하는 코드는 다음과 같습니다.

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
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 권장 사항 요청

다음 표에는 [!DNL Recommendations] 속성 및 다음을 통해 각 속성 지원 여부 [!DNL Platform Web SDK]:

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
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## 디버깅

mboxTrace 및 mboxDebug는 더 이상 사용되지 않습니다. 사용 [[!DNL Platform Web SDK] 디버깅](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## 용어

__제안:__ 위치 [!DNL Target], propositions는 활동에서 선택한 경험과 관련이 있습니다.

__스키마:__ 의사 결정 스키마는 의 오퍼 유형입니다. [!DNL Target].

__범위:__ 결정의 범위. 위치 [!DNL Target], 범위는 mBox입니다. 글로벌 mBox는 `__view__` 범위.

__XDM:__ XDM은 점 표기법으로 일련화된 다음 로 입력됩니다. [!DNL Target] 를 mBox 매개 변수로 사용합니다.
