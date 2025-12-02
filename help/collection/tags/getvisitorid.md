---
title: getVisitorId
description: Experience Cloud 방문자 ID 서비스 태그 확장 인스턴스를 검색합니다.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# `getVisitorId()`

`_satellite.getVisitorId()` 메서드가 태그 속성 내에서 [Adobe Experience Cloud ID 서비스](https://experienceleague.adobe.com/en/docs/id-service/using/home)의 인스턴스를 반환합니다. **있는 경우** ID 서비스 확장이 설치 및 게시되었습니다. 이 방법은 사용자 지정 코드 블록에서 사용하거나, 고급 데이터 요소 구성 또는 방문자 ID 문제 해결을 위해 방문자 ID 인스턴스에 직접 액세스하려는 경우에 유용합니다.

>[!IMPORTANT]
>
>이 메서드는 독립 실행형 Experience Cloud ID 서비스 태그 확장을 포함하는 속성에만 적용됩니다. 웹 SDK 태그 확장에서 사용할 수 있는 암시적 ID 서비스 기능에는 적용되지 않습니다. 웹 SDK의 암시적 ID 서비스 기능을 사용하여 방문자 ID를 얻으려면 [`getIdentity`](/help/collection/js/commands/getidentity.md) 명령을 참조하십시오.

ID 서비스 확장이 설치 및 게시된 상태에서 이 메서드를 호출하면 [`Visitor.getInstance()`](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/getinstance) 메서드를 호출한 후 얻은 개체와 유사한 개체가 반환됩니다. ID 서비스 확장이 설치되지 않았거나 게시되지 않은 경우 이 메서드를 호출하면 `null`이(가) 반환됩니다.

```ts
_satellite.getVisitorId(): Visitor | null
```

## 사용 가능한 필드 및 메서드

사용 가능한 필드 및 메서드를 보려면 Experience Cloud 방문자 ID 서비스 설명서의 Experience Cloud ID 서비스 [메서드](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/get-set)를 참조하십시오.

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
