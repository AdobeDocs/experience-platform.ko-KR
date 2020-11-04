---
title: Offer Decisioning 개요
seo-title: Offer Decisioning 및 Adobe Experience Platform 웹 SDK
description: Adobe Experience Platform 웹 SDK는 Offer Decisioning에서 관리하는 맞춤형 프로모션을 제공하고 렌더링할 수 있습니다. Offer Decisioning UI 또는 API를 사용하여 오퍼 및 기타 관련 개체를 만들 수 있습니다.
seo-description: Adobe Experience Platform 웹 SDK는 Offer Decisioning에서 관리하는 맞춤형 프로모션을 제공하고 렌더링할 수 있습니다. Offer Decisioning UI 또는 API를 사용하여 오퍼 및 기타 관련 개체를 만들 수 있습니다.
keywords: offer decisioning;decisioning;Web SDK;Platform Web SDK;personalized offers;deliver offers;offer delivery;offer personalization;
translation-type: tm+mt
source-git-commit: b10b930dca504b7672eb05bd88ab44d09d9e5c0a
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 9%

---


# [!DNL Offer Decisioning] 개요

>[!NOTE]
>
>현재 Adobe Experience Platform 웹 SDK에서 Offer Decisioning을 사용할 수 있으며 특정 사용자를 조기에 이용할 수 있습니다. 이 기능은 일부 IMS 조직에서 사용할 수 없습니다.

Adobe Experience Platform은 Offer Decisioning에서 관리되는 개인화된 제안을 제공하고 렌더링할 [!DNL Web SDK] 수 있습니다. Offer Decisioning 사용자 인터페이스(UI) 또는 API를 사용하여 오퍼 및 기타 관련 개체를 만들 수 있습니다.

## 전제 조건

* IMS 조직이 에지 의사 결정 기능을 사용할 수 있습니다.
* 오퍼, 생성된 활동
* 에지 구성이 게시됨

## 용어

