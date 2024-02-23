---
title: Web SDK에서 웹 인앱 메시지 지원 구성
description: 웹 인앱 메시지를 지원하도록 웹 SDK 태그 확장을 구성하는 방법을 알아봅니다.
source-git-commit: a020f880be2606024c6a986dc468d70a2fbdc30f
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Web SDK에서 웹 인앱 메시지 지원 구성


인앱 메시지는 웹 애플리케이션 내의 사용자에게 보내 특정 관심 영역으로 안내하는 알림입니다.

새 기능 홍보, 특별 오퍼 제공 또는 사용자 온보딩 지원 등 다양한 목적으로 이러한 알림을 사용할 수 있습니다.

인앱 메시지를 사용하면 대상자와 효과적으로 소통하고 대상자의 메시지를 애플리케이션의 중요한 측면으로 유도할 수 있습니다.

>[!IMPORTANT]
>
>웹 인앱 메시징은 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) Web SDK를 사용하여 개인화된 콘텐츠를 제공하는 기능입니다.
>
>웹 인앱 메시지 캠페인을 구성하는 방법에 대한 자세한 지침은 [Adobe Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html).


## 전제 조건 {#prerequisites}

### Web SDK 태그 확장 버전 {#extension-version}

웹 인앱 메시지 기능을 사용하려면 최신 버전의 웹 SDK 태그 확장이 필요합니다.

### 웹 인앱 메시지에 대한 CSP 구성 {#csp}

를 구성할 때 [웹 인앱 메시지](../personalization/web-in-app-messaging.md), CSP에 다음 지시문을 포함해야 합니다.

```
default-src  blob:;
```

CSP 구성에 대한 자세한 내용은 [전용 설명서](../fundamentals/configuring-a-csp.md).

## Web SDK 태그 확장을 사용하여 웹 인앱 메시지 구성 {#tag-extension}

다음을 참조하십시오. [웹 SDK 태그 확장 구성 페이지](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) 아래에 설명된 설정을 찾을 수 있는 위치를 이해합니다.

다음 작업을 수행한 후 [설치됨](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) 웹 SDK 태그 확장 기능을 사용하려면 아래 단계에 따라 웹 인앱 메시지에 대한 확장 기능을 구성하십시오.

다음에서 **[!UICONTROL 개인화]** 섹션, 다음을 확인: **[!UICONTROL 개인화 스토리지 활성화]** 옵션을 선택합니다. 이 옵션을 사용하면 웹 SDK에서 페이지 로드 중에 사용자가 본 경험을 추적할 수 있습니다.

![태그 확장 구성 페이지의 개인화 스토리지 옵션을 보여 주는 이미지입니다.](assets/web-in-app-messaging/enable-personalization-storage.png)


웹 인앱 메시지는 두 가지 유형의 트리거를 지원합니다.

