---
keywords: Experience Platform;홈;인기 항목;스트리밍 연결;스트리밍 연결 만들기;api 안내서;자습서;스트리밍 연결 만들기;스트리밍 수집;섭취;
title: Flow Service API를 사용하여 HTTP API 스트리밍 연결 만들기
description: 이 자습서에서는 Flow Service API를 사용하여 원시 및 XDM 데이터에 대한 HTTP API 소스를 사용하여 스트리밍 연결을 만드는 방법을 제공합니다
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 2b3f8b7b0a19214a95a2ad76c9fecd70ffd91743
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 2%

---


# 를 사용하여 HTTP API 스트리밍 연결을 만듭니다 [!DNL Flow Service] API

흐름 서비스는 Adobe Experience Platform 내의 다른 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 를 사용하여 스트리밍 연결을 만드는 단계를 살펴보려면 [!DNL Flow Service] API.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 경험 데이터를 구성합니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.

또한 스트리밍 연결을 만들려면 대상 XDM 스키마와 데이터 세트가 있어야 합니다. 이러한 단원을 만드는 방법을 알아보려면 [스트리밍 레코드 데이터](../../../../../ingestion/tutorials/streaming-record-data.md) 또는 [스트리밍 시계열 데이터](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 기본 연결 만들기

기본 연결은 소스를 지정하고 플로우가 수집 API와 호환되도록 하는 데 필요한 정보를 포함합니다. 기본 연결을 만들 때 인증되지 않은 연결 및 인증된 연결을 만들 수 있습니다.

### 인증되지 않은 연결

인증되지 않은 연결은 데이터를 플랫폼으로 스트리밍할 때 만들 수 있는 표준 스트리밍 연결입니다.

인증되지 않은 기본 연결을 만들려면 `/connections` 끝점입니다. 이 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**API 형식**

```http
POST /flowservice/connections
```

**요청**

다음 요청은 HTTP API에 대한 기본 연결을 만듭니다.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB 원시 데이터]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | HTTP API에 해당하는 연결 사양 ID입니다. 이 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | 스트리밍 연결에 대한 데이터 유형입니다. 지원되는 값은 다음과 같습니다. `xdm` 및 `raw`. |
| `auth.params.name` | 만들 스트리밍 연결의 이름입니다. |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 만든 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 다음 `id` 새로 만든 기본 연결 |
| `etag` | 기본 연결의 버전을 지정하여 연결에 지정된 식별자입니다. |

### 인증된 연결

인증된 연결은 신뢰할 수 있는 원본과 신뢰할 수 없는 원본에서 들어오는 레코드를 구분해야 할 때 사용해야 합니다. PII(개인 식별 정보)로 정보를 전송하려는 사용자는 플랫폼에 정보를 스트리밍할 때 인증된 연결을 만들어야 합니다.

인증된 기본 연결을 만들려면 다음을 포함해야 합니다 `authenticationRequired` 매개 변수 를 요청에 지정하고 해당 값을 로 지정합니다. `true`. 이 단계에서는 인증된 기본 연결에 대한 소스 ID를 제공할 수도 있습니다. 이 매개 변수는 선택 사항이며 와 동일한 값을 사용합니다 `name` 속성을 지정해야 합니다.


**API 형식**

```http
POST /flowservice/connections
```

**요청**

다음 요청은 HTTP API에 대한 인증된 기본 연결을 만듭니다.

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB 원시 데이터]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.sourceId` | 인증된 기본 연결을 만들 때 사용할 수 있는 추가 식별자입니다. 이 매개 변수는 선택 사항이며 와 동일한 값을 사용합니다 `name` 속성을 지정해야 합니다. |
| `auth.params.authenticationRequired` | 생성된 스트리밍 연결을 지정하는 매개 변수입니다 |

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 만든 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다`id`).

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## 스트리밍 끝점 URL 가져오기

만든 기본 연결로 이제 스트리밍 끝점 URL을 검색할 수 있습니다.

**API 형식**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 다음 `id` 이전에 만든 연결의 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 연결에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다. 스트리밍 끝점 URL은 연결을 통해 자동으로 만들어지며, `inletUrl` 값.

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## 소스 연결 만들기 {#source}

소스 연결을 만들려면 `/sourceConnections` 기본 연결 ID를 제공하는 동안 끝점입니다.

**API 형식**

```http
POST /flowservice/sourceConnections
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 만든 소스 연결에 대해 자세히 설명된 HTTP 상태 201을 반환합니다`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

Platform에서 소스 데이터를 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

대상 XDM 스키마는에 대한 POST 요청을 수행하여 만들 수 있습니다 [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [api를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md).

### 대상 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 대상 데이터 세트를 만들 수 있습니다 [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공하는 것이 좋습니다.

대상 데이터 세트를 만드는 방법에 대한 자세한 단계는 다음 사항에 대한 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../../../catalog/api/create-dataset.md).

## 대상 연결 만들기 {#target}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. Target 연결을 만들려면 다음 POST을 요청합니다. `/targetConnections` target 데이터 세트 및 target XDM 스키마에 대한 ID를 제공하는 동안. 이 단계에서는 데이터 레이크 연결 사양 ID도 제공해야 합니다. 이 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API 형식**

```http
POST /flowservice/targetConnections
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**응답**

