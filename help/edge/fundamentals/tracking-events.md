---
title: 이벤트 추적
seo-title: Adobe Experience Platform 웹 SDK 이벤트 추적
description: Experience Platform 웹 SDK 이벤트를 추적하는 방법 학습
seo-description: Experience Platform 웹 SDK 이벤트를 추적하는 방법 학습
translation-type: tm+mt
source-git-commit: 45ee1f79ac5953b7c407083b4352b2c751e8aec9

---


# 이벤트 추적

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

이벤트 데이터를 Adobe Experience Cloud로 전송하려면 `event` 명령을 사용합니다. 이 명령은 Experience Cloud로 데이터를 보내고 개인화된 콘텐츠, ID 및 대상 대상을 가져오는 기본 방법입니다. `event`

Adobe Experience Cloud로 전송된 데이터는 두 가지 카테고리로 분류됩니다.

* XDM 데이터
* XDM 데이터가 아닌 데이터(현재 지원되지 않음)

## XDM 데이터 전송

XDM 데이터는 컨텐츠 및 구조가 Adobe Experience Platform 내에서 만든 스키마와 일치하는 객체입니다. [스키마를 만드는 방법에 대해 자세히 알아보십시오.](../../xdm/tutorials/create-schema-ui.md)

분석, 개인화, 고객 또는 대상의 일부로 사용하려는 모든 XDM 데이터는 `xdm` 옵션을 사용하여 전송해야 합니다.

