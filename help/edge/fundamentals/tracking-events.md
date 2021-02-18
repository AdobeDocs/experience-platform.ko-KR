---
title: Adobe Experience Platform 웹 SDK를 사용하여 이벤트 추적
seo-description: Adobe Experience Platform 웹 SDK 이벤트를 추적하는 방법을 알아봅니다.
keywords: sendEvent;xdm;eventType;datasetId;sendBeacon;send Beacon;send Beacon;documentUnaring;document Unloading;onBeforeEventSend;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---


# 이벤트 추적

이벤트 데이터를 Adobe Experience Cloud으로 보내려면 `sendEvent` 명령을 사용합니다. `sendEvent` 명령은 데이터를 [!DNL Experience Cloud]에 보내고 개인화된 컨텐츠, ID 및 대상 대상을 검색하는 기본 방법입니다.

Adobe Experience Cloud으로 전송된 데이터는 두 가지 카테고리로 분류됩니다.

* XDM 데이터
* XDM 데이터가 아닌 데이터(현재 지원되지 않음)

## XDM 데이터 전송

XDM 데이터는 내용 및 구조가 Adobe Experience Platform 내에서 만든 스키마와 일치하는 개체입니다. [스키마를 만드는 방법에 대해 자세히 알아보십시오.](../../xdm/tutorials/create-schema-ui.md)

분석, 개인화, 고객 또는 대상의 일부로 사용하려는 모든 XDM 데이터는 `xdm` 옵션을 사용하여 전송해야 합니다.


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

`sendEvent` 명령이 실행될 때와 데이터가 서버로 전송될 때까지 다소 시간이 걸릴 수 있습니다(예: 웹 SDK 라이브러리가 완전히 로드되지 않았거나 동의를 아직 받지 못한 경우). `sendEvent` 명령을 실행한 후 `xdm` 객체의 일부를 수정하려면 `sendEvent` 명령을 실행하기 전에 `xdm` 개체 _을 복제하는 것이 좋습니다._ 예:

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