* [플랫폼으로 데이터 보내기](#send-data-platform)
* [메시지 수동 트리거](#manual-trigger)

사용할 트리거에 따라 웹 SDK 태그 확장을 구성하려면 다음 섹션을 참조하십시오.

### 구성 단계 **[!UICONTROL 플랫폼으로 데이터 보내기]** 트리거 {#send-data-platform}

웹 SDK 확장이 포함된 태그 속성을 선택합니다. [새 규칙 만들기](../../tags/ui/managing-resources/rules.md##create-a-rule) 다음 설정으로:

1. **[!UICONTROL 확장]**: [!UICONTROL 코어]
2. **[!UICONTROL 이벤트 유형]**: [!UICONTROL 라이브러리가 로드됨 (페이지 상단)]

   ![이벤트 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/rule-configuration.png)

3. 선택 **[!UICONTROL 변경 내용 유지]** 이벤트 구성을 저장합니다.

그런 다음 만든 규칙에 작업을 추가해야 합니다.

1. 다음에서 [!DNL Actions] 섹션, 선택 **[!UICONTROL 추가]**.
   ![규칙 편집 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/add-action.png)

2. 다음 사용 **[!UICONTROL 작업]** 설정:
   * **[!UICONTROL 확장]**: [!UICONTROL Adobe Experience Platform 웹 SDK]
   * **[!UICONTROL 작업 유형]**: [!UICONTROL 이벤트 보내기]

     ![작업 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/action-configuration.png)

3. 화면 오른쪽의 **[!UICONTROL 개인화]** 섹션, 활성화 **[!UICONTROL 시각적 개인화 결정 렌더링]** 옵션을 선택합니다.
   ![개인화 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/render-visual-personalization.png)

4. 화면 오른쪽의 **[!UICONTROL 의사 결정 컨텍스트]** 섹션에서 다음을 정의합니다. **[!UICONTROL 키]**/**[!UICONTROL 값]** campaign 구성에서 인앱 메시지에 사용할 수 있도록 사용한 쌍입니다.
   ![개인화 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/decision-context.png)

5. 선택 **[!UICONTROL 변경 내용 유지]** 구성을 저장합니다.


그런 다음 새로 만든 규칙을 태그 속성 라이브러리에 추가해야 합니다. 이렇게 하려면 다음으로 이동합니다. **[!UICONTROL 게시 플로우]** 을 클릭하고 이전에 만든 규칙을 선택합니다.

![라이브러리 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/add-rule-to-library.png)

라이브러리에 규칙을 추가한 후 을 선택합니다. **[!UICONTROL 개발에 저장 및 구축]**.

![개인화 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/publish-flow.png)

이제 구성 프로세스가 완료되었으며 메시지를 사용자에게 표시할 준비가 되었습니다.

### 수동 트리거 사용을 위한 구성 단계 {#manual-trigger}

웹 SDK 확장이 포함된 태그 속성을 선택합니다. [새 규칙 만들기](../../tags/ui/managing-resources/rules.md##create-a-rule) 다음 설정으로:

1. **[!UICONTROL 확장]**: [!UICONTROL 코어]
2. **[!UICONTROL 이벤트 유형]**: [!UICONTROL 클릭]
3. 선택한 CSS 선택기에 의한 식별자인 페이지의 특정 요소에 대한 트리거를 설정합니다.

   ![이벤트 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/event-configuration-manual.png)


그런 다음 만든 규칙에 작업을 추가해야 합니다.

1. 다음에서 [!DNL Actions] 섹션, 선택 **[!UICONTROL 추가]**.
   ![규칙 편집 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/add-action.png)

2. 다음 사용 **[!UICONTROL 작업]** 설정:
   * **[!UICONTROL 확장]**: [!UICONTROL Adobe Experience Platform 웹 SDK]
   * **[!UICONTROL 작업 유형]**: [!UICONTROL 규칙 세트 평가]

     ![작업 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/manual-trigger-action.png)

3. 화면 오른쪽에서 **[!UICONTROL 시각적 개인화 결정 렌더링]** 옵션을 선택합니다.
   ![개인화 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/manual-trigger-render.png)


4. 화면 오른쪽의 **[!UICONTROL 의사 결정 컨텍스트]** 섹션에서 다음을 정의합니다. **[!UICONTROL 키]**/**[!UICONTROL 값]** campaign 구성에서 인앱 메시지에 사용할 수 있도록 사용한 쌍입니다.
   ![개인화 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. 선택 **[!UICONTROL 변경 내용 유지]** 구성을 저장합니다.

그런 다음 새로 만든 규칙을 태그 속성 라이브러리에 추가해야 합니다. 이렇게 하려면 다음으로 이동합니다. **[!UICONTROL 게시 플로우]** 을 클릭하고 이전에 만든 규칙을 선택합니다.

![라이브러리 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/add-rule-to-library.png)

라이브러리에 규칙을 추가한 후 을 선택합니다. **[!UICONTROL 개발에 저장 및 구축]**.

![개인화 구성 화면을 보여 주는 이미지입니다.](assets/web-in-app-messaging/publish-flow.png)

이제 구성 프로세스가 완료되었으며 메시지를 사용자에게 표시할 준비가 되었습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 웹 인앱 메시지 구성 {#js-library}

Web SDK 태그 확장을 사용하는 대신 Web SDK JavaScript 라이브러리에서 직접 웹 인앱 메시지를 구성할 수도 있습니다.



Adobe Journey Optimizer에서 보내는 웹 인앱 메시지를 두 가지 방법으로 표시할 수 있습니다.

### 방법 1: 개인화 콘텐츠를 자동으로 가져오기 {#automatic}

Web SDK가 페이지 로드 시 개인화 콘텐츠를 자동으로 가져오도록 하려면 다음을 사용하십시오. `sendEvent` 아래 예와 같은 명령입니다.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### 방법 2: 사용자 작업에 따라 개인화 콘텐츠를 수동으로 가져오기 {#manual}

사용자가 특정 작업을 수행한 후에만 개인화 콘텐츠를 표시하려면 `evaluateRulesets` 아래 예와 같은 명령입니다.

이 예제에서 개인화 콘텐츠는 사용자가 **[!UICONTROL 지금 구입]** 단추를 클릭합니다.

```js
 alloy("evaluateRulesets", {
     renderDecisions: true,
     personalization: {
         decisionContext: {
             "userAction": "buy_now"
         }
     }
 });
```

### 개인화 스토리지 구성 {#personalization-storage}

를 통해 설정된 횟수 동안 또는 사용자가 페이지를 방문할 때마다 사용자에게 인앱 메시지를 표시하도록 선택할 수 있습니다. `personalizationStorageEnabled` 구성 옵션을 사용할 수 있습니다.

다음에서 [웹 SDK 구성](../fundamentals/configuring-the-sdk.md) 설정 `personalizationStorageEnabled` 필요에 따른 옵션:

* `personalizationStorageEnabled: true` 에서 정의한 빈도로 인앱 메시지를 트리거합니다. [Adobe Journey Optimizer campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html#configure-inapp).
* `personalizationStorageEnabled: false` 는 모든 페이지 로드 시 인앱 메시지를 트리거합니다.