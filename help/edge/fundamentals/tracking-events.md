---
title: Adobe Experience Platform Web SDK를 사용하여 이벤트 추적
description: Adobe Experience Platform Web SDK 이벤트를 추적하는 방법에 대해 알아봅니다.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;비콘 보내기;documentUnloading;문서 언로드;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: a6948e3744aa754eda22831a7e68b847eb904e76
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 1%

---

# 이벤트 추적

이벤트 데이터를 Adobe Experience Cloud으로 보내려면 `sendEvent` 명령입니다. 다음 `sendEvent` 명령은 데이터를 로 보내는 기본 방법입니다. [!DNL Experience Cloud]및 을 사용하여 개인화된 콘텐츠, ID 및 대상자 대상을 검색할 수 있습니다.

Adobe Experience Cloud으로 전송된 데이터는 다음 두 가지 범주로 분류됩니다.

* XDM 데이터
* 비 XDM 데이터

## XDM 데이터 보내기

XDM 데이터는 컨텐츠 및 구조가 Adobe Experience Platform 내에서 만든 스키마와 일치하는 개체입니다. [스키마를 만드는 방법에 대해 자세히 알아보세요.](../../xdm/tutorials/create-schema-ui.md)

분석, 개인화, 대상자 또는 대상에 포함하려는 모든 XDM 데이터는 `xdm` 옵션을 선택합니다.


```javascript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

다음 시간 사이에 시간이 경과할 수 있습니다. `sendEvent` 명령이 실행되고 데이터가 서버로 전송될 때(예: 웹 SDK 라이브러리가 완전히 로드되지 않았거나 동의를 아직 받지 않은 경우). 의 일부를 수정하려면 `xdm` 를 실행한 후 개체 `sendEvent` 명령, 다음을 복제하는 것이 좋습니다. `xdm` 오브젝트 _다음 이전_ 실행 `sendEvent` 명령입니다. 예:

```javascript
var clone = function(value) {
  return JSON.parse(JSON.stringify(value));
};

var dataLayer = {
  "commerce": {
    "order": {
      "purchaseID": "a8g784hjq1mnp3",
      "purchaseOrderNumber": "VAU3123",
      "currencyCode": "USD",
      "priceTotal": 999.98
    }
  }
};

alloy("sendEvent", {
  "xdm": clone(dataLayer)
});

// This change will not be reflected in the data sent to the 
// server for the prior sendEvent command.
dataLayer.commerce = null;
```

이 예에서 데이터 계층은 JSON으로 직렬화한 다음 역직렬화하여 복제됩니다. 그런 다음 복제된 결과가 `sendEvent` 명령입니다. 이렇게 하면 `sendEvent` 명령에는 데이터 레이어의 스냅샷이 `sendEvent` 원본 데이터 레이어 개체에 대한 나중에 수정한 내용이 서버로 전송된 데이터에 반영되지 않도록 명령이 실행되었습니다. 이벤트 기반 데이터 계층을 사용하는 경우 데이터 복제가 이미 자동으로 처리되었을 수 있습니다. 예를 들어 [Adobe 클라이언트 데이터 레이어](https://github.com/adobe/adobe-client-data-layer/wiki), `getState()` 메서드는 모든 이전 변경 내용에 대한 계산된 클론된 스냅샷을 제공합니다. 또한 Adobe Experience Platform Web SDK 태그 확장을 사용하는 경우 이 작업이 자동으로 처리됩니다.

>[!NOTE]
>
>XDM 필드의 각 이벤트에서 전송할 수 있는 데이터에는 32KB 제한이 있습니다.


## XDM이 아닌 데이터 보내기

XDM 스키마와 일치하지 않는 데이터는 `data` 옵션 `sendEvent` 명령입니다. 이 기능은 Web SDK 버전 2.5.0 이상에서 지원됩니다.

이 기능은 Adobe Target 프로필을 업데이트하거나 Target Recommendations 속성을 보내야 하는 경우에 유용합니다. [이러한 Target 기능에 대해 자세히 알아보십시오.](../personalization/adobe-target/target-overview.md#single-profile-update)

나중에 전체 데이터 레이어를 `data` 옵션을 선택하고 XDM 서버측에 매핑합니다.

**Adobe Target에 프로필 및 Recommendations 속성을 보내는 방법:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```


