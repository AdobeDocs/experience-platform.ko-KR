---
title: 콜백 끝점
description: Reactor API에서 /callbacks 종단점을 호출하는 방법을 알아봅니다.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 8%

---

# 콜백 끝점

콜백은 Reactor API가 특정 URL(일반적으로 조직에서 호스팅하는 URL)로 전송하는 메시지입니다.

콜백은 [감사 이벤트](./audit-events.md)와 함께 사용하여 Reactor API의 활동을 추적합니다. 특정 유형의 감사 이벤트가 생성될 때마다 콜백은 지정된 URL에 일치하는 메시지를 보낼 수 있습니다.

콜백에 지정된 URL 뒤의 서비스는 HTTP 상태 코드 200(OK) 또는 201(생성됨)으로 응답해야 합니다. 서비스가 이러한 상태 코드로 응답하지 않으면 다음 간격으로 메시지 배달을 다시 시도합니다.

* 1분
* 5분
* 30분
* 1시간
* 12시간
* 1일
* 3일

>[!NOTE]
>
>다시 시도 간격은 이전 간격에 상대적입니다. 예를 들어, 1분에 재시도가 실패하면 1분 시도가 실패한 후 5분 동안(메시지가 생성된 후 6분) 다음 시도가 예약됩니다.

모든 배달 시도가 실패하면 메시지가 무시됩니다.

콜백은 정확히 하나의 [속성](./properties.md)에 속합니다. 속성에는 많은 콜백이 있을 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)의 일부입니다. 계속하기 전에 API 인증 방법에 대한 중요한 정보가 필요하면 [시작 안내서](../getting-started.md)를 검토하십시오.

## 콜백 나열 {#list}

GET 요청을 만들어 속성 아래에 모든 콜백을 나열할 수 있습니다.

**API 형식**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| 매개 변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 콜백을 나열할 속성의 `id` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 콜백을 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`updated_at`</li></ul>자세한 내용은 [응답 필터링](../guides/filtering.md)에 대한 안내서를 참조하십시오.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 속성에 대한 콜백 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 콜백 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 콜백을 조회할 수 있습니다.

**API 형식**

```http
GET /callbacks/{CALLBACK_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `CALLBACK_ID` | 조회할 콜백의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 콜백의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## 콜백 만들기 {#create}

POST 요청을 수행하여 새 콜백을 만들 수 있습니다.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 에서 콜백을 정의하는 [속성](./properties.md)의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `url` | 콜백 메시지의 URL 대상입니다. URL은 HTTPS 프로토콜 확장을 사용해야 합니다. |
| `subscriptions` | 콜백을 트리거할 감사 이벤트 유형을 나타내는 문자열 배열입니다. 가능한 이벤트 유형 목록은 [감사 이벤트 엔드포인트 안내서](./audit-events.md)를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 새로 만든 콜백의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## 콜백 업데이트

PUT 요청 경로에 해당 ID를 포함하여 콜백을 업데이트할 수 있습니다.

**API 형식**

```http
PUT /callbacks/{CALLBACK_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `CALLBACK_ID` | 업데이트할 콜백의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 콜백용 `subscriptions` 배열을 업데이트합니다.

```shell
curl -X PUT \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 콜백용으로 업데이트할 속성을 나타내는 속성을 갖는 객체입니다. 각 키는 업데이트해야 하는 특정 콜백 속성과 해당 값을 나타냅니다.<br><br>콜백용으로 다음 속성을 업데이트할 수 있습니다.<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | 업데이트할 콜백의 `id` 이 값은 요청 경로에 제공된 `{CALLBACK_ID}` 값과 일치해야 합니다. |
| `type` | 업데이트할 리소스 유형입니다. 이 끝점의 경우 값은 `callbacks`이어야 합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 업데이트된 콜백의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## 콜백 삭제

DELETE 요청 경로에 해당 ID를 포함하여 콜백을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `CALLBACK_ID` | 삭제할 콜백의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적인 응답은 콜백이 삭제되었음을 나타내는 응답 본문이 없는 HTTP 상태 204(컨텐츠 없음)를 반환합니다.
