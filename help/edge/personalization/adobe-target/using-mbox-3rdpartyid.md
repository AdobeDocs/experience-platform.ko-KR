---
title: mbox3rdPartyId에 대한 실시간 프로필 동기화
description: Adobe Experience Platform Web SDK에서 mbox3rdPartyID를 사용하는 방법에 대해 알아봅니다.
keywords: 개인화;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 30%

---

# `mbox3rdPartyId`이란 

Adobe Target의 mbox3rdPartyID는 회사의 충성도 프로그램을 위한 멤버십 ID와 같은 회사의 방문자 ID입니다.

방문자가 회사 사이트에 로그인하면 일반적으로 회사는 방문자 계정, 포인트 카드, 멤버십 번호 또는 해당 회사에 대한 기타 적용 가능한 식별자에 연결되는 ID를 만듭니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## 사용 방법 `mbox3rdPartyId` Web SDK를 사용하여

### 1단계: 구성 `Target Third Party ID Namespace`

구성 `Target Third Party ID Namespace` (으)로 [데이터스트림](../../../datastreams/overview.md)를 mbox 타사 ID로 사용할 ID 네임스페이스를 사용합니다.
[ID 네임스페이스에 대해 자세히 알아보기](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko)

![](assets/mbox3rdpartyid.png)

### 2단계: 보내기 `mbox3rdpartyId` 대상 Target

보내기 `mbox3rdpartyId` 에서 Target `sendEvent` 명령, 1단계에서 구성한 ID 네임스페이스 사용.
[ID 전송에 대해 자세히 알아보기](../../identity/overview.md#syncing-identities)

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
