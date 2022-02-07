---
title: mbox3rdPartyId에 대한 실시간 프로필 동기화
description: Adobe Experience Platform Web SDK에서 mbox3rdPartyID를 사용하는 방법을 알아봅니다.
keywords: 개인화;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
source-git-commit: 86acedc6813a14648848a25e08aa7e65f48d1a2a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 9%

---


# `mbox3rdPartyId`이란 

Adobe Target의 mbox3rdPartyID는 회사의 충성도 프로그램을 위한 멤버십 ID와 같은 회사의 방문자 ID입니다.

방문자가 회사 사이트에 로그인하면 일반적으로 회사는 방문자 계정, 로열티 카드, 멤버십 번호 또는 해당 회사에 대한 기타 적용 가능한 식별자에 연결되는 ID를 만듭니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## 사용 방법 `mbox3rdPartyId` 웹 SDK 사용

### 1단계: 구성 `Target Third Party ID Namespace`

구성 `Target Third Party ID Namespace` 다음 위치에서 [데이터 스트림](../../fundamentals/datastreams.md)를 사용( mbox 타사 ID로 사용할 ID 네임스페이스 사용)
[ID 네임스페이스에 대해 자세히 알아보기](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko-KR)

![](assets/mbox3rdpartyid.png)

### 2단계: 보내기 `mbox3rdpartyId` Target

보내기 `mbox3rdpartyId` Target `sendEvent` 명령(1단계에서 구성한 ID 네임스페이스 사용)
[ID 보내기에 대한 자세한 정보](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```


