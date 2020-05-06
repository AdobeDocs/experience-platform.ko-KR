---
title: Experience Cloud ID 검색 중
seo-title: Adobe Experience Platform 웹 SDK Experience Cloud ID 검색
description: Adobe Experience Cloud ID를 가져오는 방법을 알아봅니다.
seo-description: Adobe Experience Cloud ID를 가져오는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# (베타) Experience Cloud ID 검색

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Cloud는 모든 소비자에게 고유한 ID를 사용합니다. 이 고유 ID를 사용하려면 `getIdentity` 명령을 사용하십시오. `getIdentity` 현재 방문자에 대한 기존 ECID를 반환합니다. 아직 ECID가 없는 처음 방문자의 경우 이 명령은 새 ECID를 생성합니다.

>[!NOTE]
>
>이 메서드는 일반적으로 Experience Cloud ID를 읽어야 하는 사용자 지정 솔루션에서 사용됩니다. 표준 구현에서는 사용되지 않습니다.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
