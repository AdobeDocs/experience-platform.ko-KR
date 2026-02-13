---
title: Brand Concierge 구성 설정
description: Brand Concierge 채팅에 대한 세션 지속성 및 스트림 시간 제한을 구성합니다.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# Brand Concierge 구성 설정 {#brand-concierge}

>[!AVAILABILITY]
>
>웹 SDK용 Brand Concierge은 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="속성에서 Brand Concierge을 사용할 때의 구성 설정입니다."

**[!UICONTROL Brand Concierge]** 섹션을 통해 웹 SDK 태그 확장에서 Brand Concierge 채팅 세션이 작동하는 방식을 제어할 수 있습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Brand Concierge]** 섹션까지 아래로 스크롤합니다.

다음 옵션을 사용할 수 있습니다.

## [!UICONTROL Sticky conversation session]

페이지 로드 동안 Brand Concierge 세션을 지속하는 확인란은 세션 쿠키를 사용합니다. 이 옵션은 기본적으로 비활성화되어 있습니다. 이 값을 설정하는 방법에 대한 지침은 JavaScript 라이브러리 설명서에서 [`conversation`](/help/collection/js/commands/configure/conversation.md)을(를) 참조하십시오.

## [!UICONTROL Stream timeout (seconds)]

시간 초과 오류를 트리거하기 전에 대화 스트림 청크를 기다리는 최대 시간(초)입니다. 기본값은 `10`초입니다.
