---
title: Platform Web SDK에서 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform Web SDK로 개인화된 컨텐츠를 렌더링하는 방법을 알아봅니다
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisions;코드 조각 사전 숨김;vec;양식 기반 경험 작성기;xdm;대상;결정;범위;스키마;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 202a77e4f9e8c7d5515ea0a5004b1c339f1d58ba
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 3%

---

# [!DNL Platform Web SDK]에서 [!DNL Adobe Target] 사용

[!DNL Adobe Experience Platform] [!DNL Web SDK] 은 에서 관리하는 개인화된 경험을 웹 채널 [!DNL Adobe Target] 에 제공하고 렌더링할 수 있습니다. [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)라고 하는 WYSIWYG 편집기 또는 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)라는 비시각적 인터페이스를 사용하여 활동 및 개인화 경험을 만들고, 활성화하고 전달할 수 있습니다.

다음 기능은 테스트되었으며 현재 [!DNL Target]에서 지원됩니다.

* [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [경험 타깃팅 활동](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [다변량 테스트(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [기본 Target 노출 및 전환 보고](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC 지원](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Adobe Target] 활성화

[!DNL Target]을 활성화하려면 다음을 수행하십시오.

1. 적절한 클라이언트 코드로 [데이터 스트림](../../fundamentals/datastreams.md)에서 [!DNL Target]을 활성화합니다.
1. 이벤트에 `renderDecisions` 옵션을 추가합니다.

그런 다음, 선택적으로 다음 옵션을 추가할 수도 있습니다.

* **`decisionScopes`**:이벤트에 이 옵션을 추가하여 특정 활동(양식 기반 작성기로 만든 활동에 유용함)을 검색합니다.
* **[코드 조각 사전 숨김](../manage-flicker.md)**:페이지의 특정 부분만 숨깁니다.

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
   data: { // Freeform stuff (event & profile) }
});
```

**샘플 코드**

```
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    device: {
      screenWidth: 9999
    }
  },
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
}) 
.then(console.log);
```

## 용어

__결정:__ 에서  [!DNL Target]결정은 활동에서 선택한 경험과 상호 연결됩니다.

__스키마:__ 결정 스키마는 의 오퍼 유형입니다 [!DNL Target].

__범위:__ 결정 범위입니다. [!DNL Target]에서 범위는 mBox입니다. 글로벌 mBox는 `__view__` 범위입니다.

__XDM:__ XDM은 점 표기법으로 직렬화된 다음 mBox 매개  [!DNL Target] 변수로 삽입됩니다.
