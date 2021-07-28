---
title: Adobe Experience Platform Web SDK를 사용하여 이벤트 추적
description: Adobe Experience Platform Web SDK 이벤트를 추적하는 방법을 알아봅니다.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;documentUnloading;document Unloading;onBeforeEventSend;
exl-id: 8b221cae-3490-44cb-af06-85be4f8d280a
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# 이벤트 추적

이벤트 데이터를 Adobe Experience Cloud에 보내려면 `sendEvent` 명령을 사용합니다. `sendEvent` 명령은 [!DNL Experience Cloud]에 데이터를 보내고, 개인화된 콘텐츠, ID 및 대상자 대상을 검색하는 기본 방법입니다.

Adobe Experience Cloud에 전송된 데이터는 두 가지 카테고리로 분류됩니다.

* XDM 데이터
* 비XDM 데이터

## XDM 데이터 보내기

XDM 데이터는 컨텐츠 및 구조가 Adobe Experience Platform 내에서 만든 스키마와 일치하는 객체입니다. [스키마를 만드는 방법에 대해 자세히 알아보십시오 .](../../xdm/tutorials/create-schema-ui.md)

분석, 개인화, 대상 또는 대상에 포함하려는 모든 XDM 데이터는 `xdm` 옵션을 사용하여 전송해야 합니다.


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

`sendEvent` 명령이 실행될 때와 데이터가 서버에 전송될 때(예: 웹 SDK 라이브러리가 완전히 로드되지 않았거나 동의를 아직 받지 않은 경우) 사이에 시간이 경과할 수 있습니다. `sendEvent` 명령을 실행한 후 `xdm` 개체의 일부를 수정하려면 `sendEvent` 명령을 실행하기 전에 `xdm` 개체 _를 복제하는 것이 좋습니다._ 예:

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

