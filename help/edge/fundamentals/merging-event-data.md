---
title: Adobe Experience Platform 웹 SDK에서 이벤트 데이터 병합
description: Experience Platform 웹 SDK 이벤트 데이터를 병합하는 방법 알아보기
keywords: merge;eventData;eventMergeId;createEventMergeId;sendEvent;mergeId;merge id;eventMergeIdPromise;eventMergeIdPromise;ID 병합 약속;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---


# 이벤트 데이터 병합

>[!IMPORTANT]
>
>이 기능은 아직 개발 중입니다. 이 페이지에 설명된 대로 일부 솔루션에서는 이벤트 데이터를 병합할 수 없습니다.

이벤트가 발생할 때 일부 데이터를 사용할 수 없는 경우가 있습니다. 예를 들어 사용자가 브라우저를 닫으면 데이터가 손실되지 않도록 기존 데이터를 캡처할 수 있습니다. 반면에 나중에 사용할 수 있게 될 데이터도 포함할 수 있습니다.

이러한 경우 다음과 같이 `event` 명령에 대한 옵션으로 `mergeId`을 전달하여 이전 이벤트와 데이터를 병합할 수 있습니다.

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

이 예제에서 두 이벤트 명령 모두에 `mergeId` 옵션에 동일한 값을 전달하면 두 번째 이벤트 명령의 데이터가 첫 번째 이벤트 명령에서 이전에 전송된 데이터로 증가됩니다. 각 이벤트 명령에 대한 레코드가 [!DNL Experience Data Platform]에 만들어지지만 보고 중에 레코드는 이벤트 병합 ID를 사용하여 함께 결합되고 단일 이벤트로 표시됩니다.

특정 이벤트에 대한 데이터를 제3자 제공자에게 보내는 경우 해당 데이터와 동일한 이벤트 병합 ID를 포함할 수도 있습니다. 나중에 제3자 데이터를 Adobe Experience Platform으로 가져오기로 선택하면 이벤트 병합 ID를 사용하여 웹 페이지에서 발생한 개별 이벤트의 결과로 수집된 모든 데이터를 병합합니다.

## 이벤트 병합 ID 생성

이벤트 병합 ID는 사용자가 선택하는 모든 문자열일 수 있지만, 동일한 ID를 사용하여 전송된 모든 이벤트는 단일 이벤트로 보고되므로, 이벤트를 병합하지 않아야 할 때 고유성을 적용하도록 주의하십시오. SDK가 귀하를 대신하여 고유한 이벤트 병합 ID를 생성하도록 하려는 경우(널리 채택된 [UUID v4 사양](https://www.ietf.org/rfc/rfc4122.txt) 다음에) `createEventMergeId` 명령을 사용하여 그렇게 할 수 있습니다.

모든 명령과 마찬가지로 SDK 로드가 완료되기 전에 명령을 실행할 수 있으므로 약속이 반환됩니다. 가능한 한 빨리 고유 이벤트 병합 ID로 약속이 해결됩니다. 다음과 같이 데이터를 서버로 보내기 전에 약속이 해결될 때까지 기다릴 수 있습니다.

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

다른 이유로 이벤트 병합 ID에 액세스하려는 경우(예: 제3자 공급자에게 이벤트 ID를 전송하는 경우) 동일한 패턴을 따릅니다.

```javascript
var eventMergeIdPromise = alloy("createEventMergeId");

eventMergeIdPromise.then(function(results) {
  // send event merge ID to a third-party provider
  console.log(results.eventMergeId);
});
```

## XDM 형식에 대한 참고 사항

이벤트 명령 내에서, 이벤트 병합 ID는 귀하를 대신하여 올바른 위치의 `xdm` 페이로드에 추가됩니다.  원하는 경우 다음과 같이 이벤트 병합 ID를 대신 `xdm` 옵션의 일부로 보낼 수 있습니다.

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

이벤트 병합 ID를 `xdm` 개체에 직접 추가할 때 `mergeId` 대신 `eventMergeID` 이름이 사용된다는 것을 알 수 있습니다.
