---
title: Platform Web SDK에서 Offer decisioning 사용
description: Adobe Experience Platform Web SDK는 Offer decisioning에서 관리되는 개인화된 오퍼를 제공하고 렌더링할 수 있습니다. offer decisioning UI 또는 API를 사용하여 오퍼 및 기타 관련 개체를 만들 수 있습니다.
keywords: offer decisioning;의사 결정;웹 SDK;Platform Web SDK;개인화된 오퍼;오퍼 게재;오퍼 게재;오퍼 개인화;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 3%

---

# Platform Web SDK에서 Offer decisioning 사용

>[!NOTE]
>
>Adobe Experience Platform Web SDK에서 Offer decisioning을 사용하면 현재 사용자를 선택하기 위해 일찍 액세스할 수 있습니다. 모든 IMS 조직에서는 이 기능을 사용할 수 없습니다.

Adobe Experience Platform [!DNL Web SDK]은 Offer decisioning에서 관리되는 개인화된 오퍼를 제공하고 렌더링할 수 있습니다. UI(Offer decisioning 사용자 인터페이스) 또는 API를 사용하여 오퍼 및 기타 관련 개체를 만들 수 있습니다.

## 전제 조건

* IMS 조직은 Edge Decisioning에 대해 활성화됩니다
* 오퍼, 만들어진 활동
* 데이터 스트림이 게시됨

## 용어

offer decisioning 작업 시 다음 용어를 이해하는 것이 중요합니다. 자세한 내용을 알고 추가 용어를 보려면 [Offer decisioning 용어집](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html)을 방문하십시오.

* **컨테이너:** 컨테이너는 서로 다른 문제를 구분하기 위한 격리 메커니즘입니다. 컨테이너 ID는 모든 저장소 API의 첫 번째 경로 요소입니다. 모든 의사 결정 개체는 컨테이너 내에 있습니다.

* **결정 범위:** Offer decisioning의 경우, offer decisioning 서비스에서 오퍼를 제안하는 데 사용할 활동 및 배치 ID가 포함된 JSON의 Base64 인코딩 문자열입니다.

   *결정 범위 JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *결정 범위 Base64 인코딩 문자열:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >UI의 **활동 개요** 페이지에서 의사 결정 범위 값을 복사할 수 있습니다.

   ![](assets/decision-scope-copy.png)

* **데이터 스트림:** 자세한 내용은 데이터  [](../../fundamentals/datastreams.md) 세트 설명서 를 참조하십시오.

* **ID**: 자세한 내용은  [Platform Web SDK에서 ID 서비스를 활용하는 방법에 대한 개요를 제공하는 이 설명서를 참조하십시오](../../identity/overview.md).

## offer decisioning 활성화

offer decisioning을 활성화하려면 다음 단계를 수행해야 합니다.

1. [데이터 스트림](../../fundamentals/datastreams.md)에서 Adobe Experience Platform을 활성화하고 &quot;Offer decisioning&quot; 상자를 선택합니다

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. 지침에 따라 [SDK](../../fundamentals/installing-the-sdk.md) 설치(SDK는 독립 실행형 또는 [데이터 수집 UI](https://experience.adobe.com/#/data-collection/)를 통해 설치할 수 있습니다. 자세한 내용은 [태그 빠른 시작 안내서](../../../tags/quick-start/quick-start.md))를 참조하십시오.
1. [offer decisioning용 ](../../fundamentals/configuring-the-sdk.md) SDK를 구성합니다. 추가적인 Offer decisioning 특정 단계는 아래에 제공됩니다.

   * 독립형 SDK 설치

      1. `decisionScopes`으로 &quot;sendEvent&quot; 작업을 구성합니다

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```
   * 태그를 통해 SDK 설치

      1. [태그 속성 만들기](../../../tags/ui/administration/companies-and-properties.md)
      1. [포함 코드 추가](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. &quot;데이터 스트림&quot; 드롭다운에서 구성을 선택하여 방금 만든 데이터 스트림으로 Platform Web SDK 확장을 설치하고 구성합니다. [확장](../../../tags/ui/managing-resources/extensions/overview.md)에 대한 설명서를 참조하십시오.

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. 필요한 [데이터 요소](../../../tags/ui/managing-resources/data-elements.md)를 만듭니다. 최소한으로, Platform 웹 SDK ID 맵과 Platform 웹 SDK XDM 개체 데이터 요소를 만들어야 합니다.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. [규칙](../../../tags/ui/managing-resources/rules.md)을 만듭니다.

         * Platform Web SDK 이벤트 보내기 작업을 추가하고 해당 작업의 구성에 관련 `decisionScopes`을 추가합니다

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [구성한 ](../../../tags/ui/publishing/libraries.md) 관련 규칙, 데이터 요소 및 확장이 포함된 라이브러리를 만들고 게시합니다



## 샘플 요청 및 응답

### 하나의 `decisionScopes` 값

**요청**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| 속성 | 필수 여부 | 설명 | 제한 | 예 |
|---|---|---|---|---|
| `identityMap` | 예 | 이 [ID 서비스 설명서](../../identity/overview.md)를 참조하십시오. | 요청당 하나의 ID. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 예 | 활동 및 배치 ID가 포함된 JSON의 Base64 인코딩 문자열 배열입니다. | 요청당 최대 30개 `decisionScopes`. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**응답**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 속성 | 설명 | 예 |
|---|---|---|
| `scope` | 제안된 오퍼를 초래한 결정 범위입니다. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 오퍼 활동의 고유 ID입니다. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 오퍼 배치의 고유 ID입니다. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 제안된 오퍼와 연결된 컨텐츠의 스키마. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 제안된 오퍼와 연관된 컨텐츠의 형식입니다. | `"format": "text/html"` |
| `language` | 제안된 오퍼의 컨텐츠와 연관된 언어 배열입니다. | `"language": [ "en-US" ]` |
| `content` | 문자열 형식의 제안된 오퍼와 연관된 컨텐츠. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | URL 형식으로 제안된 오퍼와 연결된 이미지 컨텐츠. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON 개체 형식의 제안된 오퍼와 연관된 특성입니다. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 여러 `decisionScopes` 값

**요청**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| 속성 | 필수 여부 | 설명 | 제한 | 예 |
|---|---|---|---|---|
| `identityMap` | 예 | 이 [ID 서비스 설명서](../../identity/overview.md)를 참조하십시오. | 요청당 하나의 ID. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 예 | 활동 및 배치 ID가 포함된 JSON의 Base64 인코딩 문자열 배열입니다. | 요청당 최대 30개 `decisionScopes`. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**응답**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 속성 | 설명 | 예 |
|---|---|---|
| `scope` | 제안된 오퍼를 초래한 결정 범위입니다. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 오퍼 활동의 고유 ID입니다. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | 오퍼 배치의 고유 ID입니다. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | 제안된 오퍼와 연결된 컨텐츠의 스키마. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | 제안된 오퍼와 연관된 컨텐츠의 형식입니다. | `"format": "text/text"` |
| `language` | 제안된 오퍼의 컨텐츠와 연관된 언어 배열입니다. | `"language": [ "en-US" ]` |
| `content` | 문자열 형식의 제안된 오퍼와 연관된 컨텐츠. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | URL 형식으로 제안된 오퍼와 연결된 이미지 컨텐츠. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON 개체 형식의 제안된 오퍼와 연관된 특성입니다. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
