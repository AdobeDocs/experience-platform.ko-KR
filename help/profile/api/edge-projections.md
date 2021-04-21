---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 가장자리 투영 API 끝점
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform을 사용하면 변경 사항이 발생하면 즉시 올바른 데이터를 사용할 수 있고 지속적으로 업데이트하여 다양한 채널에서 고객에게 개인화되고 일관된 경험을 실시간으로 제공할 수 있습니다. 이러한 작업은 데이터를 저장하고 응용 프로그램에서 쉽게 액세스할 수 있도록 지리적으로 배치된 서버인 Edge를 사용하여 수행됩니다.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 2%

---

# 가장자리 투영 구성 및 대상 끝점

여러 채널에서 실시간으로 고객에게 일관되고 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 적합한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe Experience Platform을 사용하면 가장자리라고 하는 요소를 사용하여 데이터에 실시간으로 액세스할 수 있습니다. Edge는 데이터를 저장하고 응용 프로그램에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 예를 들어 Adobe Target 및 Adobe Campaign과 같은 Adobe 애플리케이션은 실시간으로 개인화된 고객 경험을 제공하기 위해 가장자리를 사용합니다. 데이터는 투영에 의해 모서리로 라우팅되고, 투영 대상은 데이터를 보낼 가장자리를 정의하고 가장자리에서 사용할 특정 정보를 정의하는 투영 구성이 있습니다. 이 안내서에서는 대상 및 구성을 포함하여 에지 예상 작업에 [!DNL Real-time Customer Profile] API를 사용하는 방법에 대한 자세한 지침을 제공합니다.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

>[!NOTE]
>
>페이로드(POST, PUT, PATCH)을 포함하는 요청에는 `Content-Type` 헤더가 필요합니다. 이 문서에 두 개 이상의 `Content-Type`이(가) 사용됩니다. 각 요청에 대해 올바른 `Content-Type`을(를) 사용하고 있는지 확인하려면 샘플 호출의 헤더에 특히 주의하십시오.

## 투영 대상

데이터를 보낼 위치를 지정하여 프로젝션을 하나 이상의 모서리로 라우팅할 수 있습니다. 만들어진 각 투영 대상에는 고유한 ID가 있으며 이 ID를 사용하여 투영 구성을 생성합니다.

### 모든 대상 나열

`/config/destinations` 종단점에 GET 요청을 함으로써 조직에 대해 이미 만들어진 에지 대상을 나열할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 배열 내에 개별 개체로 표시된 각 대상에 대한 세부 정보가 있는 `projectionDestinations` 배열이 포함됩니다. 예상 구성이 구성되지 않은 경우 `projectionDestinations` 배열은 빈 공간을 반환합니다.

>[!NOTE]
>
>이 응답은 공간에 대해 단축되었으며 두 개의 대상만 표시합니다.

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
| `_links.self.href` | 최상위 수준에서, GET 요청을 수행하는 데 사용된 경로와 일치합니다. 각 개별 대상 개체 내에서 이 경로를 GET 요청에서 사용하여 특정 대상의 세부 사항을 직접 조회할 수 있습니다. |
| `id` | 각 대상 개체 내에서 `"id"`은 대상에 대한 읽기 전용 시스템 생성 고유 ID를 표시합니다. 이 ID는 특정 대상을 참조하거나 투영 구성을 생성할 때 사용됩니다. |

