---
title: Platform Web SDK에서 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform Web SDK로 개인화된 컨텐츠를 렌더링하는 방법을 알아봅니다
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisions;코드 조각 사전 숨김;vec;양식 기반 경험 작성기;xdm;대상;결정;범위;스키마;시스템 다이어그램;다이어그램
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c99bc94226b296463e92340723d1318e0775f6a7
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 5%

---

# [!DNL Platform Web SDK]에서 [!DNL Adobe Target] 사용

[!DNL Adobe Experience Platform] [!DNL Web SDK] 은 에서 관리하는 개인화된 경험을 웹 채널 [!DNL Adobe Target] 에 제공하고 렌더링할 수 있습니다. [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)라고 하는 WYSIWYG 편집기 또는 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)라는 비시각적 인터페이스를 사용하여 활동 및 개인화 경험을 만들고, 활성화하고 전달할 수 있습니다.

다음 기능은 테스트되었으며 현재 [!DNL Target]에서 지원됩니다.

* [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=ko-KR)
* [Automated Personalization 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [경험 타깃팅 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [다변량 테스트(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations 활동](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [기본 Target 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC 지원](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 시스템 다이어그램

다음 다이어그램은 [!DNL Target] 및 [!DNL Platform Web SDK] Edge Decisioning의 워크플로우를 이해하는 데 도움이 됩니다.

![Platform Web SDK를 사용한 Adobe Target Edge 의사 결정 다이어그램](./assets/target-platform-web-sdk.png)

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 장치가 [!DNL Platform Web SDK]을 로드합니다. [!DNL Platform Web SDK]은(는) XDM 데이터, 데이터 스트림 환경 ID, 전달된 매개 변수 및 고객 ID(선택 사항)를 사용하여 Edge 네트워크에 요청을 보냅니다. 페이지(또는 컨테이너)는 미리 숨겨져 있습니다. |
| 2 | 에지 네트워크는 방문자 ID, 동의 및 지리적 위치 및 장치 친숙한 이름과 같은 기타 방문자 컨텍스트 정보로 보강하기 위해 에지 서비스에 요청을 보냅니다. |
| 3 | 에지 네트워크는 방문자 ID 및 전달된 매개 변수와 함께 [!DNL Target] 에지에 보강된 개인화 요청을 보냅니다. |
| 4 | 프로필 스크립트가 실행된 다음 [!DNL Target] 프로필 저장소에 반영됩니다. 프로필 저장소는 [!UICONTROL 대상 라이브러리]에서 세그먼트를 가져옵니다(예: [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform]에서 공유된 세그먼트). |
| 5 | [!DNL Target] 은 URL 요청 매개 변수 및 프로필 데이터를 기반으로 현재 페이지 보기 및 향후 미리 가져온 보기에 대해 방문자에 대해 표시할 활동 및 경험을 결정합니다. [!DNL Target] 그런 다음 이 파일을 다시 에지 네트워크로 보냅니다. |
| 6 | a. 에지 네트워크는 개인화 응답을 다시 페이지로 보냅니다. 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다. 현재 페이지의 개인화된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br>나. SPA(단일 페이지 애플리케이션)의 사용자 동작으로 표시되는 보기에 대한 개인화된 콘텐츠는 캐시되므로, 보기가 트리거될 때 추가적인 서버 호출 없이 즉시 적용할 수 있습니다&#x200B;.<br>c. 에지 네트워크가 동의, 세션 ID, ID, 쿠키 확인, 개인화 등의 쿠키에 방문자 ID 및 기타 값을 보냅니다. |
| 7 | 에지 네트워크는 [!UICONTROL Target 분석] (A4T) 세부 사항(활동, 경험 및 변환 메타데이터)을 [!DNL Analytics] 에지로 &#x200B; 전달합니다. |

## [!DNL Adobe Target] 활성화

[!DNL Target]을 활성화하려면 다음을 수행하십시오.

1. 적절한 클라이언트 코드로 [데이터 스트림](../../fundamentals/datastreams.md)에서 [!DNL Target]을 활성화합니다.
1. 이벤트에 `renderDecisions` 옵션을 추가합니다.

그런 다음, 선택적으로 다음 옵션을 추가할 수도 있습니다.

* **`decisionScopes`**: 이벤트에 이 옵션을 추가하여 특정 활동(양식 기반 작성기로 만든 활동에 유용함)을 검색합니다.
* **[코드 조각 사전 숨김](../manage-flicker.md)**: 페이지의 특정 부분만 숨깁니다.

## Adobe Target VEC 사용

[!DNL Platform Web SDK] 구현에서 VEC를 사용하려면 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 또는 [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper 확장 프로그램을 설치 및 활성화합니다.

자세한 내용은 *Adobe Target 안내서*&#x200B;에서 [시각적 경험 작성기 Helper 확장 프로그램](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)을 참조하십시오.

## VEC 활동 자동 렌더링

[!DNL Adobe Experience Platform Web SDK]은(는) 사용자를 위해 웹에서 [!DNL Adobe Target]의 VEC를 통해 정의된 경험을 자동으로 렌더링할 수 있는 권한이 있습니다. VEC 활동을 자동으로 렌더링하도록 [!DNL Experience Platform Web SDK]에 나타내려면 `renderDecisions = true` 를 사용하여 이벤트를 보내십시오.

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## 양식 기반 작성기 사용

[양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)는 [!UICONTROL A/B 테스트], [!UICONTROL 경험 타깃팅], [!UICONTROL Automated Personalization] 및 JSON, HTML, 이미지 등과 같은 다른 응답 유형을 갖는 [!UICONTROL Recommendations] 활동을 구성하는 데 유용한 시각적이지 않은 인터페이스입니다. [!DNL Target]에서 반환된 응답 유형 또는 결정에 따라 핵심 비즈니스 로직을 실행할 수 있습니다. 양식 기반 작성기 활동에 대한 결정을 검색하려면 결정을 검색할 모든 &#39;decisionScopes&#39;가 있는 이벤트를 보내십시오.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## 결정 범위

`decisionScopes` 개인화된 경험을 렌더링할 페이지의 섹션, 위치 또는 부분을 정의합니다. 이러한 `decisionScopes`은 사용자 정의 가능하고 사용자가 정의합니다. 현재 [!DNL Target] 고객의 경우 `decisionScopes`을 &quot;mbox&quot;라고도 합니다. [!DNL Target] UI에서 `decisionScopes`이 &quot;위치&quot;로 표시됩니다.

## `__view__` 범위

[!DNL Experience Platform Web SDK]은 VEC 작업을 렌더링하기 위해 SDK에 의존하지 않고 VEC 작업을 검색하는 기능을 제공합니다. `__view__`이 `decisionScopes`로 정의된 이벤트를 보냅니다.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## XDM의 대상

[!DNL Platform Web SDK] 를 통해 전달되는 [!DNL Target] 활동의 대상을 정의할 때 [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=ko)을(를) 정의하고 사용해야 합니다. XDM 스키마, 클래스 및 스키마 필드 그룹을 정의한 후 타깃팅을 위해 XDM 데이터로 정의된 [!DNL Target] 대상 규칙을 만들 수 있습니다. [!DNL Target] 내에 XDM 데이터가 [!UICONTROL Audience Builder]에 사용자 지정 매개 변수로 표시됩니다. XDM은 점 표기법을 사용하여 일련화됩니다(예: `web.webPageDetails.name`).

사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 사전 정의된 대상이 있는 [!DNL Target] 활동이 있는 경우 SDK를 통해 올바로 전달되지 않습니다. 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 대신 XDM을 대신 사용해야 합니다. 그러나 [!DNL Platform Web SDK]을 통해 지원되는 기본 대상 타깃팅 필드는 XDM이 필요하지 않습니다. 이러한 필드는 XDM이 필요하지 않은 [!DNL Target] UI에서 사용할 수 있습니다.

* 타겟 라이브러리
* 지역
* 네트워크
* 운영 체제
* 사이트 페이지
* 브라우저
* 트래픽 소스
* 시간대

자세한 내용은 *Adobe Target 안내서*&#x200B;에서 [대상 카테고리](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en)를 참조하십시오.

### 단일 프로필 업데이트

[!DNL Platform Web SDK]을(를) 사용하면 프로필을 [!DNL Target] 프로필 및 [!DNL Platform Web SDK]에 경험 이벤트로 업데이트할 수 있습니다.

[!DNL Target] 프로필을 업데이트하려면 프로필 데이터가 다음과 같이 전달되는지 확인하십시오.

* `“data {“`
* `“__adobe.target”` 아래
* 접두어 `“profile.”`(예: 아래)

| 키 | 유형 | 설명 |
| --- | --- | --- |
| `renderDecisions` | 부울 | 개인화 구성 요소가 DOM 작업을 해석해야 하는지 여부를 지정합니다 |
| `decisionScopes` | 배열 `<String>` | 결정을 검색할 범위 목록 |
| `xdm` | 개체 | Platform Web SDK에 경험 이벤트로 실행되는 XDM에서 형식이 지정된 데이터 |
| `data` | 개체 | 대상 클래스 아래의 [!DNL Target] 솔루션으로 전송된 임의 키/값 쌍입니다. |

이 명령을 사용하는 일반적인 [!DNL Platform Web SDK] 코드는 다음과 같습니다.

**`sendEvent`프로필 데이터 사용**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**프로필 속성을 Adobe Target에 보내는 방법:**

```
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

다음 표에는 [!DNL Recommendations] 속성과 [!DNL Platform Web SDK]을 통해 각 속성이 지원되는지 여부가 나열되어 있습니다.

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

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## 디버깅

mboxTrace 및 mboxDebug는 더 이상 사용되지 않습니다. [[!DNL Platform Web SDK] 디버깅](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html)을 사용하십시오.

## 용어

__결정:__ 에서  [!DNL Target]결정은 활동에서 선택한 경험과 상호 연결됩니다.

__스키마:__ 결정 스키마는 의 오퍼 유형입니다 [!DNL Target].

__범위:__ 결정 범위입니다. [!DNL Target]에서 범위는 mBox입니다. 글로벌 mBox는 `__view__` 범위입니다.

__XDM:__ XDM은 점 표기법으로 직렬화된 다음 mBox 매개  [!DNL Target] 변수로 삽입됩니다.
