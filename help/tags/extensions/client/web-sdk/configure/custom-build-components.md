---
title: 사용자 지정 빌드 구성 요소
description: 빌드 크기를 줄이는 기능을 사용하지 않도록 설정하는 사용자 지정 웹 SDK 빌드를 만듭니다.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# 사용자 지정 빌드 구성 요소

웹 SDK 라이브러리에는 개인화, ID, 링크 추적 등과 같은 다양한 기능에 대한 여러 모듈이 포함되어 있습니다. 사용 사례에 따라 전체 라이브러리가 아닌 특정 기능만 필요할 수 있습니다. 빌드 구성 요소를 비활성화하면 필요한 모듈만 사용할 수 있으므로 라이브러리 크기를 줄이고 성능을 향상시킬 수 있습니다.

구성 요소를 비활성화하면 해당 구성 요소의 설정을 더 이상 편집할 수 없습니다. 여러 웹 SDK 인스턴스를 사용하는 경우 선택한 빌드 구성 요소가 모든 인스턴스에 적용됩니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. 맨 위에 있는 **[!UICONTROL Custom build components]** 아코디언을 확장합니다.

>[!WARNING]
>
>이러한 설정을 잘못 수정하면 데이터 손실을 포함하여 원하지 않는 결과가 발생할 수 있습니다. 이러한 변경 사항을 프로덕션에 게시하기 전에 개발 환경에서 구현을 철저히 테스트하십시오.

Adobe은 다음 웹 SDK 빌드 구성 요소를 비활성화하는 기능을 제공합니다.

| 구성 요소 빌드 | 설명 | 종속 피쳐 |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | 자동 링크 컬렉션 및 Activity Map 추적을 허용합니다. | |
| **[!UICONTROL Advertising]** | Customer Journey Analytics과 Adobe Advertising 통합을 활성화합니다. | |
| **[!UICONTROL Audiences]** | ID 동기화와 같이 Adobe Audience Manager과의 통합을 지원합니다. | |
| **[!UICONTROL Consent]** | 동의 기능을 사용할 수 있습니다. | [[!UICONTROL Set consent]](../actions/set-consent.md) 액션 |
| **[!UICONTROL Event merge]** | 사용하지 않음. | [[!UICONTROL Event merge ID]](../data-element-types.md) 데이터 요소(더 이상 사용되지 않음)<br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md) 작업(더 이상 사용되지 않음) |
| **[!UICONTROL Media Analytics bridge]** | 는 기존 Media Analytics와의 통합을 지원합니다. | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md) 액션 |
| **[!UICONTROL Personalization]** | Adobe Target 및 Adobe Journey Optimizer과의 통합을 지원합니다. | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md) 액션 |
| **[!UICONTROL Push notifications]** | Adobe Journey Optimizer에 대한 웹 푸시 알림을 활성화합니다. | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md) 액션 |
| **[!UICONTROL Rules engine]** | Adobe Journey Optimizer을 사용하여 디바이스 의사 결정을 활성화합니다. | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md) 작업<br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items) 이벤트 |
| **[!UICONTROL Streaming media]** | 스트리밍 미디어 컬렉션과의 통합을 지원합니다. | [[!UICONTROL Send media event]](../actions/send-media-event.md) 액션 |
