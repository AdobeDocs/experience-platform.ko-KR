---
title: 'Adobe Target 및 Adobe Experience Platform 웹 SDK. '
seo-title: Adobe Experience Platform 웹 SDK 및 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform 웹 SDK로 개인화된 컨텐츠를 렌더링하는 방법 학습
seo-description: Adobe Target을 사용하여 Experience Platform 웹 SDK로 개인화된 컨텐츠를 렌더링하는 방법 학습
keywords: target;adobe target;activity.id;experience.id;renderDecisions;decisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;audiences;decisions;scope;schema;
translation-type: tm+mt
source-git-commit: d069b3007265406367ca9de2b85540b2a070cf36
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 3%

---


# [!DNL Target] 개요

Adobe Experience Platform은 Adobe Target에서 관리하는 개인화된 경험을 웹 채널에 전달하고 렌더링할 [!DNL Web SDK] 수 있습니다. VEC( [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) )라고 하는 WYSIWYG 편집기 또는 [양식 기반 Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)비시각적 인터페이스를 사용하여 활동 및 개인화 경험을 만들고 활성화하고 제공할 수 있습니다.

## Adobe Target 활성화

활성화하려면 [!DNL Target]다음을 수행해야 합니다.

1. UI에서 activity.id 및 experience.id 응답 토큰을 [!DNL Target] 설정합니다.

![target_reponse_token](./assets/target_response_token.png)

1. 적절한 클라이언트 코드를 사용하여 [Edge 구성에서](../../fundamentals/edge-configuration.md) target을 활성화합니다.
1. 이벤트에 `renderDecisions` 옵션을 추가합니다.

그런 다음 다음을 수행할 수도 있습니다.

* 이벤트 `decisionScopes` 에 추가하여 특정 활동을 검색합니다(양식 기반 컴포저를 사용하여 만든 활동에 유용함).
* 코드 [조각을](../manage-flicker.md) 추가하여 페이지의 특정 부분만 숨깁니다.

## Adobe Target VEC 사용

SDK에서는 VEC를 일반적으로 다음 한 가지 예외를 사용할 수 있습니다.대상 VEC [도우미 익스텐션을](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 설치하고 활성화해야 합니다.

## VEC 활동 자동 렌더링

AEP 웹 SDK는 사용자를 위해 웹상에서 Adobe Target의 VEC를 통해 정의된 경험을 자동으로 렌더링할 수 있는 강력한 기능을 제공합니다. AEP 웹 SDK에서 VEC 활동을 자동 렌더링하도록 나타내려면 다음을 사용하여 이벤트를 전송합니다. `renderDecisions = true`

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

## 양식 기반 컴포저 사용

양식 기반 경험 작성기는 JSON, HTML, 이미지 등과 같은 다양한 응답 유형을 갖는 A/B 테스트, [!DNL Experience Targeting]Automated Personalization 및 Recommendations 활동을 구성하는 데 유용한 비시각적 인터페이스입니다. Adobe Target이 반환하는 응답 유형 또는 결정에 따라 핵심 비즈니스 로직을 실행할 수 있습니다. 양식 기반 컴포저 활동에 대한 결정을 검색하려면 결정을 검색할 모든 &#39;decisionScopes&#39;가 있는 이벤트를 보냅니다.

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

`decisionScopes` 개인화된 경험을 렌더링할 페이지의 섹션, 위치 또는 일부를 정의합니다. 사용자 정의 `decisionScopes` 가능하고 사용자가 정의할 수 있습니다. 현재 [!DNL Target] 고객의 경우 `decisionScopes` &quot;mbox&quot;라고도 합니다. UI에서 [!DNL Target] &quot;위치&quot; `decisionScopes` 로 나타납니다.

## The `__view__` Scope

AEP는 AEP에 의존하지 않고 VEC 작업을 검색할 수 있는 기능 [!DNL Web SDK] [!DNL Web SDK] 을 제공합니다. &quot;a&quot;로 `__view__` 정의된 이벤트를 전송합니다 `decisionScopes`.

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## XDM 고객

AEP 웹 SDK를 통해 전달할 Target 활동에 대해 대상을 정의할 때 [XDM을](https://docs.adobe.com/content/help/ko-KR/experience-platform/xdm/home.html) 정의하고 사용해야 합니다. XDM 스키마, 클래스 및 믹스를 정의한 후 타깃팅을 위해 XDM 데이터로 정의된 Target 대상 규칙을 만들 수 있습니다. Target 내에서 XDM 데이터는 Audience Builder에 사용자 지정 매개 변수로 표시됩니다. XDM은 점 표기법(예: )을 사용하여 `web.webPageDetails.name`정리됩니다.

사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 사전 정의된 대상이 있는 Target 활동이 있는 경우 AEP 웹 SDK를 통해 올바로 전달되지 않습니다. 사용자 지정 매개 변수 또는 사용자 프로필을 사용하는 대신 XDM을 사용해야 합니다. 그러나 XDM이 필요하지 않은 AEP 웹 SDK를 통해 지원되는 기본 대상 타깃팅 필드가 있습니다. XDM이 필요하지 않은 Target UI에서 사용할 수 있는 필드는 다음과 같습니다.

* 타겟 라이브러리
* 지역
* 네트워크
* 운영 체제
* 사이트 페이지
* 브라우저
* 트래픽 소스
* 시간대

## 용어

__결정:__ 에서 [!DNL Target]이러한 상호 작용은 활동에서 선택한 경험과 관련이 있습니다.

__스키마:__ 의사 결정 스키마는 오퍼의 유형입니다 [!DNL Target].

__범위:__ 결정의 범위. 여기서 [!DNL Target]는 mBox입니다. 글로벌 mBox는 `__view__` 범위입니다.

__XDM:__ XDM은 점 표기법으로 직렬화된 다음 mBox 매개 변수 [!DNL Target] 로 입력됩니다.