### 설정 `eventType` {#event-types}

XDM ExperienceEvent 스키마에는 선택 사항이 있습니다. `eventType` 필드. 레코드에 대한 기본 이벤트 유형이 보관됩니다. 이벤트 유형을 설정하면 전송할 여러 이벤트를 구분하는 데 도움이 됩니다. XDM은 사용할 수 있거나 사용 사례에 맞게 항상 사용자 지정 이벤트 유형을 만들 수 있는 사전 정의된 이벤트 유형을 제공합니다. 자세한 내용은 XDM 설명서 를 참조하십시오. [사전 정의된 모든 이벤트 유형 목록](../../xdm/classes/experienceevent.md#eventType).

태그 확장을 사용하거나 태그 없이 언제든지 전달할 수 있는 경우 이러한 이벤트 유형이 드롭다운에 표시됩니다. 이러한 매개 변수는 의 일부로 전달될 수 있습니다. `xdm` 옵션을 선택합니다.


```javascript
alloy("sendEvent", {
  "xdm": {
    "eventType": "commerce.purchases",
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

또는 `eventType` 를 사용하여 이벤트 명령에 전달할 수 있습니다. `type` 옵션을 선택합니다. 이 기능은 XDM 데이터에 추가됩니다. 사용 `type` as a 옵션을 사용하면 를 보다 쉽게 설정할 수 있습니다 `eventType` XDM 페이로드를 수정할 필요가 없습니다.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 데이터 세트 ID 재정의

>[!IMPORTANT]
>
>다음 `datasetId` 옵션이에서 지원됨 `sendEvent` 명령이 더 이상 사용되지 않습니다. 데이터 세트 ID를 재정의하려면 [구성 재정의](../datastreams/overrides.md) 대신,

일부 사용 사례에서는 이벤트를 구성 UI에 구성된 데이터 세트가 아닌 데이터 세트로 보낼 수 있습니다. 이를 위해 다음을 설정해야 합니다. `datasetId` 옵션 `sendEvent` 명령:



```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### ID 정보 추가

사용자 지정 ID 정보를 이벤트에 추가할 수도 있습니다. 다음을 참조하십시오 [Experience Cloud ID 검색 중](../identity/overview.md).

## sendBeacon API 사용

웹 페이지 사용자가 탐색하기 직전에 이벤트 데이터를 보내는 것은 어려울 수 있습니다. 요청이 너무 오래 걸리면 브라우저가 요청을 취소할 수 있습니다. 일부 브라우저는 이라는 웹 표준 API를 구현했습니다. `sendBeacon` 이 시간 동안 데이터를 보다 쉽게 수집할 수 있도록 하기 위해 사용 시 `sendBeacon`을 사용하면 브라우저가 전역 검색 컨텍스트에서 웹 요청을 수행합니다. 즉, 브라우저가 백그라운드에서 비콘 요청을 수행하고 페이지 탐색을 유지하지 않습니다. Adobe Experience Platform에 알리기 [!DNL Web SDK] 사용 `sendBeacon`, 옵션을 추가합니다. `"documentUnloading": true` 이벤트 명령.  다음은 한 예입니다.


```javascript
alloy("sendEvent", {
  "documentUnloading": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

브라우저에는 로 전송할 수 있는 데이터 양에 대한 제한이 적용되었습니다. `sendBeacon` 한 번에. 많은 브라우저에서 제한은 64K입니다. 페이로드가 너무 크기 때문에 브라우저가 이벤트를 거부하는 경우 Adobe Experience Platform [!DNL Web SDK] 는 일반적인 전송 방법(예: fetch)을 사용하는 것으로 돌아갑니다.

## 이벤트에서 응답 처리

이벤트의 응답을 처리하려는 경우 다음과 같이 성공 또는 실패에 대한 알림을 받을 수 있습니다.


```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


### 다음 `result` 오브젝트

다음 `sendEvent` 명령은 로 해결된 약속을 반환합니다. `result` 개체. 다음 `result` 개체에는 다음 속성이 포함되어 있습니다.

**제안**: 방문자가 자격을 얻은 개인화 오퍼입니다. [제안에 대해 자세히 알아보세요.](../personalization/rendering-personalization-content.md#manually-rendering-content)

**결정**: 이 속성은 더 이상 사용되지 않습니다. 대신 `propositions`를 사용하십시오.

**대상**: 외부 개인화 플랫폼, 컨텐츠 관리 시스템, 광고 서버 및 고객 웹 사이트에서 실행되는 기타 애플리케이션과 공유할 수 있는 Adobe Experience Platform의 세그먼트입니다. [대상에 대해 자세히 알아보세요.](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en)

>[!WARNING]
>
>`destinations` 는 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

## 전체적으로 이벤트 수정 {#modifying-events-globally}

이벤트에서 필드를 전체적으로 추가, 제거 또는 수정하려면 `onBeforeEventSend` callback.  이 콜백은 이벤트가 전송될 때마다 호출됩니다.  이 콜백은 이벤트 개체에서 `xdm` 필드.  수정 `content.xdm` 를 클릭하여 이벤트와 함께 전송되는 데이터를 변경합니다.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(content) {
    // Change existing values
    content.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete content.xdm.web.webReferrer.URL;
    // Or add new values
    content.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` 필드는 다음 순서로 설정됩니다.

1. 이벤트 명령에 옵션으로 전달된 값 `alloy("sendEvent", { xdm: ... });`
2. 자동으로 수집된 값.  (참조: [자동 정보](../data-collection/automatic-information.md).)
3. 에서 수행한 변경 사항 `onBeforeEventSend` callback.

에 대한 몇 가지 참고 사항 `onBeforeEventSend` callback:

* 콜백 중에 이벤트 XDM을 수정할 수 있습니다. 콜백이 반환되면 content.xdm 및 content.data 개체의 수정된 필드 및 값이 이벤트와 함께 전송됩니다.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 콜백에서 예외가 발생하면 이벤트 처리가 중지되고 이벤트가 전송되지 않습니다.
* 콜백이 부울 값 을 반환하는 경우 `false`, 이벤트 처리는 오류 없이 중단되며 이벤트는 전송되지 않습니다. 이 메커니즘을 사용하면 이벤트 데이터를 검사하고 를 반환하여 특정 이벤트를 쉽게 무시할 수 있습니다 `false` 이벤트를 보내지 말아야 하는 경우.

   >[!NOTE]
   >페이지의 첫 번째 이벤트에서 false를 반환하지 않도록 주의해야 합니다. 첫 번째 이벤트에서 false를 반환하면 개인화에 부정적인 영향을 줄 수 있습니다.

```javascript
   onBeforeEventSend: function(content) {
     // ignores events from bots
     if (MyBotDetector.isABot()) {
       return false;
     }
   }
```

부울 이외의 모든 반환 값 `false` 은 이벤트를 처리하고 콜백 후 을(를) 보낼 수 있도록 합니다.

* 이벤트 유형을 검사하여 이벤트를 필터링할 수 있습니다(참조 [이벤트 유형](#event-types).)

```javascript
    onBeforeEventSend: function(content) {  
      // augments XDM if link click event is to a partner website
      if (
        content.xdm.eventType === "web.webinteraction.linkClicks" &&
        content.xdm.web.webInteraction.URL ===
          "http://example.com/partner-page.html"
      ) {
        content.xdm.partnerWebsiteClick = true;
      }
   }
```

## 실행 가능한 잠재적 오류

이벤트를 전송할 때 전송되는 데이터가 너무 큰 경우(전체 요청의 경우 32KB 이상) 오류가 발생할 수 있습니다. 이 경우 전송되는 데이터의 양을 줄여야 합니다.