개별 대상의 특성에 대한 자세한 내용은 다음에 나오는 [대상](#create-a-destination)을 만드는 섹션을 참조하십시오.

### 대상 {#create-a-destination} 만들기

필요한 대상이 아직 없는 경우 `/config/destinations` 끝점에 POST 요청을 하여 새 투영 대상을 만들 수 있습니다.

**API 형식**

```http
POST /config/destinations
```

**요청**

다음 요청은 새 에지 대상을 만듭니다.

>[!NOTE]
>
>대상을 만들기 위한 POST 요청에는 아래와 같이 특정 `Content-Type` 헤더가 필요합니다. 잘못된 `Content-Type` 헤더를 사용하면 HTTP 상태 415(지원되지 않는 미디어 유형) 오류가 발생합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `type` **(필수 여부)** | 만들 대상 유형입니다. 유일하게 허용되는 값 &quot;EDGE&quot;는 가장자리 대상을 만듭니다. |
| `dataCenters` **(필수 여부)** | 경로설정될 투영의 가장자리를 나열하는 문자열 배열입니다. 다음 값 중 하나 이상을 포함할 수 있습니다.&quot;OR1&quot; - 미국 서부, &quot;VA5&quot; - 미국 동부, &quot;NLD1&quot; - EMEA. |
| `ttl` **(필수 여부)** | 투영 만료일을 지정합니다. 허용된 값 범위:600~604800. 기본값:3600. |
| `replicationPolicy` **(필수 여부)** | 허브에서 가장자리까지의 데이터 복제 동작을 정의합니다.  지원되는 값:사전 대처, 사후 대응 기본값:반응형 |

**응답**

성공적으로 응답하면 시스템이 생성한 읽기 전용 고유 ID(`id`)를 포함하여 새로 만든 가장자리 대상의 세부 정보를 반환합니다.

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
| `id` | 대상에 대한 읽기 전용 시스템 생성 고유 ID. 이 ID는 대상을 직접 참조하거나 투영 구성을 생성할 때 사용됩니다. |
| `version` | 이 읽기 전용 값은 대상의 현재 버전을 보여 줍니다. 대상이 업데이트되면 버전 번호가 자동으로 증가합니다. |

### 대상 보기

투영 대상의 고유 ID를 알고 있는 경우 조회 요청을 수행하여 세부 사항을 볼 수 있습니다. 이 작업은 요청 경로에서 대상의 ID를 포함하여 `/config/destinations` 끝점에 GET 요청을 함으로써 수행됩니다.

**API 형식**

```http
GET /config/destinations/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DESTINATION_ID}` | 보려는 투영 대상의 고유 ID입니다. |

**요청**

다음 요청은 요청 경로에 제공된 ID의 대상을 보기 위해 조회(GET)을 수행합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 객체에는 투영 대상의 세부 사항이 표시됩니다. `id` 속성은 요청에 제공된 투영 대상의 ID와 일치해야 합니다.

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

기존 대상은 요청 경로에서 업데이트할 대상의 ID를 포함하여 `/config/destinations` 끝점에 PUT 요청을 함으로써 업데이트할 수 있습니다. 이 작업은 기본적으로 대상을 다시 작성하고 있으므로 새 대상을 만들 때 제공된 것처럼 요청의 본문에 동일한 특성을 제공해야 합니다.

>[!CAUTION]
>
>업데이트 요청에 대한 API 응답은 즉시 적용되지만 예상치에 대한 변경 사항은 비동기적으로 적용됩니다. 즉, 대상 정의에 대한 업데이트를 수행한 시점과 대상을 적용한 시점은 서로 다릅니다.

**API 형식**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DESTINATION_ID}` | 업데이트할 투영 대상의 고유 ID입니다. |

**요청**

다음 요청은 두 번째 위치(`dataCenters`)를 포함하도록 기존 대상을 업데이트합니다.

>[!IMPORTANT]
>
>PUT 요청에는 아래와 같이 특정 `Content-Type` 헤더가 필요합니다. 잘못된 `Content-Type` 헤더를 사용하면 HTTP 상태 415(지원되지 않는 미디어 유형) 오류가 발생합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `currentVersion` | 기존 대상의 현재 버전입니다. 대상에 대한 조회 요청을 수행할 때 `version` 속성의 값입니다. |

**응답**

응답에는 대상의 ID 및 대상의 새 `version`을 포함하여 대상에 대한 업데이트된 세부 정보가 포함됩니다.

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

조직에서 더 이상 투영 대상을 필요로 하지 않는 경우 DELETE 요청을 `/config/destinations` 끝점과 요청 경로에서 삭제하려는 대상의 ID를 포함하여 삭제할 수 있습니다.

>[!CAUTION]
>
>삭제 요청에 대한 API 응답은 즉시 적용되지만 가장자리의 데이터에 대한 실제 변경 사항은 비동기적으로 발생합니다. 즉, 프로파일 데이터는 모든 가장자리(투영 대상에 지정된 `dataCenters`)에서 제거되지만 프로세스는 완료하는 데 시간이 걸립니다.

**API 형식**

```http
DELETE /config/destinations/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DESTINATION_ID}` | 삭제할 투영 대상의 고유 ID입니다. |


**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

삭제 요청은 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문을 반환합니다. ID로 대상에 대한 조회 요청을 수행하여 삭제에 성공했는지 확인할 수 있습니다. 조회는 HTTP 상태 404(찾을 수 없음)를 반환해야 합니다.

## 투영 구성

투영 구성은 각 가장자리에서 사용할 수 있는 데이터에 대한 정보를 제공합니다. 전체 [!DNL Experience Data Model](XDM) 스키마를 가장자리에 투영하는 대신 투영에서는 스키마의 특정 데이터 또는 필드만 제공합니다. 조직은 각 XDM 스키마에 대해 두 개 이상의 프로젝션 구성을 정의할 수 있습니다.

### 모든 투영 구성 나열

`/config/projections` 종단점에 GET 요청을 하여 조직에 대해 만들어진 모든 프로젝션 구성을 나열할 수 있습니다. 요청 경로에 선택적 매개변수를 추가하여 특정 스키마에 대한 프로젝션 구성에 액세스하거나 이름으로 개별 투영을 조회할 수도 있습니다.

**API 형식**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| 매개 변수 | 설명 |
|---|---|
| `{SCHEMA_NAME}` | 액세스하려는 프로젝션 구성과 연결된 스키마 클래스의 이름입니다. |
| `{PROJECTION_NAME}` | 액세스하려는 프로젝션 구성의 이름입니다. |

>[!NOTE]
>
>`schemaName` 는  `name` 스키마 클래스 컨텍스트에서만 투영 구성 이름이 고유하므로 매개 변수를 사용할 때 필요합니다.

**요청**

다음 요청은 [!DNL Experience Data Model] 스키마 클래스 [!DNL XDM Individual Profile]와 연관된 모든 프로젝션 구성을 나열합니다. [!DNL Platform] 내의 XDM 및 해당 역할에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 읽어 보십시오.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `projectionConfigs` 배열 내에 포함된 루트 `_embedded` 특성 내의 프로젝션 구성 목록을 반환합니다. 조직에 대해 투영 구성이 없는 경우 `projectionConfigs` 배열은 비어 있게 됩니다.

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

모서리에서 사용할 수 있는 XDM 필드를 지정하는 새 투영 구성을 생성(POST)할 수 있습니다.

**API 형식**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| 매개 변수 | 설명 |
|---|---|
| `{SCHEMA_NAME}` | 액세스하려는 프로젝션 구성과 연결된 스키마 클래스의 이름입니다. |

**요청**

>[!NOTE]
>
>구성을 만들기 위한 POST 요청에는 아래와 같이 특정 `Content-Type` 헤더가 필요합니다. 잘못된 `Content-Type` 헤더를 사용하면 HTTP 상태 415(지원되지 않는 미디어 유형) 오류가 발생합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `selector` | 가장자리에 복제할 스키마 내의 속성 목록을 포함하는 문자열입니다. 선택기 작업에 대한 우수 사례는 이 문서의 [선택기](#selectors) 섹션에서 사용할 수 있습니다. |
| `name` | 새 투영 구성의 설명형 이름입니다. |
| `destinationId` | 데이터가 투영될 에지 대상의 식별자입니다. |

**응답**

성공적인 응답은 새로 생성된 투영 구성의 세부 정보를 반환합니다.

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

선택기는 XDM 필드 이름의 쉼표로 구분된 목록입니다. 투영 구성에서 선택기는 투영에 포함할 속성을 지정합니다. `selector` 매개 변수 값의 형식은 XPath 구문에 따라 느슨하게 설정됩니다. 지원되는 구문은 아래에 요약되어 있으며 참조할 수 있도록 추가 예가 제공됩니다.

### 지원되는 구문

* 여러 필드를 선택하려면 쉼표를 사용합니다. 공백은 사용하지 마십시오.
* 도트 표기법을 사용하여 중첩된 필드를 선택합니다.
   * 예를 들어 `foo` 필드에 중첩된 `field`이라는 필드를 선택하려면 `foo.field` 선택기를 사용합니다.
* 하위 필드가 포함된 필드를 포함하면 모든 하위 필드도 기본적으로 투영됩니다. 그러나 괄호 `"( )"`를 사용하여 반환되는 하위 필드를 필터링할 수 있습니다.
   * 예를 들어 `addresses(type,city.country)`은 각 `addresses` 배열 요소에 대해 주소 유형과 주소 도시 위치의 국가만 반환합니다.
   * 위의 예는 `addresses.type,addresses.city.country`에 해당합니다.

>[!NOTE]
>
>하위 필드를 참조하기 위해 도트 표기법과 괄호 표기법 모두 지원됩니다. 그러나 보다 간결하고 필드 계층 구조를 더 잘 보여 주기 때문에 도트 표기법을 사용하는 것이 좋습니다.

* 선택기의 각 필드는 응답의 루트를 기준으로 지정됩니다.
   * 데이터가 리소스 컬렉션인 경우 프로젝트에는 리소스 배열이 포함됩니다.
   * 데이터가 단일 리소스인 경우 프로젝트에는 해당 리소스를 기준으로 하는 필드가 포함됩니다.
   * 선택한 필드가 배열의 일부이거나 배열인 경우 투영에는 배열에 있는 모든 요소의 선택된 부분이 포함됩니다.

### 선택기 매개 변수의 예

다음 예는 샘플 `selector` 매개 변수와 해당 매개 변수가 나타내는 구조적 값을 보여 줍니다.

**person.lastName**

요청된 리소스에 있는 `person` 개체의 `lastName` 하위 필드를 반환합니다.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**주소**

각 요소의 모든 필드를 포함하여 `addresses` 배열의 모든 요소를 반환하지만 다른 필드는 반환합니다.

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

**person.lastName,주소**

`person.lastName` 필드와 `addresses` 배열의 모든 요소를 반환합니다.

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

**address.city**

주소 배열의 모든 요소에 대한 구/군/시 필드만 반환합니다.

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
>중첩 필드를 반환할 때마다 프로젝트에는 바깥쪽 상위 객체가 포함됩니다. 상위 필드는 명시적으로 선택되어 있지 않으면 다른 하위 필드를 포함하지 않습니다.

**address(type,city)**

`addresses` 배열의 각 요소에 대한 `type` 및 `city` 필드의 값만 반환합니다. 각 `addresses` 요소에 포함된 다른 모든 하위 필드는 필터링됩니다.

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

이 안내서에서는 `selector` 매개 변수의 형식을 제대로 지정하는 방법을 포함하여 예상 및 대상을 구성하는 데 관련된 단계를 보여 줍니다. 이제 조직의 요구 사항에 맞는 새로운 투영 대상 및 구성을 만들 수 있습니다.
