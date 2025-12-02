---
title: 푸시 알림 설정
description: 웹 SDK 태그 확장에 대한 푸시 알림 설정을 구성합니다.
source-git-commit: 0b3f4ec51cac182b637c79b9fcb883e5f8f78d02
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# 푸시 알림 설정

>[!AVAILABILITY]
>
>웹 SDK에 대한 푸시 알림이 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

이 구성 섹션에서는 푸시 알림 인증을 위한 VAPID 공개 키를 설정할 수 있습니다.

>[!NOTE]
>
>이 기능은 먼저 [사용자 지정 빌드 구성 요소](custom-build-components.md)를 사용하여 활성화해야 합니다. 기본적으로 비활성화되어 있습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 클릭합니다.
1. **[!UICONTROL Custom build components]**&#x200B;을(를) 확장한 다음 **[!UICONTROL Push notifications]**&#x200B;을(를) 활성화합니다.
1. [!UICONTROL SDK instances]에서 아래로 스크롤하여 [!UICONTROL Push Notifications] 섹션을 찾습니다.
1. **[!UICONTROL VAPID Public Key]** 필드에 VAPID 공개 키를 입력합니다.

![웹 SDK 태그 확장을 사용하여 푸시 알림 설정을 표시하는 이미지](../assets/push-notifications.png)

다음 필드를 사용할 수 있습니다.

## [!UICONTROL VAPID public key]

푸시 구독에 사용되는 VAPID 공개 키입니다. Base64로 인코딩된 문자열입니다.

## [!UICONTROL Application ID]

VAPID 공개 키와 연결된 애플리케이션 ID.

## [!UICONTROL Tracking dataset ID]

푸시 알림 추적 및 분석을 위한 데이터 세트 ID.

## JavaScript 라이브러리를 사용한 푸시 알림

이 섹션은 JavaScript 라이브러리를 구성할 때 [`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md)에 해당하는 태그입니다. 연결된 페이지는 사전 요구 사항 및 VAPID 공개 키 생성에 대한 정보도 제공합니다.