성공적인 응답은 고유 식별자( )를 포함하여 새로 만든 대상 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다`id`).

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 세트에 수집하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다.

매핑 세트를 만들려면, `mappingSets` 의 끝점 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) target XDM 스키마를 제공하는 동안 `$id` 생성하려는 매핑 세트의 세부 정보를 표시합니다.

**API 형식**

```http
POST /mappingSets
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `xdmSchema` | 다음 `$id` 대상 XDM 스키마 중 하나입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`). 이 ID는 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

| 속성 | 설명 |
| --- | --- |

## 데이터 흐름 만들기

이제 소스 및 타겟 연결을 만들어 데이터 흐름을 만들 수 있습니다. 데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 에 대한 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다 `/flows` 엔드포인트.

**API 형식**

```http
POST /flows
```

**요청**

>[!BEGINTABS]

>[!TAB 변형 없이]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB 변형 사용]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| 속성 | 설명 |
| --- | --- |
| `name` | 데이터 흐름의 이름입니다. 데이터 흐름에서 정보를 조회하는 데 사용할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인합니다. |
| `description` | (선택 사항) 데이터 집합에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `flowSpec.id` | 흐름 사양 ID [!DNL HTTP API]. 변형을 사용하여 데이터 흐름을 만들려면  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. 변형 없이 데이터 흐름을 만들려면 `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source) 이전 단계에서 검색됨. |
| `targetConnectionIds` | 다음 [target 연결 ID](#target) 이전 단계에서 검색됨. |
| `transformations.params.mappingId` | 다음 [매핑 ID](#mapping) 이전 단계에서 검색됨. |

**응답**

성공적으로 응답하면 고유 식별자( )를 포함하여 새로 만든 데이터 흐름의 세부 정보와 함께 HTTP 상태 201을 반환합니다`id`).

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```


## Platform에 수집할 데이터 게시 {#ingest-data}

이제 플로우를 만들었으므로 이전에 만든 스트리밍 엔드포인트로 JSON 메시지를 보낼 수 있습니다.

**API 형식**

```http
POST /collection/{INLET_URL}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{INLET_URL}` | 스트리밍 끝점 URL입니다. 에 GET 요청을 작성하여 이 URL을 검색할 수 있습니다 `/connections` 기본 연결 ID를 제공하는 동안 끝점입니다. |

**요청**

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB 원시 데이터]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!ENDTABS]

**응답**

성공적인 응답은 새로 수집된 정보의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 ID입니다. |
| `xactionId` | 방금 보낸 레코드에 대해 서버 측에서 생성된 고유 식별자입니다. 이 ID는 Adobe이 다양한 시스템과 디버깅을 통해 이 레코드의 라이프사이클을 추적하는 데 도움이 됩니다. |
| `receivedTimeMs` | 요청을 받은 시간을 보여주는 타임스탬프(밀리초 단위)입니다. |


## 다음 단계

이 자습서에 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 데이터를 플랫폼으로 수집할 수 있습니다. UI에서 스트리밍 연결을 만드는 지침은 [스트리밍 연결 만들기 자습서](../../../ui/create/streaming/http.md).

데이터를 Platform으로 스트리밍하는 방법에 대해 알아보려면 다음 자습서를 참조하십시오. [스트리밍 시계열 데이터](../../../../../ingestion/tutorials/streaming-time-series-data.md) 또는 [스트리밍 레코드 데이터](../../../../../ingestion/tutorials/streaming-record-data.md).

## 부록

이 섹션에서는 API를 사용하여 스트리밍 연결을 만드는 방법에 대한 추가 정보를 제공합니다.

### 인증된 스트리밍 연결로 메시지 보내기

스트리밍 연결에 인증이 활성화되면 클라이언트를 `Authorization` 헤더 를 추가합니다.

만약 `Authorization` 헤더가 없거나 유효하지 않거나 만료된 액세스 토큰이 전송되면 HTTP 401 Unauthorized 응답이 아래와 같이 반환됩니다.

**응답**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
