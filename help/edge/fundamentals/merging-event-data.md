---
title: 이벤트 데이터 병합
seo-title: Adobe Experience Platform 웹 SDK 이벤트 데이터 병합
description: Experience Platform 웹 SDK 이벤트 데이터를 병합하는 방법 살펴보기
seo-description: Experience Platform 웹 SDK 이벤트 데이터를 병합하는 방법 살펴보기
keywords: merge;event data;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise; Merge Id Promise;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# 이벤트 데이터 병합

>[!IMPORTANT]
>
>이 기능은 아직 개발 중입니다. 이 페이지에 설명된 대로 일부 솔루션에서 이벤트 데이터를 병합할 수는 없습니다.

이벤트 발생 시 일부 데이터를 사용할 수 없는 경우가 있습니다. 예를 들어 사용자가 브라우저를 닫으면 데이터가 손실되지 않도록 사용자가 갖고 있는 데이터를 캡처할 수 있습니다. 반면에 나중에 사용할 수 있게 될 데이터도 포함할 수 있습니다.

이러한 경우 다음과 같은 명령 옵션으로 전달하여 이전 이벤트 `mergeId` 와 데이터를 `event` 병합할 수 있습니다.

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
  },
  "mergeId": "ABC123"
});

// Time passes and more data becomes available

alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "payments": [
          {
            "transactionID": "TR426941",
            "paymentAmount": 999.98,
            "paymentType": "credit_card",
            "currencyCode": "USD"
          }
        ]
      }
    }
  },
  "mergeId": "ABC123"
});
```

이 예제에서 두 이벤트 명령 모두에 동일한 `mergeId` 옵션에 대해 동일한 값을 전달함으로써 두 번째 이벤트 명령의 데이터는 첫 번째 이벤트 명령에서 이전에 전송된 데이터로 증가됩니다. 보고서에서 각 이벤트 명령에 대한 레코드가 만들어지지만 보고 중에는 이벤트 병합 ID를 사용하여 레코드가 함께 결합되고 단일 이벤트로 나타납니다. [!DNL Experience Data Platform]

특정 이벤트에 대한 데이터를 타사 공급업체에 보내는 경우 해당 데이터와 동일한 이벤트 병합 ID를 포함할 수도 있습니다. 나중에 타사 데이터를 Adobe Experience Platform으로 가져오기로 선택하면 이벤트 병합 ID가 웹 페이지에서 발생한 개별 이벤트의 결과로 수집된 모든 데이터를 병합하는 데 사용됩니다.

## 이벤트 병합 ID 생성

이벤트 병합 ID는 선택한 모든 문자열일 수 있지만, 동일한 ID를 사용하여 전송된 모든 이벤트는 단일 이벤트로 보고되므로 이벤트를 병합하지 않아야 할 때 고유성을 강제 적용하도록 주의하십시오. SDK가 귀하를 대신하여 고유한 이벤트 병합 ID를 생성하도록 하려는 경우(널리 채택된 [UUID v4 사양에](https://www.ietf.org/rfc/rfc4122.txt)따라) `createEventMergeId` 명령을 사용하여 생성할 수 있습니다.

모든 명령과 마찬가지로 SDK 로드가 완료되기 전에 명령을 실행할 수 있으므로 약속이 반환됩니다. 약속은 가능한 한 빨리 고유한 이벤트 병합 ID로 해결됩니다. 다음과 같이 데이터를 서버에 보내기 전에 약속이 해결될 때까지 기다릴 수 있습니다.

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
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
    },
    "mergeId": results.eventMergeId
  });
});

// Time passes and more data becomes available

eventMergeIdPromise.then(function(results) {
  alloy("sendEvent", {
    "xdm": {
      "commerce": {
        "order": {
          "payments": [
            {
              "transactionID": "TR426941",
              "paymentAmount": 999.98,
              "paymentType": "credit_card",
              "currencyCode": "USD"
            }
          ]
        }
      }
    },
    "mergeId": results.eventMergeId
  });
});
```

다른 이유로 이벤트 병합 ID에 액세스하려는 경우(예: 타사 공급업체에 보내기) 동일한 패턴을 따릅니다.

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## XDM 포맷 참고

이벤트 명령 내에서, 이벤트 병합 ID는 사용자 대신 올바른 위치의 페이로드에 `xdm` 추가됩니다.  원하는 경우 다음과 같이 이벤트 병합 ID를 대신 옵션의 일부로 `xdm` 보낼 수 있습니다.

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
    },
    "eventMergeId": "ABC123"
  }
});
```

이벤트 병합 ID를 `xdm` 개체에 직접 추가할 때 이름이 대신 `eventMergeID` 사용됩니다 `mergeId`.
