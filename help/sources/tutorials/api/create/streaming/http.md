---
keywords: Experience Platform;홈;인기 항목;스트리밍 연결;스트리밍 연결;api 안내서;자습서;스트리밍 연결;스트리밍 통합;통합;;home;popular topics;streaming connection;tutorial;streaming connection;streaming ingestion;inestion;
solution: Experience Platform
title: API를 사용하여 스트리밍 연결 만들기
topic-legacy: tutorial
type: Tutorial
description: 이 자습서는 Adobe Experience Platform 데이터 통합 서비스 API의 일부인 스트리밍 통합 API를 사용하는 데 도움이 됩니다.
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 2%

---


# API를 사용하여 스트리밍 연결 만들기

Flow Service는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 중앙에서 수집하고 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서는 [!DNL Flow Service] API를 사용하여 Flow Service API를 사용하여 스트리밍 연결을 만드는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 실시간으로 제공합니다.

다음 섹션에서는 스트리밍 통합 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../../../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 연결 만들기

연결은 소스를 지정하며 스트리밍 통합 API와 호환되는 흐름을 만드는 데 필요한 정보를 포함합니다. 연결을 만들 때 인증되지 않은 연결 및 인증된 연결을 만들 수 있습니다.

### 인증되지 않은 연결

인증되지 않은 연결은 데이터를 Platform(플랫폼)으로 스트리밍하고자 할 때 만들 수 있는 표준 스트리밍 연결입니다.

**API 형식**

```http
POST /flowservice/connections
```

**요청**

스트리밍 연결을 만들려면 공급자 ID 및 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. 공급자 ID는 `521eee4d-8cbe-4906-bb48-fb6bd4450033`이고 연결 사양 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`입니다.

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
 }
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.sourceId` | 만들려는 스트리밍 연결의 ID입니다. |
| `auth.params.dataType` | 스트리밍 연결에 대한 데이터 유형입니다. 이 값은 `xdm`이어야 합니다. |
| `auth.params.name` | 만들려는 스트리밍 연결의 이름입니다. |
| `connectionSpec.id` | 스트리밍 연결을 위한 연결 사양 `id`입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 사항과 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 연결의 `id`. 이것은 `{CONNECTION_ID}`이라고 합니다. |
| `etag` | 연결의 개정을 지정하는 연결에 할당된 식별자입니다. |

### 인증된 연결

인증된 연결은 신뢰할 수 있는 소스와 신뢰할 수 없는 소스에서 나오는 레코드를 구별해야 할 때 사용해야 합니다. PII(개인 식별 정보)로 정보를 전송하려는 사용자는 플랫폼에 정보를 스트리밍할 때 인증된 연결을 만들어야 합니다.

**API 형식**

```http
POST /flowservice/connections
```

**요청**

스트리밍 연결을 만들려면 공급자 ID 및 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. 공급자 ID는 `521eee4d-8cbe-4906-bb48-fb6bd4450033`이고 연결 사양 ID는 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`입니다.

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
| `auth.params.sourceId` | 만들려는 스트리밍 연결의 ID입니다. |
| `auth.params.dataType` | 스트리밍 연결에 대한 데이터 유형입니다. 이 값은 `xdm`이어야 합니다. |
| `auth.params.name` | 만들려는 스트리밍 연결의 이름입니다. |
| `auth.params.authenticationRequired` | 생성된 스트리밍 연결을 지정하는 매개 변수 |
| `connectionSpec.id` | 스트리밍 연결을 위한 연결 사양 `id`입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 사항과 함께 HTTP 상태 201을 반환합니다.

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 연결의 `id`. 이것은 `{CONNECTION_ID}`이라고 합니다. |
| `etag` | 연결의 개정을 지정하는 연결에 할당된 식별자입니다. |

## 스트리밍 끝점 URL 가져오기

이제 연결이 만들어지면 스트리밍 끝점 URL을 검색할 수 있습니다.

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

성공적인 응답은 요청된 연결에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다. 스트리밍 끝점 URL은 연결과 함께 자동으로 만들어지며 `inletUrl` 값을 사용하여 검색할 수 있습니다.

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

## 다음 단계

이 자습서를 따라 스트리밍 HTTP 연결을 만들어 스트리밍 끝점을 사용하여 데이터를 플랫폼에 인제스트할 수 있습니다. UI에서 스트리밍 연결을 만드는 지침을 보려면 [스트리밍 연결 자습서 만들기](../../../ui/create/streaming/http.md)를 참조하십시오.

데이터를 플랫폼으로 스트리밍하는 방법을 알아보려면 [스트리밍 시간 시리즈 데이터](../../../../../ingestion/tutorials/streaming-time-series-data.md)에 대한 자습서 또는 [스트리밍 레코드 데이터](../../../../../ingestion/tutorials/streaming-record-data.md)에 대한 자습서를 읽으십시오.

## 부록

이 섹션에서는 API를 사용하여 스트리밍 연결을 만드는 방법에 대한 추가 정보를 제공합니다.

### 인증된 스트리밍 연결로 메시지 보내기

스트리밍 연결에 인증이 활성화되어 있으면 클라이언트는 `Authorization` 헤더를 요청에 추가해야 합니다.

`Authorization` 헤더가 없거나 유효하지 않거나 만료된 액세스 토큰이 전송되면 HTTP 401 권한 없는 응답이 아래와 같이 반환됩니다.

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