이 예에서 데이터 계층은 JSON으로 직렬화한 다음 역직렬화하여 복제됩니다. 그런 다음 복제된 결과가 `sendEvent` 명령에 전달됩니다. 이렇게 하면 `sendEvent` 명령에 `sendEvent` 명령이 실행될 때 데이터 계층의 스냅샷이 있으므로 나중에 원래 데이터 계층 객체에 대한 수정 사항이 서버로 전송된 데이터에 반영되지 않습니다. 이벤트 기반 데이터 레이어를 사용하는 경우 데이터 복제가 이미 자동으로 처리될 수 있습니다. 예를 들어 [클라이언트 데이터 레이어 Adobe](https://github.com/adobe/adobe-client-data-layer/wiki)를 사용하는 경우 `getState()` 메서드는 모든 이전 변경 사항에 대한 계산된 복제된 스냅샷을 제공합니다. Adobe Experience Platform 웹 SDK 태그 확장을 사용하는 경우에도 자동으로 처리됩니다.

>[!NOTE]
>
>XDM 필드의 각 이벤트에서 전송할 수 있는 데이터에는 32KB 제한이 있습니다.


## 비 XDM 데이터 보내기

XDM 스키마와 일치하지 않는 데이터는 `sendEvent` 명령의 `data` 옵션을 사용하여 전송해야 합니다. 이 기능은 Web SDK 버전 2.5.0 이상에서 지원됩니다.

이 기능은 Adobe Target 프로필을 업데이트하거나 Target Recommendations 특성을 보내야 하는 경우에 유용합니다. [이러한 Target 기능에 대해 자세히 알아보십시오.](../personalization/adobe-target/target-overview.md#single-profile-update)

향후에는 `data` 옵션 아래에서 전체 데이터 계층을 전송하고 XDM 서버측에 매핑할 수 있습니다.

**Adobe Target에 프로필 및 Recommendations 속성을 보내는 방법:**

```javascript
alloy("sendEvent", {
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30,
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```


### 설정 `eventType` {#event-types}

XDM 경험 이벤트에는 선택적 `eventType` 필드가 있습니다. 여기에는 레코드에 대한 기본 이벤트 유형이 포함됩니다. 이벤트 유형을 설정하면 전송할 다른 이벤트를 구별할 수 있습니다. XDM은 사용할 수 있거나 사용 사례에 대해 자신만의 사용자 지정 이벤트 유형을 만들 수 있는 사전 정의된 이벤트 유형을 제공합니다. 다음은 XDM에서 제공하는 모든 사전 정의된 이벤트 유형 목록입니다. [XDM 공개 보고서에서 자세히 알아보십시오](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values).


| **이벤트 유형:** | **정의:** |
| ---------------------------------- | ------------ |
| advertising.completes | 시간 미디어 자산을 끝까지 감시했는지 여부를 나타냅니다. 시청자가 반드시 전체 비디오를 시청했음을 의미하지는 않습니다. 뷰어가 건너뛸 수 있음 |
| advertising.timePlayed | 특정 시간 미디어 자산에서 사용자가 사용한 시간을 설명합니다 |
| advertising.federated | 데이터 페더레이션(고객 간의 데이터 공유)를 통해 경험 이벤트가 생성되었는지 여부를 나타냅니다 |
| advertising.clicks | 광고에서 작업을 클릭합니다 |
| advertising.conversions | 성능 평가를 위한 이벤트를 트리거하는 고객 사전 정의된 작업 |
| advertising.firstQuartiles | 디지털 비디오 광고는 그 지속 시간의 25%를 보통 속도로 재생했다 |
| advertising.impressions | 최종 사용자에게 표시될 가능성이 있는 광고의 노출 횟수 |
| advertising.midpoints | 디지털 비디오 광고는 그 지속 시간의 50%를 보통 속도로 재생했다 |
| advertising.starts | 디지털 비디오 광고가 재생을 시작했습니다 |
| advertising.thirdQuartiles | 디지털 비디오 광고는 전체 재생 시간의 75%를 일반 속도로 재생했습니다 |
| web.webpagedetails.pageViews | 웹 페이지 보기가 발생했습니다. |
| web.webinteraction.linkClicks | 웹 링크를 클릭했습니다 |
| commerce.checkouts | 제품 목록의 체크아웃 프로세스 중에 체크아웃 프로세스에 여러 단계가 있는 경우 두 개 이상의 체크아웃 이벤트가 있을 수 있습니다. 여러 단계가 있는 경우 이벤트 시간 정보 및 참조된 페이지 또는 경험을 사용하여 개별 이벤트가 순서대로 나타내는 단계를 식별합니다 |
| commerce.productListAdds | 제품 목록에 제품 추가. 장바구니에 추가된 제품 예 |
| commerce.productListOpens | 새 제품 목록의 초기화. 장바구니가 만들어지는 예 |
| commerce.productListRemovals | 제품 목록에서 제품 항목을 제거합니다. 장바구니에서 제품이 제거된 예 |
| commerce.productListReopens | 사용자가 더 이상 액세스할 수 없는(포기) 제품 목록을 다시 활성화했습니다. 리마케팅 활동을 통한 예 |
| commerce.productListViews | 제품 목록 보기가 발생했습니다. |
| commerce.productViews | 제품 보기가 발생했습니다. |
| commerce.purchases | 주문이 수락되었습니다. 구매는 상거래 전환에서 유일한 필수 작업입니다. Purchase에는 참조된 제품 목록이 있어야 합니다 |
| commerce.saveForLaters | 제품 목록은 나중에 사용할 수 있도록 저장됩니다. 제품 위시 목록 예 |
| delivery.feedback | 게재에 대한 피드백 이벤트. 이메일 게재에 대한 피드백 이벤트 예 |


이러한 이벤트 유형은 태그 확장을 사용하는 경우 드롭다운에 표시되거나 태그 없이 항상 전달할 수 있습니다. `xdm` 옵션의 일부로 전달될 수 있습니다.


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

또는 `type` 옵션을 사용하여 `eventType`을 이벤트 명령에 전달할 수 있습니다. 백그라운드에서 XDM 데이터에 추가됩니다. `type` 을 옵션으로 사용하면 XDM 페이로드를 수정하지 않고 `eventType` 을(를) 보다 쉽게 설정할 수 있습니다.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 데이터 세트 ID 재정의

일부 사용 사례에서는 구성 UI에 구성된 이벤트 이외의 데이터 세트에 이벤트를 보낼 수 있습니다. 이를 위해 `sendEvent` 명령에서 `datasetId` 옵션을 설정해야 합니다.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### ID 정보 추가

사용자 지정 ID 정보를 이벤트에 추가할 수도 있습니다. [Experience Cloud ID 검색](../identity/overview.md)을 참조하십시오.

## sendBeacon API 사용

웹 페이지 사용자가 이동하기 전에 이벤트 데이터를 보내는 것은 까다로울 수 있습니다. 요청이 너무 오래 걸리는 경우 브라우저가 요청을 취소할 수 있습니다. 일부 브라우저는 이 시간 동안 데이터를 보다 쉽게 수집할 수 있도록 `sendBeacon`이라는 웹 표준 API를 구현했습니다. `sendBeacon`을 사용하는 경우 브라우저가 전역 탐색 컨텍스트에서 웹 요청을 수행합니다. 즉, 브라우저가 배경에서 비콘 요청을 수행하고 페이지 탐색을 유지하지 않습니다. Adobe Experience Platform [!DNL Web SDK]에 `sendBeacon`을 사용하도록 하려면 `"documentUnloading": true` 옵션을 이벤트 명령에 추가합니다.  다음은 한 예입니다.


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

브라우저에는 `sendBeacon`으로 한 번에 전송할 수 있는 데이터 양에 제한을 두었습니다. 많은 브라우저에서 제한은 64K입니다. 페이로드가 너무 커서 브라우저가 이벤트를 거부하는 경우 Adobe Experience Platform [!DNL Web SDK]은(는) 일반적인 전송 방법을 사용하여 다시 폴백됩니다(예: 가져오기).

## 이벤트의 응답 처리

이벤트의 응답을 처리하려면 다음과 같이 성공 또는 실패에 대한 알림을 받을 수 있습니다.


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
}).then(function(results) {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## 이벤트 전역 수정 {#modifying-events-globally}

이벤트에서 전체적으로 필드를 추가, 제거 또는 수정하려면 `onBeforeEventSend` 콜백을 구성할 수 있습니다.  이 콜백은 이벤트가 전송될 때마다 호출됩니다.  이 콜백은 `xdm` 필드를 사용하여 이벤트 개체에 전달됩니다.  이벤트를 사용하여 전송되는 데이터를 변경하려면 `content.xdm` 을 수정합니다.


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

1. 이벤트 명령 `alloy("sendEvent", { xdm: ... });`에 옵션으로 전달된 값
2. 자동으로 수집된 값.  ([자동 정보](../data-collection/automatic-information.md) 참조)
3. `onBeforeEventSend` 콜백에서 변경된 사항입니다.

`onBeforeEventSend` 콜백에 대한 몇 가지 참고 사항:

* 이벤트 XDM은 콜백 중에 수정할 수 있습니다. 콜백이 반환되면 다음과 같은 수정된 필드와 값이
content.xdm 및 content.data 개체는 이벤트와 함께 전송됩니다.

   ```javascript
   onBeforeEventSend: function(content){
     //sets a query parameter in XDM
     const queryString = window.location.search;
     const urlParams = new URLSearchParams(queryString);
     content.xdm.marketing.trackingCode = urlParams.get('cid')
   }
   ```

* 콜백에서 예외가 발생하면, 이벤트에 대한 처리가 중단되고 이벤트가 전송되지 않습니다.
* 콜백이 `false` 부울 값을 반환하는 경우 이벤트 처리가 중단됩니다.
오류가 없으면 이벤트가 전송되지 않습니다. 이 메커니즘을 사용하면 특정 이벤트를
이벤트를 전송하지 않아야 하는 경우 이벤트 데이터를 검사하고 `false` 를 반환합니다.

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

부울 `false` 이외의 모든 반환 값에서는 콜백 후에 이벤트가 처리되고 전송될 수 있습니다.

* 이벤트 유형을 검사하여 이벤트를 필터링할 수 있습니다( [이벤트 유형](#event-types) 참조).

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

## 잠재적 실행 가능한 오류

이벤트를 전송할 데이터가 너무 큰 경우(전체 요청의 경우 32KB 이상) 오류가 발생할 수 있습니다. 이 경우 전송되는 데이터 양을 줄여야 합니다.
