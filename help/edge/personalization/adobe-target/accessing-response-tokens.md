---
title: Adobe Experience Platform Web SDK를 사용하여 응답 토큰에 액세스
description: Adobe Experience Platform Web SDK를 사용하여 응답 토큰에 액세스하는 방법을 알아봅니다.
keywords: 개인화;target;adobe target;renderDecisions;sendEvent;decisions;result.decisions,응답 토큰;
source-git-commit: 4bddd9f23ae885468148d1592af219290d6fafd9
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 응답 토큰 액세스

Adobe Target에서 반환된 개인화 컨텐츠에는 활동, 오퍼, 경험, 사용자 프로필, 지역 정보 등에 대한 세부 사항인 [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)이 포함됩니다. 이러한 세부 사항은 타사 도구와 공유하거나 디버깅에 사용할 수 있습니다. Adobe Target 사용자 인터페이스에서 응답 토큰을 구성할 수 있습니다.

개인화 콘텐츠에 액세스하려면 이벤트를 전송할 때 콜백 함수를 제공합니다. 이 콜백은 SDK가 서버에서 성공적인 응답을 받은 후에 호출됩니다. 콜백에는 반환된 개인화 컨텐츠가 포함된 `propositions` 속성이 포함될 수 있는 `result` 개체가 제공됩니다. 다음은 콜백 함수를 제공하는 예입니다.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

이 예에서 `result.propositions`이 존재하면 은 이벤트와 관련된 개인화 proposition이 포함된 배열입니다. `result.propositions`의 콘텐츠에 대한 자세한 내용은 [개인화 콘텐츠 렌더링](../rendering-personalization-content.md)을 참조하십시오.

웹 SDK에서 자동으로 렌더링한 모든 프로필에서 모든 활동 이름을 수집하고 단일 배열로 푸시하려고 한다고 가정합니다. 그런 다음 단일 스토리지를 타사 시스템으로 보낼 수 있습니다. 이 경우:

1. `result` 개체에서 proposition을 추출합니다.
1. 각각의 제안을 반복하세요.
1. SDK가 제안을 렌더링했는지 확인합니다.
1. 만약 그렇다면, 제안에 있는 각 항목들을 반복합니다.
1. 응답 토큰이 포함된 객체인 `meta` 속성에서 활동 이름을 검색합니다.
1. 활동 이름을 배열에 푸시합니다.
1. 활동 이름을 타사에 보냅니다.

코드는 다음과 같습니다.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```


