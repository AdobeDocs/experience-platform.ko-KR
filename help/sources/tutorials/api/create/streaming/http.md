---
keywords: Experience Platform;홈;인기 항목;스트리밍 연결;스트리밍 연결 만들기;api 안내서;자습서;스트리밍 연결 만들기;스트리밍 수집;섭취;
solution: Experience Platform
title: API를 사용하여 스트리밍 연결 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서는 Adobe Experience Platform 데이터 수집 서비스 API의 일부인 스트리밍 수집 API를 사용하는 데 도움이 됩니다.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 0ff93d580482f44954321089659bd2fc062f3f61
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 2%

---


# API를 사용하여 스트리밍 연결 만들기

Flow Service는 Adobe Experience Platform 내의 다양한 종류의 소스로부터 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 Flow Service API를 사용하여 스트리밍 연결을 만드는 단계를 안내합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md): 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크입니다.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.

또한 스트리밍 연결을 만들려면 대상 XDM 스키마와 데이터 세트가 있어야 합니다. 이러한 내용을 만드는 방법을 알아보려면 [스트리밍 레코드 데이터](../../../../../ingestion/tutorials/streaming-record-data.md)에서 자습서를 읽어보거나 [스트리밍 시계열 데이터](../../../../../ingestion/tutorials/streaming-time-series-data.md)에서 자습서를 읽어보십시오.

다음 섹션에서는 스트리밍 수집 API를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

- 권한 부여: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../../../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## 기본 연결 만들기

기본 연결은 소스를 지정하고 플로우가 수집 API와 호환되도록 하는 데 필요한 정보를 포함합니다. 기본 연결을 만들 때 인증되지 않은 연결 및 인증된 연결을 만들 수 있습니다.

### 인증되지 않은 연결

인증되지 않은 연결은 데이터를 플랫폼으로 스트리밍할 때 만들 수 있는 표준 스트리밍 연결입니다.

**API 형식**

```http
POST /flowservice/connections
```

**요청**

스트리밍 연결을 만들려면 POST 요청의 일부로 공급자 ID 및 연결 사양 ID를 제공해야 합니다. 공급자 ID는 `521eee4d-8cbe-4906-bb48-fb6bd4450033`이고 연결 사양 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`입니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.sourceId` | 만들 스트리밍 연결의 ID입니다. |
| `auth.params.dataType` | 스트리밍 연결에 대한 데이터 유형입니다. 이 값은 `xdm`이어야 합니다. |
| `auth.params.name` | 만들 스트리밍 연결의 이름입니다. |
| `connectionSpec.id` | 스트리밍 연결을 위한 연결 사양 `id`입니다. |

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 연결의 `id`. 이를 `{CONNECTION_ID}`이라고 합니다. |
| `etag` | 연결의 개정을 지정하는 연결에 지정된 식별자입니다. |

### 인증된 연결

인증된 연결은 신뢰할 수 있는 원본과 신뢰할 수 없는 원본에서 들어오는 레코드를 구분해야 할 때 사용해야 합니다. PII(개인 식별 정보)로 정보를 전송하려는 사용자는 플랫폼에 정보를 스트리밍할 때 인증된 연결을 만들어야 합니다.

**API 형식**

```http
POST /flowservice/connections
```

**요청**

스트리밍 연결을 만들려면 POST 요청의 일부로 공급자 ID 및 연결 사양 ID를 제공해야 합니다. 공급자 ID는 `521eee4d-8cbe-4906-bb48-fb6bd4450033`이고 연결 사양 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`입니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.sourceId` | 만들 스트리밍 연결의 ID입니다. |
| `auth.params.dataType` | 스트리밍 연결에 대한 데이터 유형입니다. 이 값은 `xdm`이어야 합니다. |
| `auth.params.name` | 만들 스트리밍 연결의 이름입니다. |
| `auth.params.authenticationRequired` | 생성된 스트리밍 연결을 지정하는 매개 변수입니다 |
| `connectionSpec.id` | 스트리밍 연결을 위한 연결 사양 `id`입니다. |

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 연결의 `id`. 이를 `{CONNECTION_ID}`이라고 합니다. |
| `etag` | 연결의 개정을 지정하는 연결에 지정된 식별자입니다. |

