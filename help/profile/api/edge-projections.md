---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: Edge Projection API 끝점
type: Documentation
description: Adobe Experience Platform을 사용하면 변경 사항이 발생할 때 올바른 데이터를 즉시 사용할 수 있고 지속적으로 업데이트하여 여러 채널에서 실시간으로 고객에게 통합되고 일관되며 개인화된 경험을 제공할 수 있습니다. 이 작업은 데이터를 저장하고 애플리케이션에 쉽게 액세스할 수 있도록 해주는 지리적으로 배치된 서버인 가장자리를 사용하여 수행됩니다.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 2%

---

# 에지 투영 구성 및 대상 끝점

여러 채널에서 실시간으로 고객에게 통합되고 일관되고 개인화된 경험을 제공하려면 변경 사항이 발생할 때 적합한 데이터를 즉시 사용할 수 있고 지속적으로 업데이트해야 합니다. Adobe Experience Platform을 사용하면 에지라고 알려진 것을 사용하여 데이터에 실시간으로 액세스할 수 있습니다. 에지는 데이터를 저장하고 애플리케이션에서 쉽게 액세스할 수 있도록 해주는 지리적으로 배치된 서버입니다. 예를 들어, Adobe Target 및 Adobe Campaign과 같은 Adobe 애플리케이션은 에지를 사용하여 개인화된 고객 경험을 실시간으로 제공합니다. 데이터가 전송되는 모서리를 정의하는 투영 대상 및 모서리에서 사용할 수 있는 특정 정보를 정의하는 투영 구성을 갖는 투영에 의해 데이터가 모서리로 라우팅됩니다. 이 안내서에서는 사용 방법에 대한 자세한 지침을 제공합니다. [!DNL Real-Time Customer Profile] 대상 및 구성을 포함하여 에지 프로젝션과 작업할 수 있는 API입니다.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 계속하기 전에 다음을 검토하십시오. [시작 안내서](getting-started.md) 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기에 대한 안내서 및 를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보 [!DNL Experience Platform] API.

>[!NOTE]
>
>페이로드가 포함된 요청(POST, PUT, PATCH)에는 `Content-Type` 머리글입니다. 두 개 이상 `Content-Type` 이 문서에서 사용됩니다. 올바른 을(를) 사용하고 있는지 확인하기 위해 샘플 호출의 헤더에 특별히 주의하십시오 `Content-Type` 각 요청에 대해.

## 투영 대상

데이터가 전송될 위치를 지정하여 하나 이상의 모서리에 투영을 라우팅할 수 있습니다. 생성된 각 투영 대상에는 고유한 ID가 있으며, 이 ID는 투영 구성을 생성하는 데 사용됩니다.

### 모든 대상 나열

에 GET 요청을 하여 조직에 대해 이미 만들어진 Edge 대상을 나열할 수 있습니다. `/config/destinations` 엔드포인트.

**API 형식**

