---
keywords: Experience Platform;홈;인기 항목;스트리밍 연결;스트리밍 연결 만들기;api 안내서;자습서;스트리밍 연결 만들기;스트리밍 수집;수집;
title: 흐름 서비스 API를 사용하여 HTTP API 스트리밍 연결 만들기
description: 이 자습서에서는 흐름 서비스 API를 사용하여 원시 데이터와 XDM 데이터 모두에 대해 HTTP API 소스를 사용하여 스트리밍 연결을 만드는 방법에 대한 단계를 제공합니다
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 3%

---


# [!DNL Flow Service] API를 사용하여 HTTP API 스트리밍 연결 만들기

플로우 서비스는 Adobe Experience Platform 내의 다양한 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결 가능한 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Flow Service] API를 사용하여 스트리밍 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): [!DNL Platform]에서 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본에서 집계한 데이터를 기반으로 통합 소비자 프로필을 실시간으로 제공합니다.

또한 스트리밍 연결을 만들려면 타겟 XDM 스키마와 데이터 세트가 있어야 합니다. 이러한 데이터를 만드는 방법에 대해 알아보려면 [레코드 데이터 스트리밍](../../../../../ingestion/tutorials/streaming-record-data.md)에 대한 자습서 또는 [시계열 데이터 스트리밍](../../../../../ingestion/tutorials/streaming-time-series-data.md)에 대한 자습서를 참조하십시오.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

기본 연결은 소스를 지정하고 흐름이 스트리밍 수집 API와 호환되도록 하는 데 필요한 정보를 포함합니다. 기본 연결을 만들 때 인증되지 않은 연결과 인증된 연결을 만들 수 있는 옵션이 있습니다.

### 인증되지 않은 연결

인증되지 않은 연결은 데이터를 플랫폼으로 스트리밍할 때 만들 수 있는 표준 스트리밍 연결입니다.

인증되지 않은 기본 연결을 만들려면 연결 이름, 데이터 형식 및 HTTP API 연결 사양 ID를 제공하는 동안 `/connections` 끝점에 POST 요청을 합니다. 이 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`입니다.

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
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 이름이 설명적인지 확인하십시오. |
| `description` | (선택 사항) 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `connectionSpec.id` | HTTP API에 해당하는 연결 사양 ID입니다. 이 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`입니다. |
| `auth.params.dataType` | 스트리밍 연결에 대한 데이터 유형입니다. 지원되는 값은 `xdm` 및 `raw`입니다. |
| `auth.params.name` | 만들려는 스트리밍 연결의 이름입니다. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 생성된 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 기본 연결의 `id`입니다. |
| `etag` | 연결에 할당된 식별자로, 기본 연결의 버전을 지정합니다. |

### 인증된 연결

인증된 연결은 신뢰할 수 있는 원본과 신뢰할 수 없는 원본에서 오는 레코드를 구별해야 할 때 사용해야 합니다. PII(개인 식별 정보)가 있는 정보를 전송하려는 사용자는 Platform으로 정보를 스트리밍할 때 인증된 연결을 만들어야 합니다.

인증된 기본 연결을 만들려면 요청에 `authenticationRequired` 매개 변수를 포함하고 해당 값을 `true`(으)로 지정해야 합니다. 이 단계에서는 인증된 기본 연결에 대한 소스 ID를 제공할 수도 있습니다. 이 매개 변수는 선택 사항이며, 지정하지 않을 경우 `name` 특성과 동일한 값을 사용합니다.


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
| `auth.params.sourceId` | 인증된 기본 연결을 만들 때 사용할 수 있는 추가 식별자입니다. 이 매개 변수는 선택 사항이며, 지정하지 않을 경우 `name` 특성과 동일한 값을 사용합니다. |
| `auth.params.authenticationRequired` | 이 매개 변수는 스트리밍 연결에 인증이 필요한지 여부를 지정합니다. `authenticationRequired`이(가) `true`(으)로 설정된 경우 스트리밍 연결에 대한 인증을 제공해야 합니다. `authenticationRequired`이(가) `false`(으)로 설정된 경우 인증이 필요하지 않습니다. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 생성된 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## 스트리밍 끝점 URL 가져오기

기본 연결이 만들어지면 스트리밍 끝점 URL을 검색할 수 있습니다.

**API 형식**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전에 만든 연결의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 연결에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다. 스트리밍 끝점 URL은 연결을 통해 자동으로 만들어지며 `inletUrl` 값을 사용하여 검색할 수 있습니다.

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

원본 연결을 만들려면 기본 연결 ID를 제공하는 동안 `/sourceConnections` 끝점에 대한 POST 요청을 만듭니다.

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

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 생성된 소스 연결에 대한 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

[스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다.

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md)에 대한 자습서를 참조하십시오.

### 타겟 데이터 세트 만들기 {#target-dataset}

