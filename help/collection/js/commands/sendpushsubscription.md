---
title: sendPushSubscription
description: Adobe Experience Platform으로 푸시 알림 구독을 등록합니다.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
>웹 SDK에 대한 푸시 알림이 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

`sendPushSubscription` 명령은 Adobe Experience Platform에 푸시 알림 구독을 등록합니다. 이 명령은 브라우저에서 푸시 구독 세부 정보 검색을 처리하고 구성된 데이터 스트림으로 보냅니다. 웹 SDK 버전 2.29.0 이상에서 사용할 수 있습니다.

## 전제 조건 {#prerequisites}

`sendPushSubscription`을(를) 사용하기 전에 다음을 확인하십시오.

1. **구성된 푸시 알림**: VAPID 공개 키로 [`pushNotifications`](configure/pushnotifications.md) 구성 속성을 설정합니다.
2. **사용자 권한**: 사용자는 알림 권한(`Notification.permission === "granted"`)을 부여해야 합니다.
3. **서비스 작업자**: 등록된 서비스 작업자를 사이트에서 사용할 수 있어야 합니다.
4. **푸시 관리자 지원**: 브라우저가 푸시 알림을 지원하고 PushManager API를 사용할 수 있어야 합니다.

웹 SDK의 구성된 인스턴스를 호출할 때 `sendPushSubscription` 명령을 실행합니다. [`configure`](configure/overview.md) 명령을 호출하기 전에 푸시 알림이 구성된 `sendPushSubscription` 명령을 호출해야 합니다.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## 권장 실행 빈도 {#recommended-execution-frequency}

최적의 푸시 알림 기능을 위해 Adobe에서는 `sendPushSubscription` 명령을 **하루에 한 번**&#x200B;실행하는 것이 좋습니다. 이 빈도를 통해 다음을 확인할 수 있습니다.

* 구독 세부 정보가 Adobe Experience Platform에 최신 상태로 유지됨
* 푸시 토큰 또는 구독 상태에 대한 모든 변경 사항이 캡처됩니다
* 사용자의 프로필은 최신 푸시 알림 환경 설정으로 업데이트된 상태를 유지합니다

아래 접근 방식과 유사한 접근 방식을 사용하여 이를 구현할 수 있습니다.

```js
// Check if subscription data was sent today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## 작동 방식 {#how-it-works}

`sendPushSubscription` 명령은 다음 작업을 수행합니다.

1. **필수 구성 요소의 유효성을 검사합니다**: 푸시 알림이 구성되어 있고 사용자 권한이 부여되었는지 확인합니다
2. **ID 대기**: 사용자의 ECID를 사용할 수 있을 때까지 대기합니다.
3. **구독을 검색합니다**: 구성된 VAPID 키를 사용하여 서비스 작업자의 활성 푸시 구독을 가져옵니다.
4. **변경 내용 확인**: 현재 구독 세부 정보를 캐시된 값(ECID + 구독 세부 정보)과 비교합니다. 구독 세부 사항이 변경되지 않은 경우 명령은 정보 메시지를 기록하고 네트워크 요청을 하지 않고 를 반환합니다
5. **데이터 스트림으로 전송**: 변경 내용이 검색되면 구성된 Adobe Experience Platform 데이터 스트림으로 구독 데이터를 전송합니다
6. **업데이트 캐시**: 나중에 비교할 수 있도록 새 구독 세부 정보를 저장합니다.

## 오류 처리 {#error-handling}

일반적인 오류 조건 및 해당 메시지:

| 오류 | 원인 |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | 푸시 알림 구성이 누락되었거나 잘못되었습니다. |
| `"Service workers are not supported in this browser."` | 브라우저가 서비스 작업자를 지원하지 않습니다. |
| `"Push notifications are not supported in this browser."` | 브라우저가 푸시 알림 또는 알림 API를 지원하지 않습니다. |
| `"The user has not given permission to send push notifications."` | 사용자가 알림 권한(`Notification.permission === "granted"`)을 부여하지 않았습니다. |
| `"No service worker registration was found."` | 현재 출처에 등록된 서비스 작업자가 없습니다. |
| `"No VAPID public key was provided."` | 구성에서 VAPID 공개 키가 누락되었습니다. |

## 데이터 페이로드 {#data-payload}

이 명령은 다음 형식으로 푸시 알림 데이터를 보냅니다.

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## 웹 SDK 태그 확장을 사용하여 푸시 구독 등록 {#register-push-subscription-tag-extension}

이 필드에 해당하는 웹 SDK 태그 확장에서는 태그 규칙 내에서 [[!UICONTROL Send Push Subscription]](/help/tags/extensions/client/web-sdk/actions/send-push-subscription.md) 작업을 사용합니다.

>[!MORELIKETHIS]
>
>* [푸시 알림 구성](configure/pushnotifications.md)
>* [웹 푸시 API 사양](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [서비스 작업자 API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