```http
GET /config/destinations
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 다음이 포함됩니다. `projectionDestinations` 배열 내 개별 객체로 표시된 각 대상에 대한 세부 정보가 포함된 배열입니다. 프로젝션이 구성되지 않은 경우 `projectionDestinations` 배열이 빈 을 반환합니다.

>[!NOTE]
>
>이 응답은 공간에 대해 짧아졌으며 두 개의 대상만 표시됩니다.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| 속성 | 설명 |
|---|---|
| `_links.self.href` | 최상위 수준에서 은 GET 요청을 하는 데 사용되는 경로와 일치합니다. 각 개별 대상 개체 내에서 이 경로를 GET 요청에 사용하여 특정 대상의 세부 정보를 직접 조회할 수 있습니다. |
| `id` | 각 대상 객체 내에서 `"id"` 대상에 대한 읽기 전용, 시스템 생성 고유 ID를 표시합니다. 이 ID는 특정 대상을 참조하고 투영 구성을 생성할 때 사용됩니다. |

개별 대상의 속성에 대한 자세한 내용은 다음 섹션 을 참조하십시오 [대상 만들기](#create-a-destination) 그 다음입니다.

### 대상 만들기 {#create-a-destination}

필요한 대상이 아직 없는 경우 POST 요청을 통해 새 투영 대상을 생성할 수 있습니다. `/config/destinations` 엔드포인트.

**API 형식**

```http
POST /config/destinations
```

**요청**

다음 요청은 새 Edge 대상을 만듭니다.

>[!NOTE]
>
>대상을 만들기 위한 POST 요청에는 특정 항목이 필요합니다 `Content-Type` 머리글(아래 참조) 잘못된 항목 사용 `Content-Type` 헤더에서 HTTP 상태 415(지원되지 않는 미디어 유형) 오류가 발생합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| 속성 | 설명 |
|---|---|
| `type` **(필수 여부)** | 생성할 대상 유형입니다. 허용되는 유일한 값 &quot;EDGE&quot;는 Edge 대상을 생성합니다. |
| `dataCenters` **(필수 여부)** | 투영을 경로설정할 모서리를 나열하는 문자열 배열입니다. 다음 값 중 하나 이상을 포함할 수 있습니다. &quot;OR1&quot; - 미국 서부, &quot;VA5&quot; - 미국 동부, &quot;NLD1&quot; - EMEA. |
| `ttl` **(필수 여부)** | 프로젝션 만료를 지정합니다. 허용되는 값 범위: 600~604800. 기본값: 3600. |
| `replicationPolicy` **(필수 여부)** | 허브에서 에지로의 데이터 복제 동작을 정의합니다.  지원되는 값: 사전, 사후 기본값: 반응 |

**응답**

성공한 응답은 시스템이 생성한 읽기 전용 고유 ID( )를 포함하여 새로 생성된 에지 대상의 세부 정보를 반환합니다`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| 속성 | 설명 |
|---|---|
| `self.href` | 이 경로는 대상을 직접 조회(GET)하는 데 사용되며 대상을 업데이트(PUT)하거나 삭제(DELETE)하는 데에도 사용할 수 있습니다. |
| `id` | 대상에 대한 읽기 전용, 시스템 생성 고유 ID. 이 ID는 대상을 직접 참조하고 투영 구성을 생성하는 데 사용됩니다. |
| `version` | 이 읽기 전용 값은 대상의 현재 버전을 보여 줍니다. 대상이 업데이트되면 버전 번호가 자동으로 증가합니다. |

### 대상 보기

프로젝션 대상의 고유 ID를 알고 있는 경우 조회 요청을 수행하여 세부 정보를 볼 수 있습니다. 이 작업은 (으)로 GET 요청을 함으로써 수행됩니다. `/config/destinations` 엔드포인트 및 요청 경로에 대상 ID 포함

**API 형식**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DESTINATION_ID}` | 보려는 프로젝션 대상의 고유 ID. |

**요청**

다음 요청은 조회(GET)를 수행하여 요청 경로에 제공된 ID에 대한 대상을 확인합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 개체는 투영 대상의 세부 정보를 표시합니다. 다음 `id` 속성은 요청에 제공된 프로젝션 대상의 ID와 일치해야 합니다.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### 대상 업데이트

에 PUT 요청을 하여 기존 대상을 업데이트할 수 있습니다. `/config/destinations` 종단점 및 요청 경로에 업데이트할 대상 ID를 포함합니다. 이 작업은 본질적으로 대상을 다시 작성하는 것이므로 새 대상을 만들 때 제공된 것과 동일한 속성이 요청 본문에 제공되어야 합니다.

>[!CAUTION]
>
>업데이트 요청에 대한 API 응답은 즉각적이지만 예측 변경 사항은 비동기적으로 적용됩니다. 즉, 목적지의 정의에 대한 업데이트가 이루어진 시점과 적용되는 시점 간에는 시차가 존재한다.

**API 형식**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DESTINATION_ID}` | 업데이트하려는 프로젝션 대상의 고유 ID. |

**요청**

다음 요청은 두 번째 위치를 포함하도록 기존 대상을 업데이트합니다(`dataCenters`).