## 스트리밍 끝점 URL 가져오기

만든 기본 연결로 이제 스트리밍 끝점 URL을 검색할 수 있습니다.

**API 형식**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 연결의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 요청된 연결에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다. 스트리밍 끝점 URL은 연결을 사용하여 자동으로 만들어지며, `inletUrl` 값을 사용하여 검색할 수 있습니다.

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## 소스 연결 만들기

기본 연결을 만든 후 소스 연결을 만들어야 합니다. 소스 연결을 만들 때 생성된 기본 연결에서 `id` 값이 필요합니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    }
}'
```

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 소스 연결에 대한 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## 대상 연결 만들기

대상 연결은 수집된 데이터가 들어오는 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크와 연결된 고정 연결 사양 ID를 제공해야 합니다. 이 연결 사양 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`

이제 대상 스키마에서 대상 데이터 세트와 데이터 레이크에 대한 연결 사양 ID의 고유 식별자가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 소스 데이터가 포함될 데이터 세트를 지정할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**응답**

성공적인 응답은 해당 고유 식별자(`id`)를 포함하여 새로 생성된 대상 연결의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## 데이터 흐름 만들기

이제 소스 및 타겟 연결을 만들어 데이터 흐름을 만들 수 있습니다. 데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. `/flows` 종단점에 대한 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 데이터 흐름의 세부 정보와 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## 다음 단계

이 자습서에 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 데이터를 플랫폼으로 수집할 수 있습니다. UI에서 스트리밍 연결을 만드는 방법에 대한 지침은 [스트리밍 연결 자습서 만들기](../../../ui/create/streaming/http.md)를 참조하십시오.

데이터를 Platform으로 스트리밍하는 방법을 배우려면 [스트리밍 시계열 데이터](../../../../../ingestion/tutorials/streaming-time-series-data.md)에서 자습서를 읽어보거나 [스트리밍 레코드 데이터](../../../../../ingestion/tutorials/streaming-record-data.md)에서 자습서를 읽어보십시오.

## 부록

이 섹션에서는 API를 사용하여 스트리밍 연결을 만드는 방법에 대한 추가 정보를 제공합니다.

### 인증된 스트리밍 연결로 메시지 보내기

스트리밍 연결에 인증이 활성화되면 클라이언트가 해당 요청에 `Authorization` 헤더를 추가해야 합니다.

`Authorization` 헤더가 없거나 유효하지 않거나 만료된 액세스 토큰이 전송된 경우 다음과 유사한 응답이 있는 HTTP 401 Unauthorized 응답이 반환됩니다.

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

### Platform에 수집할 원시 데이터 게시 {#ingest-data}

이제 플로우를 만들었으므로 이전에 만든 스트리밍 엔드포인트로 JSON 메시지를 보낼 수 있습니다.

**API 형식**

```http
POST /collection/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 새로 만든 스트리밍 연결의 `id` 값입니다. |

**요청**

이 예제 요청은 이전에 만든 스트리밍 종단점에 원시 데이터를 수집합니다.

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
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

**응답**

성공적인 응답은 새로 수집된 정보의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 이전에 만든 스트리밍 연결의 ID입니다. |
| `xactionId` | 방금 보낸 레코드에 대해 서버 측에서 생성된 고유 식별자입니다. 이 ID는 Adobe이 다양한 시스템과 디버깅을 통해 이 레코드의 라이프사이클을 추적하는 데 도움이 됩니다. |
| `receivedTimeMs` | 요청을 받은 시간을 보여주는 타임스탬프(밀리초 단위)입니다. |