```javascript
alloy("event", {
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

>[!NOTE]
>XDM 필드의 각 이벤트에서 전송할 수 있는 데이터에는 32KB 제한이 있습니다.

### XDM 이외의 데이터 전송

현재 XDM 스키마와 일치하지 않는 데이터를 전송할 수 없습니다. 지원은 향후 날짜로 예정되어 있습니다.

### 설정 `eventType`

XDM 경험 이벤트에는 필드가 `eventType` 있습니다. 여기에는 레코드의 기본 이벤트 유형이 포함됩니다. 이 옵션은 옵션의 일부로 전달될 수 `xdm` 있습니다.

```javascript
alloy("event", {
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

또는 옵션을 사용하여 이벤트 명령으로 전달될 `eventType` 수 `type` 있습니다. 백그라운드에서 XDM 데이터에 추가됩니다. 옵션 `type` 을 사용하면 XDM 페이로드를 수정하지 않고도 `eventType` 보다 손쉽게 설정할 수 있습니다.

```javascript
var myXDMData = { ... };

alloy("event", {
  "xdm": myXDMData,
  "type": "commerce.purchases"
});
```

### 보기 시작

보기가 시작되면 명령 내 `viewStart` 로 설정하여 SDK에 `true` 알려야 `event` 합니다. 이는 SDK가 개인화된 컨텐츠를 검색하고 렌더링해야 함을 의미합니다. 현재 개인화를 사용하고 있지 않더라도 페이지 내 코드를 수정할 필요가 없기 때문에 나중에에서 개인화 또는 기타 기능을 간편하게 사용할 수 있습니다. 또한 데이터 수집 후 분석 보고서를 볼 때 보기 추적을 하면 유용합니다.

뷰의 정의는 컨텍스트에 따라 달라질 수 있습니다.

* 일반 웹 사이트에서 각 웹 페이지는 일반적으로 고유한 보기로 간주됩니다. 이 경우, 설정된 이벤트 `viewStart` 는 페이지 맨 위에서 가능한 빨리 `true` 실행해야 합니다.
* 단일 페이지 응용 프로그램 \(SPA\)에서 보기가 덜 정의되어 있습니다. 이는 일반적으로 사용자가 애플리케이션 내에서 탐색했으며 대부분의 컨텐츠가 변경되었음을 의미합니다. 단일 페이지 애플리케이션의 기술적 기초 위에 익숙한 사용자는 일반적으로 애플리케이션이 새로운 경로를 로드할 때 발생합니다. 사용자가 새 보기로 이동할 때마다 _보기를_&#x200B;정의하도록 선택하면 `viewStart` 설정된 이벤트가 `true` 실행됩니다.

다음으로 설정된 이벤트 `viewStart` `true` 는 Adobe Experience Cloud로 데이터를 보내고 Adobe Experience Cloud에서 콘텐츠를 요청하는 기본 메커니즘입니다. 보기를 시작하는 방법은 다음과 같습니다.

```javascript
alloy("event", {
  "viewStart": true,
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

데이터가 전송되면 서버는 개인화된 컨텐츠로 응답합니다. 이 개인화된 컨텐츠는 사용자의 관점에서 자동으로 렌더링됩니다. 링크 핸들러는 새 보기의 컨텐츠에도 자동으로 첨부됩니다.

## sendBeacon API 사용

웹 페이지 사용자가 다른 곳으로 이동하기 전에 이벤트 데이터를 전송하기가 어려울 수 있습니다. 요청이 너무 길면 브라우저가 요청을 취소할 수 있습니다. 일부 브라우저는 이 시간 동안 데이터를 보다 쉽게 수집할 수 있도록 `sendBeacon` 하는 웹 표준 API를 구현했습니다. 사용 `sendBeacon`시 브라우저는 글로벌 브라우징 컨텍스트에서 웹 요청을 수행합니다. 즉, 브라우저가 백그라운드에서 비콘 요청을 수행하고 페이지 탐색을 유지하지 않습니다. Adobe Experience Platform 웹 SDK에 사용할 수 있도록 하려면 이벤트 명령 `sendBeacon``"documentUnloading": true` 에 옵션을 추가합니다.  다음은 한 예입니다.

```javascript
alloy("event", {
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

브라우저는 한 번에 전송할 수 있는 데이터 양을 제한했습니다 `sendBeacon` . 많은 브라우저에서 제한은 64K입니다. 페이로드가 너무 커서 브라우저가 이벤트를 거부하는 경우, Adobe Experience Platform 웹 SDK는 일반적인 전송 방식(예: 가져오기)을 다시 사용합니다.

## 이벤트의 응답 처리

이벤트에서 응답을 처리하려면 다음과 같이 성공 또는 실패에 대한 알림을 받을 수 있습니다.

```javascript
alloy("event", {
  "viewStart": true,
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
}).then(function() {
    // Tracking the event succeeded.
  })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

## 전역 이벤트 수정 {#modifying-events-globally}

이벤트에서 전체적으로 필드를 추가, 제거 또는 수정하려면 콜백을 구성할 수 `onBeforeEventSend` 있습니다.  이 콜백은 이벤트가 전송될 때마다 호출됩니다.  이 콜백은 필드가 있는 이벤트 개체에서 `xdm` 전달됩니다.  이벤트 `event.xdm` 에서 전송된 데이터를 변경하려면 수정합니다.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
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

1. 이벤트 명령에 옵션으로 전달된 값 `alloy("event", { xdm: ... });`
2. 자동으로 수집된 값.  자세한 내용은 [자동 정보를 참조하십시오](../reference/automatic-information.md).
3. 콜백에서 수행된 `onBeforeEventSend` 변경 사항.

콜백에서 `onBeforeEventSend` 예외가 발생해도 이벤트가 계속 전송됩니다. 하지만 콜백 내에서 수행된 변경 사항은 최종 이벤트에 적용되지 않습니다.

## 실행 가능한 잠재적 오류

이벤트를 전송할 때 전송 중인 데이터가 너무 큰 경우(전체 요청의 경우 32KB 이상) 오류가 발생할 수 있습니다. 이 경우 전송되는 데이터의 양을 줄여야 합니다.

디버깅이 활성화되면 서버는 구성된 XDM 스키마에 대해 전송되는 이벤트 데이터를 동기식으로 검증합니다. 데이터가 스키마와 일치하지 않으면 서버에서 불일치 세부 정보가 반환되고 오류가 발생합니다. 이 경우 스키마를 일치하도록 데이터를 수정합니다. 디버깅이 활성화되지 않으면 서버가 데이터를 비동기식으로 검증하므로 해당 오류가 발생하지 않습니다.
