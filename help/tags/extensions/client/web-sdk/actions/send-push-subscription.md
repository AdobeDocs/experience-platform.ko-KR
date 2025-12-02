---
title: 푸시 구독 전송
description: 브라우저 푸시 가입에 대한 데이터를 등록, 전송 및 수집합니다.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# 푸시 구독 전송

>[!AVAILABILITY]
>
>웹 SDK에 대한 푸시 알림이 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

**[!UICONTROL Send push subscription]** 작업은 Adobe Experience Platform에 푸시 알림 구독을 등록합니다. 브라우저에서 푸시 구독 세부 정보 검색을 처리하고 구성된 데이터 스트림으로 전송합니다. 웹 SDK 확장 버전 2.32.0 이상에서 사용할 수 있습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL Actions]에서 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL Extension] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL Action Type]을(를) **[!UICONTROL Send push subscription]**(으)로 설정합니다.

이 작업에는 SDK 인스턴스를 선택하는 것 이상의 구성 설정이 없습니다.

이 명령을 사용하기 전에 확장을 구성할 때 유효한 [VAPID 공개 키](../configure/push-notifications.md)를 설정해야 합니다.

이 작업은 [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md) 명령에 해당하는 태그 확장입니다. 사전 요구 사항, 권장 실행 빈도, 명령 작동 방식 및 오류 처리에 대한 자세한 내용은 링크된 페이지를 참조하십시오.

>[!MORELIKETHIS]
>
>* [푸시 알림 구성](../configure/push-notifications.md)
>* [웹 푸시 API 사양](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [서비스 작업자 API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
