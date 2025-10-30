---
title: 푸시 알림
description: 웹 SDK에 대한 푸시 알림을 구성하여 브라우저 기반 푸시 메시지를 활성화합니다.
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> 웹 SDK에 대한 푸시 알림이 현재 **베타**&#x200B;에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

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

공개 및 개인 키 쌍을 생성합니다. 웹 SDK 구성에서 공개 키를 사용하고 Adobe Journey Optimizer 푸시 알림 채널 내에 개인 키를 저장합니다.

## 서비스 작업자 JavaScript 설치

서비스 작업자 코드는 웹 사이트와 동일한 도메인에서 제공되어야 합니다. Adobe의 CDN에서 서비스 작업자 코드를 다운로드한 다음 자체 서버에서 JavaScript 파일을 호스팅합니다. 웹 SDK 서비스 작업자 코드는 다음 URL 구조를 사용하여 사용할 수 있습니다.

- **축소됨**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **전체**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

다음은 서비스 작업자를 설치하는 방법의 예입니다.

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## 웹 SDK 태그 확장을 사용하여 푸시 알림 구성 {#configure-push-notifications-tag-extension}

푸시 알림을 활성화하고 구성하려면 다음 단계를 따르십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 클릭합니다.
1. **[!UICONTROL Custom build components]** 섹션에서 **[!UICONTROL Push notifications]**&#x200B;을(를) 사용하도록 설정합니다.
1. 아래로 스크롤하여 [!UICONTROL Push Notifications] 섹션을 찾습니다.
1. **[!UICONTROL VAPID Public Key]** 필드에 VAPID 공개 키를 입력합니다.
1. **[!UICONTROL Application ID]** 필드에 응용 프로그램 ID를 입력합니다.
1. **[!UICONTROL Tracking Dataset ID]** 필드에 추적 데이터 세트 ID를 입력합니다.
1. **[!UICONTROL Save]**&#x200B;을(를) 클릭한 다음 변경 내용을 게시합니다.

>[!NOTE]
>
> 푸시 알림은 태그 확장 구성에서 명시적으로 활성화되어야 합니다. 이 기능은 기본적으로 비활성화되어 있습니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 푸시 알림 구성 {#configure-push-notifications-javascript}

`pushNotifications` 명령을 실행할 때 `configure` 개체 설정:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey:
      "BEl62iUYgUivElbkzaBgNL3r3vOAhvJyFXjS6FjjRRojYD4NElJkLBJKZvS3xAAh4_gE3WnMaZNu_KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## 속성 {#properties}

| 속성 | 유형 | 필수 여부 | 설명 |
|---------|----|---------|-----------|
| `vapidPublicKey` | 문자열 | 예 | 푸시 구독에 사용되는 VAPID 공개 키입니다. Base64로 인코딩된 문자열이어야 합니다. |
| `applicationId` | 문자열 | 예 | 해당 VAPID 공개 키와 연결된 애플리케이션 ID. |
| `trackingDatasetId` | 문자열 | 예 | 푸시 알림 추적에 사용되는 시스템 데이터 세트 ID. |

## 중요한 고려 사항 {#important-considerations}

- **보안**: 푸시 구독은 구독 중에 사용되는 특정 VAPID 공개 키에 연결되어 있습니다. VAPID 키를 변경하면 기존 구독이 자동으로 구독 취소되고 새 키로 다시 생성됩니다.
- **캐싱**: 웹 SDK은 현재 ECID 및 구독 세부 정보를 캐시된 값과 비교하여 구독 업데이트를 자동으로 관리합니다. 변경 사항이 감지된 경우에만 구독 데이터가 전송됩니다.
- **서비스 작업자 요구 사항**: 푸시 알림에는 등록된 서비스 작업자가 필요합니다. 푸시 이벤트를 처리하도록 서비스 작업자가 올바르게 구성되었는지 확인합니다.

## 다음 단계 {#next-steps}

푸시 알림을 구성한 후 [sendPushSubscription](../sendpushsubscription.md) 명령을 사용하여 Adobe Experience Platform에 푸시 구독을 등록합니다.