[카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 수행하고 페이로드 내에 대상 스키마의 ID를 제공하여 대상 데이터 집합을 만들 수 있습니다.

대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오.

## 대상 연결 만들기 {#target}

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 대상 데이터 세트 및 대상 XDM 스키마에 대한 ID를 제공하는 동안 `/targetConnections`에 POST 요청을 하십시오. 이 단계에서 데이터 레이크 연결 사양 ID도 제공해야 합니다. 이 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다.

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

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 생성된 대상 연결에 대한 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다.

매핑 세트를 만들려면 대상 XDM 스키마 `$id`과(와) 만들려는 매핑 세트의 세부 정보를 제공하는 동안 [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)의 `mappingSets` 끝점에 POST 요청을 하십시오.

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
| `xdmSchema` | 대상 XDM 스키마의 `$id`. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

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

## 데이터 흐름 만들기

이제 소스 및 타겟 연결이 만들어지면 데이터 흐름을 만들 수 있습니다. 데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. `/flows` 끝점에 대한 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

**API 형식**

```http
POST /flows
```

**요청**

>[!BEGINTABS]

>[!TAB XDM]

다음 요청은 XDM 데이터에 대한 스트리밍 데이터 흐름을 만듭니다.

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

>[!TAB 원시]

다음 요청은 원시 데이터에 대한 스트리밍 데이터 흐름을 만듭니다.

변환을 사용하여 데이터 흐름을 만들 때 `name` 매개 변수를 변경할 수 없습니다. 이 값은 항상 `Mapping`(으)로 설정해야 합니다.

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
| `name` | 데이터 흐름의 이름입니다. 이 옵션을 사용하여 데이터 흐름에서 정보를 조회할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인하십시오. |
| `description` | (선택 사항) 데이터 흐름에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 속성입니다. |
| `flowSpec.id` | [!DNL HTTP API]에 대한 흐름 사양 ID입니다. 변환을 사용하여 데이터 흐름을 만들려면 `c1a19761-d2c7-4702-b9fa-fe91f0613e81`을(를) 사용해야 합니다. 변환하지 않고 데이터 흐름을 만들려면 `d8a6f005-7eaf-4153-983e-e8574508b877`을(를) 사용합니다. |
| `sourceConnectionIds` | 이전 단계에서 [원본 연결 ID](#source)을(를) 검색했습니다. |
| `targetConnectionIds` | 이전 단계에서 [대상 연결 ID](#target)을(를) 검색했습니다. |
| `transformations.params.mappingId` | [매핑 ID](#mapping)이(가) 이전 단계에서 검색되었습니다. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 데이터 흐름의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## 플랫폼에 수집할 게시물 데이터 {#ingest-data}

>[!NOTE]
>
>데이터 흐름 생성과 스트리밍 데이터 수집 사이에 최소 ~5분의 지연을 추가해야 합니다. 이렇게 하면 데이터를 수집하기 전에 데이터 흐름을 완전히 활성화할 수 있습니다.

플로우를 만들었으므로 이제 이전에 만든 스트리밍 엔드포인트로 JSON 메시지를 보낼 수 있습니다.

**API 형식**

```http
POST /collection/{INLET_URL}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{INLET_URL}` | 스트리밍 끝점 URL. 기본 연결 ID를 제공하는 동안 `/connections` 끝점에 대한 GET 요청을 수행하여 이 URL을 검색할 수 있습니다. |
| `{FLOW_ID}` | HTTP API 스트리밍 데이터 흐름의 ID입니다. 이 ID는 XDM 및 RAW 데이터 모두에 필요합니다. |

**요청**

>[!BEGINTABS]

>[!TAB XDM 데이터 보내기]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
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

>[!TAB 흐름 ID가 있는 원시 데이터를 HTTP 헤더로 보내기]

원시 데이터를 전송할 때 흐름 ID를 쿼리 매개 변수 또는 HTTP 헤더의 일부로 지정할 수 있습니다. 다음 예제에서는 흐름 ID를 HTTP 헤더로 지정합니다.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
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

>[!TAB 흐름 ID를 쿼리 매개 변수로 사용하는 원시 데이터 보내기]

원시 데이터를 전송할 때 흐름 ID를 쿼리 매개 변수 또는 HTTP 헤더로 지정할 수 있습니다. 다음 예제에서는 흐름 ID를 쿼리 매개 변수로 지정합니다.

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
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
| `xactionId` | 방금 전송한 레코드에 대해 서버측에서 생성된 고유 식별자입니다. 이 ID는 Adobe이 다양한 시스템을 통해 디버깅을 사용하여 이 레코드의 라이프사이클을 추적하는 데 도움이 됩니다. |
| `receivedTimeMs` | 요청이 수신된 시간을 보여 주는 타임스탬프(시간(밀리초 단위))입니다. |


## 다음 단계

이 자습서에 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 데이터를 Platform에 수집할 수 있습니다. UI에서 스트리밍 연결을 만드는 방법에 대한 지침은 [스트리밍 연결 만들기 자습서](../../../ui/create/streaming/http.md)를 참조하십시오.

데이터를 플랫폼으로 스트리밍하는 방법에 대해 알아보려면 [시계열 데이터 스트리밍](../../../../../ingestion/tutorials/streaming-time-series-data.md)에 대한 자습서 또는 [레코드 데이터 스트리밍](../../../../../ingestion/tutorials/streaming-record-data.md)에 대한 자습서를 참조하십시오.

## 부록

이 섹션에서는 API를 사용하여 스트리밍 연결을 만드는 방법에 대한 보충 정보를 제공합니다.

### 인증된 스트리밍 연결에 메시지 보내기

스트리밍 연결에 인증을 사용하도록 설정한 경우 클라이언트가 요청에 `Authorization` 헤더를 추가해야 합니다.

`Authorization` 헤더가 없거나 유효하지 않거나 만료된 액세스 토큰이 전송된 경우 HTTP 401 Unauthorized 응답이 반환되고 다음과 유사한 응답이 표시됩니다.

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