Offer Decisioning에서 일할 때 다음 용어를 이해하는 것이 중요합니다. 자세한 내용이나 추가 용어를 보려면 [Offer Decisioning 용어집을 방문하십시오](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html?lang=en#get-started).

* **컨테이너:** 컨테이너는 서로 다른 우려를 분리시키는 격리 메커니즘입니다. 컨테이너 ID는 모든 저장소 API에 대한 첫 번째 경로 요소입니다. 모든 의사 결정 개체는 컨테이너 내에 있습니다.

* **결정 범위:** Offer Decisioning의 경우, 오퍼 의사 결정 서비스가 오퍼를 제안하는 데 사용할 활동 및 배치 ID가 포함된 JSON의 Base64 인코딩 문자열입니다.

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

**에지 구성:** 자세한 내용은 [Edge 구성](../../fundamentals/edge-configuration.md) 설명서를 참조하십시오.

**ID**:자세한 내용은 Platform Web SDK가 Identity Service를 활용하는 방법에 대한 개요를 [설명하는 이 설명서를 참조하십시오](../../identity/overview.md).

## Offer Decisioning 활성화

Offer Decisioning을 활성화하려면 다음 단계를 수행해야 합니다.

1. Adobe Experience Platform을 [에지 구성에서](../../fundamentals/edge-configuration.md) 활성화한 다음 &quot;Offer Decisioning&quot; 상자를 선택합니다.
   ![offer-decising-edge-config](./assets/offer-decisioning-edge-config.png)
2. 지침에 따라 SDK를 [설치합니다](../../fundamentals/installing-the-sdk.md) (SDK는 독립 실행형 또는 [Adobe Experience Platform Launch을 통해 설치할 수 있습니다](http://launch.adobe.com/). 다음은 Launch에 대한 [빠른 시작 안내서입니다](https://docs.adobe.com/content/help/ko-KR/launch/using/intro/get-started/quick-start.html).
3. [Offer Decisioning용 SDK](../../fundamentals/configuring-the-sdk.md) 구성 아래에 Offer Decisioning 특정 추가 단계가 제공됩니다.
   * 독립형 설치 SDK
      1. &quot;sendEvent&quot; 동작을 `decisionScopes`

      ```javascript
      alloy("sendEvent", {
          ...
          "decisionScopes": [
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
              "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
          ]
      })
      ```
   * 설치된 SDK 실행
      1. [론치 속성 만들기](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/admin/companies-and-properties.html)
      2. [Launch 포함 코드 추가](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. &quot;에지 구성&quot; 드롭다운에서 구성을 선택하여 방금 만든 에지 구성을 사용하여 AEP 웹 SDK 익스텐션을 설치하고 구성합니다. 익스텐션에 대한 유용한 [설명서입니다](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. 필요한 [데이터 요소를 만듭니다](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/manage-resources/data-elements.html). 최소 AEP 웹 SDK Identity Map 및 AEP 웹 SDK XDM 개체 데이터 요소를 만들어야 합니다. (여기에서 연결할 수 있는 AEP 웹 SDK 데이터 요소에 대한 더 많은 설명서가 필요함)
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. 규칙 [만들기를 참조하십시오](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/manage-resources/rules.html).
         * AEP 웹 SDK 이벤트 보내기 작업 추가 및 해당 작업의 구성 `decisionScopes` 에 관련 추가
            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      6. [구성한 모든 관련 규칙, 데이터 요소 및 익스텐션이 포함된 라이브러리](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/publish/libraries.html) 만들기 및 게시


## 요청 및 응답 샘플

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
| `identityMap` | 예 | 이 ID [서비스 설명서를 참조하십시오](../../identity/overview.md). | 요청당 ID 1개 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 예 | 활동 및 배치 ID를 포함하는 JSON의 Base64 인코딩 문자열 배열. | 요청당 최대 30 `decisionScopes` 개 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
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
| `scope` | 제안된 오퍼를 일으킨 결정 범위. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `items.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 제안된 오퍼와 연관된 컨텐츠의 스키마입니다. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 제안된 오퍼와 연관된 컨텐츠의 형식. | `"format": "text/html"` |
| `language` | 제안된 오퍼의 컨텐츠와 연관된 언어 배열. | `"language": [ "en-US" ]` |
| `content` | 제안된 오퍼와 연관된 컨텐츠는 문자열 형식으로 표시됩니다. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | URL 형식의 제안된 오퍼와 연관된 이미지 컨텐츠. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON 개체 형식의 제안된 오퍼와 관련된 특성입니다. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

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
| `identityMap` | 예 | 이 ID [서비스 설명서를 참조하십시오](../../identity/overview.md). | 요청당 ID 1개 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | 예 | 활동 및 배치 ID를 포함하는 JSON의 Base64 인코딩 문자열 배열. | 요청당 최대 30 `decisionScopes` 개 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p style="color:red;">20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:235fe313094cdb75",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "data": {
                "id": "xcore:personalized-offer:235fe313094cdb75",
                "format": "text/text",
                "language": [
                  "en-US"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2",
                  "foo3": "bar3"
                }
              }
            }
          ]
        }
      ],
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ==",
          "items": [
            {
              "id": "xcore:personalized-offer:312de312095cda65",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "data": {
                "id": "xcore:personalized-offer:312de312095cda65",
                "format": "image/png",
                "language": [
                  "en-US"
                ],
                "deliveryURL": "https://image.jpeg"
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
| `scope` | 제안된 오퍼를 일으킨 결정 범위. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `items.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 제안된 오퍼와 연관된 컨텐츠의 스키마입니다. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 제안된 오퍼의 ID입니다. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 제안된 오퍼와 연관된 컨텐츠의 형식. | `"format": "text/html"` |
| `language` | 제안된 오퍼의 컨텐츠와 연관된 언어 배열. | `"language": [ "en-US" ]` |
| `content` | 제안된 오퍼와 연관된 컨텐츠는 문자열 형식으로 표시됩니다. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | URL 형식의 제안된 오퍼와 연관된 이미지 컨텐츠. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | JSON 개체 형식의 제안된 오퍼와 관련된 특성입니다. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |