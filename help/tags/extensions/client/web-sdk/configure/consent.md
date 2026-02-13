---
title: 동의 구성 설정
description: 태그 확장에 대한 기본 동의 및 개인 정보 설정을 구성합니다.
exl-id: 93913a8b-0351-409d-b26a-8dc2ac0296c5
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 동의 구성 설정 {#consent}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_consent"
>title="동의"
>abstract="다른 명시적 동의 환경 설정이 제공되지 않을 경우 가정하는 기본 동의 수준을 선택합니다."

**[!UICONTROL Consent]** 섹션에서 다른 명시적 동의 환경 설정이 제공되지 않을 경우 가정하는 기본 동의 수준을 선택할 수 있습니다. 기본 동의 수준이 사용자 프로필에 저장되지 않습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. **[!UICONTROL Consent]** 섹션까지 아래로 스크롤합니다.

![태그 UI에서 웹 SDK 태그 확장의 개인 정보 설정을 보여 주는 이미지](../assets/web-sdk-ext-privacy.png)

이 섹션에는 기본 동의 수준을 결정하는 단일 라디오 버튼 세트가 포함되어 있습니다.

* **[!UICONTROL In]**: 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 수집합니다.
* **[!UICONTROL Out]**: 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 삭제합니다.
* **[!UICONTROL Pending]**: 사용자가 동의 환경 설정을 제공하기 전에 발생하는 이벤트를 큐에 추가합니다. 동의하면 큐에 있는 이벤트가 Adobe으로 전송됩니다. 동의가 거부되면 대기 중인 이벤트가 무시됩니다.
* **[!UICONTROL Provide a data element]**: 위의 구성 설정 중 하나를 결정하는 데이터 요소를 선택합니다. 유효한 값에는 문자열 `"in"`, `"out"` 또는 `"pending"`이(가) 포함됩니다.

조직에서 데이터를 수집하기 위해 명시적인 사용자 동의가 필요한 경우 Adobe에서는 기본 동의를 **[!UICONTROL Out]** 또는 **[!UICONTROL Pending]**(으)로 설정하는 것이 좋습니다.
