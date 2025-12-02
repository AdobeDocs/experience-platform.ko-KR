---
title: 푸시 알림
description: 웹 SDK에 대한 푸시 알림을 구성하여 브라우저 기반 푸시 메시지를 활성화합니다.
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>웹 SDK에 대한 푸시 알림이 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

`pushNotifications` 속성을 사용하면 웹 응용 프로그램에 대한 푸시 알림을 구성할 수 있습니다. 이 기능을 사용하면 웹 사이트가 현재 브라우저에 로드되지 않은 경우에도 웹 앱이 서버에서 푸시된 메시지를 받을 수 있습니다.

## 전제 조건 {#prerequisites}

푸시 알림을 구성하기 전에 다음을 확인하십시오.

1. **사용자 권한**: 사용자는 알림에 대한 권한을 명시적으로 부여해야 합니다.
2. **서비스 작업자**: 푸시 알림이 작동하려면 등록된 서비스 작업자가 필요합니다
3. **VAPID 키**: 보안 통신을 위한 VAPID(Democratic Application Server Identification) 키 생성
4. **응용 프로그램 ID**: Adobe Journey Optimizer -> 채널 -> 푸시 설정 -> 푸시 자격 증명 내에 VAPID 키를 저장할 때 사용되는 앱 ID입니다.
5. **추적 데이터 세트 ID**: 이름이 &quot;AJO 푸시 추적 경험 이벤트 데이터 세트&quot;인 시스템 데이터 세트의 ID입니다. Adobe Journey Optimizer -> 데이터 세트에서 다운로드

## VAPID 키 생성 {#generate-vapid-keys}

VAPID 키를 생성하려면 `web-push` NPM 패키지를 설치하고 다음을 실행하십시오.

```bash
npm install web-push -g
web-push generate-vapid-keys
```

이 작업은 공개 및 개인 키 쌍을 생성합니다. 웹 SDK 구성에서 공개 키를 사용하고 Adobe Journey Optimizer 푸시 알림 채널 내에 개인 키를 저장합니다.

## 서비스 작업자 설치

서비스 작업자 코드는 웹 사이트와 동일한 도메인에서 제공되어야 합니다. Adobe의 CDN에서 서비스 작업자 코드를 다운로드하고 자체 서버에서 JavaScript 파일을 호스팅합니다. 웹 SDK 서비스 작업자 코드는 다음 URL 구조를 사용하여 사용할 수 있습니다.

- **축소됨**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **전체**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

다음은 서비스 작업자를 설치하는 방법의 예입니다.

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## 구현

`pushNotifications` 명령을 실행할 때 `configure` 개체 설정:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## 속성 {#properties}

| 속성 | 유형 | 필수 여부 | 설명 |
|---|---|---|---|
| **`vapidPublicKey`** | 문자열 | 예 | 푸시 구독에 사용되는 VAPID 공개 키입니다. Base64로 인코딩된 문자열이어야 합니다. |
| **`applicationId`** | 문자열 | 예 | VAPID 공개 키와 연결된 애플리케이션 ID. |
| **`trackingDatasetId`** | 문자열 | 예 | 푸시 알림 추적에 사용되는 시스템 데이터 세트 ID. |

## 중요한 고려 사항 {#important-considerations}

- **보안**: 푸시 구독은 구독 중에 사용되는 특정 VAPID 공개 키에 연결되어 있습니다. VAPID 키를 변경하면 기존 구독이 자동으로 구독 취소되고 새 키로 다시 생성됩니다.
- **캐싱**: 웹 SDK은 현재 ECID 및 구독 세부 정보를 캐시된 값과 비교하여 구독 업데이트를 자동으로 관리합니다. 변경 사항이 감지된 경우에만 구독 데이터가 전송됩니다.
- **서비스 작업자 요구 사항**: 푸시 알림에는 등록된 서비스 작업자가 필요합니다. 푸시 이벤트를 처리하도록 서비스 작업자가 올바르게 구성되었는지 확인합니다.

## 웹 SDK 태그 확장을 사용하여 푸시 알림 구성 {#configure-push-notifications-tag-extension}

이 속성에 해당하는 웹 SDK 태그 확장은 확장을 구성할 때 [[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md) 섹션입니다.

## 다음 단계 {#next-steps}

푸시 알림을 구성한 후 [sendPushSubscription](../sendpushsubscription.md) 명령을 사용하여 Adobe Experience Platform에 푸시 구독을 등록합니다.