이 예에서 데이터 레이어는 JSON으로 직렬화한 다음 역직렬화하여 복제됩니다. 다음으로 복제된 결과가 `sendEvent` 명령에 전달됩니다. 이렇게 하면 `sendEvent` 명령이 실행될 때 데이터 레이어의 스냅샷이 존재하므로 나중에 원본 데이터 레이어 개체에 대한 수정 내용이 서버에 전송된 데이터에 반영되지 않습니다. `sendEvent` 이벤트 기반 데이터 레이어를 사용하는 경우 데이터 복제가 이미 자동으로 처리됩니다. 예를 들어 [Adobe 클라이언트 데이터 레이어](https://github.com/adobe/adobe-client-data-layer/wiki)를 사용하는 경우 `getState()` 메서드는 모든 이전 변경 사항에 대한 계산된 복제된 스냅샷을 제공합니다. AEP 웹 SDK 시작 확장 프로그램을 사용하는 경우에도 자동으로 처리됩니다.

>[!NOTE]
>
>XDM 필드의 각 이벤트에서 전송할 수 있는 데이터에는 32KB 제한이 있습니다.

### 비 XDM 데이터 전송

현재 XDM 스키마와 일치하지 않는 데이터 전송이 지원되지 않습니다. 지원은 향후 날짜에 예정되어 있습니다.

### 설정 `eventType`

XDM 경험 이벤트에는 선택적 `eventType` 필드가 있습니다. 레코드에 대한 기본 이벤트 유형을 보유합니다. 이벤트 유형을 설정하면 전송할 다른 이벤트를 구분할 수 있습니다. XDM은 사용할 수 있는 사전 정의된 이벤트 유형을 몇 가지 제공하며 사용자가 사용 사례에 대해 사용자 지정 이벤트 유형을 항상 생성합니다. 다음은 XDM에서 제공하는 사전 정의된 이벤트 유형의 목록입니다. [XDM 공개 보고서에서 자세히 알아보십시오](https://github.com/adobe/xdm/blob/master/docs/reference/behaviors/time-series.schema.md#xdmeventtype-known-values).


| **이벤트 유형:** | **정의:** |
| ---------------------------------- | ------------ |
| advertising.completes | 시간 지정 미디어 에셋이 완료되는 것을 보았는지 여부를 나타냅니다. 이것이 뷰어가 전체 비디오를 시청했다는 의미는 아닙니다.미리 보기를 건너뛸 수 있음 |
| advertising.timePlayed | 특정 시간 제한 미디어 자산에 대해 사용자가 보낸 시간을 설명합니다. |
| advertising.federated | 데이터 통합을 통해 경험 이벤트가 만들어졌는지 여부를 나타냅니다(고객 간 데이터 공유). |
| advertising.clicks | 광고에서 클릭 작업 |
| advertising.conversions | 성능 평가를 위한 이벤트를 트리거하는 고객 사전 정의된 작업 |
| advertising.firstQuartiles | 디지털 비디오 광고는 전체 재생 시간의 25%를 정상적인 속도로 재생했습니다 |
| advertising.impressions | 최종 사용자에게 표시될 가능성이 있는 광고의 노출 수 |
| advertising.midpoints | 디지털 비디오 광고는 전체 재생 시간의 50%를 정상적인 속도로 재생했습니다. |
| advertising.starts | 디지털 비디오 광고 재생을 시작했습니다. |
| advertising.thirdQuartiles | 디지털 비디오 광고는 재생 시간의 75%를 정상적인 속도로 재생했습니다. |
| web.webpagedetails.pageViews | 웹 페이지 보기가 발생했습니다. |
| web.webinteraction.linkClicks | 웹 링크를 클릭했습니다. |
| commerce.checkouts | 제품 목록의 체크아웃 프로세스 중에 체크아웃 프로세스에 여러 단계가 있을 경우 체크아웃 이벤트를 두 개 이상 생성할 수 있습니다. 여러 단계가 있을 경우 이벤트 시간 정보 및 참조된 페이지 또는 경험을 사용하여 개별 이벤트가 순서대로 나타내는 단계를 식별합니다 |
| commerce.productListAdds | 제품 목록에 제품 추가 장바구니에 추가된 제품 예 |
| commerce.productListOpens | 새 제품 목록 초기화 장바구니가 만들어진 예 |
| commerce.productListRemovals | 제품 목록에서 제품 항목을 제거합니다. 장바구니에서 제품이 제거된 예 |
| commerce.productListReopens | 사용자가 더 이상 액세스할 수 없게(포기)된 제품 목록을 다시 활성화했습니다. 재마케팅 활동을 통한 예 |
| commerce.productListViews | 제품 목록 보기가 발생했습니다. |
| commerce.productViews | 제품 보기가 발생했습니다. |
| commerce.purchases | 주문이 수락되었습니다. 구매(Purchase)는 상거래 전환에서 유일하게 필요한 작업입니다. 구매에는 참조된 제품 목록이 있어야 합니다. |
| commerce.saveForLaters | 제품 목록은 나중에 사용할 수 있도록 저장됩니다. 제품 위시리스트 예 |
| delivery.feedback | 전달에 대한 피드백 이벤트입니다. 이메일 전달에 대한 피드백 이벤트 예 |


이러한 이벤트 유형은 Adobe Experience Platform Launch 확장을 사용하거나 Experience Platform Launch 없이 언제든지 전달할 수 있는 경우 드롭다운에 표시됩니다. 이 매개 변수는 `xdm` 옵션의 일부로 전달할 수 있습니다.


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

또는 `eventType`은 `type` 옵션을 사용하여 이벤트 명령에 전달할 수 있습니다. 백그라운드에서 XDM 데이터에 추가됩니다. `type`을 옵션으로 사용하면 XDM 페이로드를 수정하지 않고도 `eventType`을(를) 보다 쉽게 설정할 수 있습니다.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 데이터 세트 ID 재정의

경우에 따라 구성 UI에 구성된 이벤트 이외의 데이터세트에 이벤트를 보낼 수도 있습니다. 이를 위해서는 `sendEvent` 명령에 `datasetId` 옵션을 설정해야 합니다.


```javascript
var myXDMData = { ... };

alloy("sendEvent", {
  "xdm": myXDMData,
  "type": "commerce.checkout",
  "datasetId": "YOUR_DATASET_ID"
});
```

### ID 정보 추가

사용자 지정 ID 정보를 이벤트에 추가할 수도 있습니다. [Experience Cloud ID 검색](../identity/overview.md)을(를) 참조하십시오.

## sendBeacon API 사용

웹 페이지 사용자가 다른 곳으로 이동하기 전에 이벤트 데이터를 보내는 것은 까다로울 수 있습니다. 요청이 너무 오래 걸리면 브라우저가 요청을 취소할 수 있습니다. 일부 브라우저는 이 시간 동안 데이터를 보다 쉽게 수집할 수 있도록 `sendBeacon`이라는 웹 표준 API를 구현했습니다. `sendBeacon`을(를) 사용할 때 브라우저는 전역 탐색 컨텍스트에서 웹 요청을 수행합니다. 즉, 브라우저는 백그라운드에서 비콘 요청을 수행하고 페이지 탐색을 유지하지 않습니다. Adobe Experience Platform [!DNL Web SDK]에 `sendBeacon`을(를) 사용하도록 하려면 `"documentUnloading": true` 옵션을 이벤트 명령에 추가합니다.  다음은 한 예입니다.


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

브라우저는 `sendBeacon`으로 한 번에 전송할 수 있는 데이터 양에 제한을 두었습니다. 많은 브라우저에서 제한은 64K입니다. 페이로드가 너무 커서 브라우저가 이벤트를 거부하는 경우 Adobe Experience Platform [!DNL Web SDK]은(는) 일반적인 전송 방식(예: 가져오기)을 다시 사용합니다.

## 이벤트의 응답 처리

이벤트에서 응답을 처리하려면 다음과 같이 성공 또는 실패에 대한 알림을 받을 수 있습니다.


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

## 전역적으로 이벤트 수정 {#modifying-events-globally}

이벤트에서 전체적으로 필드를 추가, 제거 또는 수정하려면 `onBeforeEventSend` 콜백을 구성할 수 있습니다.  이 콜백은 이벤트를 보낼 때마다 호출됩니다.  이 콜백은 `xdm` 필드가 있는 이벤트 객체에 전달됩니다.  이벤트에서 전송된 데이터를 변경하려면 `event.xdm`을(를) 수정합니다.


```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "onBeforeEventSend": function(event) {
    // Change existing values
    event.xdm.web.webPageDetails.URL = xdm.web.webPageDetails.URL.toLowerCase();
    // Remove existing values
    delete event.xdm.web.webReferrer.URL;
    // Or add new values
    event.xdm._adb3lettersandnumbers.mycustomkey = "value";
  }
});
```

`xdm` 필드는 다음 순서로 설정됩니다.

1. 이벤트 명령 `alloy("sendEvent", { xdm: ... });`에 옵션으로 전달된 값
2. 자동으로 수집된 값.  ([자동 정보](../data-collection/automatic-information.md)를 참조하십시오.)
3. `onBeforeEventSend` 콜백에서 변경한 내용

`onBeforeEventSend` 콜백에서 예외가 발생해도 이벤트는 여전히 전송됩니다.하지만 콜백 내에서 수행된 변경 사항은 최종 이벤트에 적용되지 않습니다.

## 실행 가능한 잠재적 오류

이벤트를 전송할 때 전송 중인 데이터가 너무 큰 경우(전체 요청인 경우 32KB 이상) 오류가 발생할 수 있습니다. 이 경우 전송되는 데이터의 양을 줄여야 합니다.

디버깅이 활성화되면 서버는 구성된 XDM 스키마에 대해 전송되는 이벤트 데이터를 동기적으로 확인합니다. 데이터가 스키마와 일치하지 않으면 서버에서 불일치 세부 정보가 반환되고 오류가 발생합니다. 이 경우 스키마에 맞게 데이터를 수정합니다. 디버깅이 활성화되지 않으면 서버가 데이터를 비동기적으로 검사하므로 해당 오류가 발생하지 않습니다.