>[!IMPORTANT]
>
>PUT 요청에는 특정 `Content-Type` 머리글(아래 참조) 잘못된 항목 사용 `Content-Type` 헤더에서 HTTP 상태 415(지원되지 않는 미디어 유형) 오류가 발생합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| 속성 | 설명 |
|---|---|
| `currentVersion` | 기존 대상의 현재 버전입니다. 값 `version` 대상에 대한 조회 요청을 수행할 때의 특성입니다. |

**응답**

응답에는 ID 및 새 대상을 포함하여 대상에 대해 업데이트된 세부 정보가 포함됩니다 `version` 대상.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### 대상 삭제

조직에 더 이상 투영 대상이 필요하지 않은 경우 DELETE을 요청하여에 삭제할 수 있습니다. `/config/destinations` 엔드포인트 및 요청 경로에 삭제하려는 대상 ID 포함

>[!CAUTION]
>
>삭제 요청에 대한 API 응답은 즉각적이지만, 에지의 데이터에 대한 실제 변경 사항은 비동기적으로 발생합니다. 즉, 프로필 데이터가 모든 가장자리에서 제거됩니다( `dataCenters` 투영 대상에 지정되었지만 프로세스를 완료하는 데 시간이 소요됩니다.

**API 형식**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DESTINATION_ID}` | 삭제하려는 프로젝션 대상의 고유 ID. |


**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

삭제 요청은 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문을 반환합니다. 해당 ID로 대상에 대한 조회 요청을 수행하여 삭제가 성공했는지 확인할 수 있습니다. 조회는 HTTP 상태 404(찾을 수 없음)를 반환해야 합니다.

## 투영 구성

투영 구성은 각 에지에서 사용할 수 있어야 하는 데이터에 관한 정보를 제공합니다. 완전한 것으로 투영하지 않고 [!DNL Experience Data Model] (XDM) 스키마부터 에지까지 프로젝션은 스키마의 특정 데이터 또는 필드만 제공합니다. 조직은 각 XDM 스키마에 대해 둘 이상의 투영 구성을 정의할 수 있습니다.

### 모든 투영 구성 나열

에 GET 요청을 하여 조직에 대해 만들어진 모든 투영 구성을 나열할 수 있습니다. `/config/projections` 엔드포인트. 요청 경로에 선택적 매개 변수를 추가하여 특정 스키마에 대한 투영 구성에 액세스하거나 해당 이름으로 개별 투영을 조회할 수도 있습니다.

**API 형식**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 매개 변수 | 설명 |
|---|---|
| `{SCHEMA_NAME}` | 액세스하려는 투영 구성과 연관된 스키마 클래스의 이름입니다. |
| `{PROJECTION_NAME}` | 액세스하려는 투영 구성의 이름입니다. |

>[!NOTE]
>
>`schemaName` 을(를) 사용할 때 필요합니다. `name` 스키마 클래스 컨텍스트에서만 프로젝션 구성 이름이 고유한 매개 변수가 있습니다.

**요청**

다음 요청은 와 연관된 모든 투영 구성을 나열합니다. [!DNL Experience Data Model] 스키마 클래스, [!DNL XDM Individual Profile]. XDM 및 내의 해당 역할에 대한 자세한 내용 [!DNL Platform], 다음 문서를 읽는 것부터 시작하십시오. [XDM 시스템 개요](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 루트 내에서 투영 구성 목록을 반환합니다 `_embedded` 속성, 다음 내에 포함됨 `projectionConfigs` 배열입니다. 조직에 대한 투영 구성이 만들어지지 않은 경우 `projectionConfigs` 배열이 비어 있습니다.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### 투영 구성 만들기

에지에서 사용할 수 있는 XDM 필드를 지정하는 새 투영 구성을 생성(POST)할 수 있습니다.

**API 형식**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 매개 변수 | 설명 |
|---|---|
| `{SCHEMA_NAME}` | 액세스하려는 투영 구성과 연관된 스키마 클래스의 이름입니다. |

**요청**

>[!NOTE]
>
>구성을 만들기 위한 POST 요청에는 다음이 필요합니다. `Content-Type` 머리글(아래 참조) 잘못된 항목 사용 `Content-Type` 헤더에서 HTTP 상태 415(지원되지 않는 미디어 유형) 오류가 발생합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| 속성 | 설명 |
|---|---|
| `selector` | 스키마에는에지에복제될속성의목록을포함하는문자열. 선택기 작업에 대한 우수 사례는에서 사용할 수 있습니다. [선택기](#selectors) 섹션에 있는 마지막 항목이 될 필요가 없습니다. |
| `name` | 새 투영 구성에 대한 수사적 이름입니다. |
| `destinationId` | 데이터가 투영될 에지 대상에 대한 식별자입니다. |

**응답**

성공한 응답은 새로 생성된 투영 구성에 대한 세부 정보를 반환합니다.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## 선택기 {#selectors}

선택기는 쉼표로 구분된 XDM 필드 이름 목록입니다. 투영 구성에서, 선택기는 투영들에 포함될 속성들을 지정한다. 형식 `selector` 매개 변수 값은 XPath 구문을 기반으로 합니다. 참조용으로 제공된 추가 예와 함께 지원되는 구문이 아래에 요약되어 있습니다.

### 지원되는 구문

* 여러 필드를 선택하려면 쉼표를 사용하십시오. 공백은 사용하지 마십시오.
* 점 표기법을 사용하여 중첩된 필드를 선택합니다.
   * 예를 들어, `field` (은)는 이라는 필드 내에 중첩되어 있습니다. `foo`, 선택기 사용 `foo.field`.
* 하위 필드가 포함된 필드를 포함할 때 기본적으로 모든 하위 필드도 투영됩니다. 그러나 괄호를 사용하여 반환된 하위 필드를 필터링할 수 있습니다 `"( )"`.
   * 예를 들어, `addresses(type,city.country)` 주소 유형 및 각각에 대한 주소 도시가 있는 국가만 반환합니다. `addresses` 배열 요소입니다.
   * 위의 예는 와 같습니다. `addresses.type,addresses.city.country`.

>[!NOTE]
>
>점 표기법과 괄호 표기법 모두 하위 필드를 참조할 수 있습니다. 그러나 점 표기법을 사용하는 것이 가장 좋습니다. 이는 보다 간결하고 필드 계층 구조를 더 잘 보여 주기 때문입니다.

* 선택기의 각 필드는 응답의 루트를 기준으로 지정됩니다.
   * 데이터가 리소스의 컬렉션인 경우 프로젝션은 리소스의 배열을 포함합니다.
   * 데이터가 단일 리소스인 경우 프로젝션에는 해당 리소스와 관련된 필드가 포함됩니다.
   * 선택한 필드가 배열이거나 배열의 일부인 경우 배열의 모든 요소에서 선택한 부분이 투영됩니다.

### 선택기 매개 변수의 예

다음 예제는 샘플을 보여 줍니다 `selector` 매개 변수 뒤에 매개 변수가 나타내는 구조화된 값이 옵니다.

**person.lastName**

다음을 반환합니다. `lastName` 의 하위 필드 `person` 요청된 리소스의 객체입니다.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**주소**

의 모든 요소를 반환합니다. `addresses` 배열입니다. 각 요소의 모든 필드는 포함하지만 다른 필드는 포함되지 않습니다.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName,address**

다음을 반환합니다. `person.lastName` 필드 및 `addresses` 배열입니다.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**addresses.city**

주소 배열의 모든 요소에 대해 도시 필드만 반환합니다.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>
>중첩된 필드가 반환될 때마다 투영에 바깥쪽 부모 개체가 포함됩니다. 상위 필드는 명시적으로 선택하지 않는 한 다른 하위 필드를 포함하지 않습니다.

**주소(유형, 도시)**

다음 값 반환: `type` 및 `city` 의 각 요소에 대한 필드 `addresses` 배열입니다. 각각에 포함된 다른 모든 하위 필드 `addresses` 요소가 필터링됩니다.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## 다음 단계

이 안내서에서는 올바른 형식 지정 방법을 포함하여 프로젝션과 대상을 구성하는 데 관련된 단계를 보여줍니다. `selector` 매개 변수. 이제 조직의 요구 사항에 맞는 새로운 투영 대상 및 구성을 생성할 수 있습니다.
