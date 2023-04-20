---
title: Platform Web SDK에서 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform Web SDK로 개인화된 컨텐츠를 렌더링하는 방법을 알아봅니다
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisions;코드 조각 사전 숨김;vec;양식 기반 경험 작성기;xdm;대상;결정;범위;스키마;시스템 다이어그램;다이어그램
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 5a048505be139b58dbb3bf85120df5e3cc46881e
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 6%

---

# 사용 [!DNL Adobe Target] 사용 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 에서 관리하는 개인화된 경험을 제공하고 렌더링할 수 있습니다. [!DNL Adobe Target] 참조하십시오. 라는 WYSIWYG 편집기를 사용할 수 있습니다. [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) 또는 비시각적 인터페이스에서 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), 활동 및 개인화 경험을 만들고, 활성화하고, 전달하는 데 사용됩니다.

>[!IMPORTANT]
>
>를 사용하여 Target 구현을 Platform Web SDK로 마이그레이션하는 방법을 배웁니다. [at.js 2.x에서 Platform Web SDK로 Target 마이그레이션](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) 자습서입니다.
>
>를 사용하여 처음으로 Target을 구현하는 방법을 알아봅니다. [웹 SDK를 사용하여 Adobe Experience Cloud 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR) 자습서입니다. Target 관련 정보는 라는 자습서 섹션을 참조하십시오. [Platform Web SDK를 사용하여 Target 설정](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


다음 기능은 테스트되었으며 현재 [!DNL Target]:

* [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [경험 타깃팅 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [다변량 테스트(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [권장 사항 활동](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [기본 Target 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC 지원](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 시스템 다이어그램

다음 다이어그램은 [!DNL Target] 및 [!DNL Platform Web SDK] edge decisioning.

![Platform Web SDK를 사용한 Adobe Target Edge 의사 결정 다이어그램](./assets/target-platform-web-sdk.png)

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 장치는 [!DNL Platform Web SDK]. 다음 [!DNL Platform Web SDK] XDM 데이터, 데이터 스트림 환경 ID, 전달된 매개 변수 및 고객 ID(선택 사항)를 사용하여 에지 네트워크에 요청을 보냅니다. 페이지(또는 컨테이너)는 미리 숨겨져 있습니다. |
| 2 | 에지 네트워크는 방문자 ID, 동의 및 지리적 위치 및 장치 친숙한 이름과 같은 기타 방문자 컨텍스트 정보로 보강하기 위해 에지 서비스에 요청을 보냅니다. |
| 3 | 에지 네트워크에서 보강한 개인화 요청을 [!DNL Target] edge에 사용할 수 있습니다. |
| 4 | 프로필 스크립트가 실행된 다음 [!DNL Target] 프로필 저장소. 프로필 저장소는 [!UICONTROL 대상 라이브러리] (예: [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]). |
| 5 | URL 요청 매개 변수 및 프로필 데이터를 기반으로, [!DNL Target] 현재 페이지 보기 및 미리 가져온 보기에 대해 방문자에 대해 표시할 활동 및 경험을 결정합니다. [!DNL Target] 그런 다음 이 파일을 다시 에지 네트워크로 보냅니다. |
| 6 | a. 에지 네트워크는 개인화 응답을 다시 페이지로 보냅니다. 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다. 현재 페이지의 개인화된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br>나. SPA(단일 페이지 애플리케이션)에서 사용자 작업의 결과로 표시되는 보기에 대한 개인화된 콘텐츠는 캐시되므로, 보기가 트리거될 때 추가 서버 호출 없이 즉시 적용할 수 있습니다. <br>c. 에지 네트워크가 동의, 세션 ID, ID, 쿠키 확인, 개인화 등의 쿠키에 방문자 ID 및 기타 값을 보냅니다. |
| 7 | 에지 네트워크가 앞으로 이동합니다. [!UICONTROL Target 분석] (A4T) 세부 정보(활동, 경험 및 전환 메타데이터)를에 [!DNL Analytics] edge. |

## 활성화 [!DNL Adobe Target]

활성화하려면 [!DNL Target]를 채울 때 다음을 수행합니다.

1. 활성화 [!DNL Target] 다음 위치에서 [데이터 스트림](../../datastreams/overview.md) 적절한 클라이언트 코드 사용.
1. 추가 `renderDecisions` 선택 사항을 이벤트에 추가합니다.

그런 다음, 선택적으로 다음 옵션을 추가할 수도 있습니다.

* **`decisionScopes`**: 이벤트에 이 옵션을 추가하여 특정 활동(양식 기반 작성기로 만든 활동에 유용함)을 검색합니다.
* **[코드 조각 사전 숨김](../manage-flicker.md)**: 페이지의 특정 부분만 숨깁니다.

## Adobe Target VEC 사용

와 함께 VEC를 사용하려면 [!DNL Platform Web SDK] 구현, 설치 및 활성화 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper 확장 프로그램.

자세한 내용은 [시각적 경험 작성기 Helper 확장 프로그램](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 에서 *Adobe Target 안내서*.

## 개인화된 콘텐츠 렌더링

자세한 내용은 [개인화 콘텐츠 렌더링](../rendering-personalization-content.md) 추가 정보.

## XDM의 대상

대상자를 정의할 때 [!DNL Target] 를 통해 전달되는 활동 [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko-KR) 를 정의하고 사용해야 합니다. XDM 스키마, 클래스 및 스키마 필드 그룹을 정의한 후에는 [!DNL Target] 타깃팅을 위해 XDM 데이터에 의해 정의된 대상 규칙. 내 [!DNL Target], XDM 데이터는 [!UICONTROL Audience Builder] 를 사용자 지정 매개 변수로 사용하십시오. XDM은 점 표기법을 사용하여 일련화됩니다(예: `web.webPageDetails.name`).

만약 [!DNL Target] 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 사전 정의된 대상이 있는 활동은 SDK를 통해 올바로 전달되지 않습니다. 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 대신 XDM을 대신 사용해야 합니다. 그러나 를 통해 지원되는 기본 대상 타깃팅 필드가 있습니다 [!DNL Platform Web SDK] XDM이 필요하지 않습니다. 이러한 필드는 [!DNL Target] XDM이 필요하지 않은 UI:

* 타겟 라이브러리
* 지역
* 네트워크
* 운영 체제
* 사이트 페이지
* 브라우저
* 트래픽 소스
* 시간대

자세한 내용은 [대상의 카테고리](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) 에서 *Adobe Target 안내서*.

### 응답 토큰

응답 토큰은 주로 Google, Facebook 등과 같은 타사에 메타데이터를 전송하는 데 사용됩니다. 응답 토큰은 `meta` 내 필드 `propositions` -> `items`. 다음은 샘플입니다.

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

응답 토큰을 수집하려면 `alloy.sendEvent` 약속, 반복 `propositions`
세부 사항을 `items` -> `meta`. 모두 `proposition` 에 `renderAttempted` 부울 필드 `proposition` 이 렌더링되었거나 렌더링되지 않았습니다. 아래 샘플을 참조하십시오.

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

자동 렌더링 이 활성화되면 Proposition 배열에 다음이 포함됩니다.

#### 페이지 로드 시:

* 양식 기반 작성기 기반 `propositions` with `renderAttempted` 로 설정된 플래그 `false`
* 시각적 경험 작성기 기반 제안 사항 `renderAttempted` 로 설정된 플래그 `true`
* 다음 아이콘을 사용하여 단일 페이지 애플리케이션 보기를 위한 시각적 경험 작성기 기반 제안 `renderAttempted` 로 설정된 플래그 `true`

#### 보기 시 - 변경(캐시된 보기의 경우):

* 다음 아이콘을 사용하여 단일 페이지 애플리케이션 보기를 위한 시각적 경험 작성기 기반 제안 `renderAttempted` 로 설정된 플래그 `true`

자동 렌더링 이 비활성화되면 Proposition 배열에 다음이 포함됩니다.

#### 페이지 로드 시:

* 양식 기반 작성기 기반 `propositions` with `renderAttempted` 로 설정된 플래그 `false`
* 시각적 경험 작성기 기반 제안 사항 `renderAttempted` 로 설정된 플래그 `false`
* 다음 아이콘을 사용하여 단일 페이지 애플리케이션 보기를 위한 시각적 경험 작성기 기반 제안 `renderAttempted` 로 설정된 플래그 `false`

#### 보기 시 - 변경(캐시된 보기의 경우):

* 다음 아이콘을 사용하여 단일 페이지 애플리케이션 보기를 위한 시각적 경험 작성기 기반 제안 `renderAttempted` 로 설정된 플래그 `false`

### 단일 프로필 업데이트

다음 [!DNL Platform Web SDK] 프로필을 로 업데이트할 수 있습니다. [!DNL Target] 프로필 및 [!DNL Platform Web SDK] 를 경험 이벤트로 사용하십시오.

를 업데이트하려면 [!DNL Target] 프로필에서 프로필 데이터가 다음과 같이 전달되는지 확인하십시오.

* `"data {"`
* `"__adobe.target"`
* 접두사 `"profile."` 예: 아래

| 키 | 유형 | 설명 |
| --- | --- | --- |
| `renderDecisions` | 부울 | 개인화 구성 요소가 DOM 작업을 해석해야 하는지 여부를 지정합니다 |
| `decisionScopes` | 어레이 `<String>` | 결정을 검색할 범위 목록 |
| `xdm` | 오브젝트 | Platform Web SDK에 경험 이벤트로 실행되는 XDM에서 형식이 지정된 데이터 |
| `data` | 오브젝트 | 에 전송되는 임의 키/값 쌍 [!DNL Target] target 클래스의 솔루션. |

일반 [!DNL Platform Web SDK] 이 명령을 사용하는 코드는 다음과 같습니다.

**`sendEvent`프로필 데이터 사용**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**프로필 속성을 Adobe Target에 보내는 방법:**

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

다음 테이블 목록 [!DNL Recommendations] 속성 및 각 속성이 [!DNL Platform Web SDK]:

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
| 카테고리 친화성에 대한 페이지 또는 항목 카테고리 | user.categoryId | 지원됨 |

**Recommendations 특성을 Adobe Target에 보내는 방법:**

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

__제안:__ in [!DNL Target], proposition 은 활동에서 선택한 경험에 상호 연결됩니다.

__스키마:__ 결정 스키마는 의 오퍼 유형입니다 [!DNL Target].

__범위:__ 결정의 범위입니다. in [!DNL Target]이고, 범위는 mBox입니다. 글로벌 mBox는 `__view__` 범위.

__XDM:__ XDM은 점 표기법으로 직렬화된 다음 [!DNL Target] 매개 변수로 사용됩니다.
