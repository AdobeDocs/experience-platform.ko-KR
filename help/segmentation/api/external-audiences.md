---
title: 외부 대상 API 엔드포인트
description: 외부 대상 API를 사용하여 Adobe Experience Platform에서 외부 대상을 만들고, 업데이트하고, 활성화하고, 삭제하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '2312'
ht-degree: 4%

---


# 외부 대상 엔드포인트

외부 대상을 사용하면 외부 소스의 프로필 데이터를 Adobe Experience Platform에 업로드할 수 있습니다. 세그먼테이션 서비스 API의 `/external-audience` 끝점을 사용하여 외부 대상을 Experience Platform으로 수집하고, 세부 정보를 보고, 외부 대상을 업데이트하며, 외부 대상을 삭제할 수 있습니다.

## 시작

>[!IMPORTANT]
>
>이 안내서의 끝점에는 `/core/ais`이(가) 아닌 `/core/ups`이(가) 접두사로 사용됩니다.

Experience Platform API를 사용하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Experience Platform] API에 대한 모든 요청에는 작업을 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스 작업에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하세요.

## 외부 대상 만들기 {#create-audience}

`/external-audience/` 끝점에 대한 POST 요청을 수행하여 외부 대상을 만들 수 있습니다.

**API 형식**

```http
POST /external-audience/
```

**요청**

+++ 외부 대상을 만들기 위한 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `name` | 문자열 | 외부 대상의 이름입니다. |
| `description` | 문자열 | 외부 대상자에 대한 선택적 설명입니다. |
| `customAudienceId` | 문자열 | 외부 대상자에 대한 선택적 식별자입니다. |
| `fields` | 오브젝트 배열 | 필드 및 해당 데이터 유형 목록. 필드 목록을 만들 때 다음 항목을 추가할 수 있습니다. <ul><li>`name`: **필수** 외부 대상 지정에 속하는 필드의 이름입니다.</li><li>`type`: **필수** 필드에 들어가는 데이터 형식입니다. 지원되는 값은 `string`, `number`, `long`, `integer`, `date`(`2025-05-13`), `datetime`(`2025-05-23T20:19:00+00:00`) 및 `boolean`입니다.</li>`identityNs`: **ID 필드에 필요** ID 필드에서 사용하는 네임스페이스입니다. 지원되는 값에는 `ECID` 또는 `email`.li>과 같이 유효한 모든 네임스페이스가 포함됩니다.<li>`labels`: *선택 사항* 필드에 대한 액세스 제어 레이블의 배열입니다. 사용 가능한 액세스 제어 레이블에 대한 자세한 내용은 [데이터 사용 레이블 용어집](/help/data-governance/labels/reference.md)에 있습니다. </li></ul> |
| `sourceSpec` | 오브젝트 | 외부 대상자가 있는 정보가 포함된 객체입니다. 이 개체를 사용할 때 **다음 정보를 포함해야** 합니다. <ul><li>`path`: **필수**: 외부 대상 또는 소스 내의 외부 대상이 포함된 폴더의 위치입니다.</li><li>`type`: **필수** 원본에서 검색 중인 개체의 형식입니다. 이 값은 `file` 또는 `folder`일 수 있습니다.</li><li>`sourceType`: *선택 사항* 검색 중인 원본 유형입니다. 현재 지원되는 값은 `Cloud Storage`뿐입니다.</li><li>`cloudType`: *선택 사항* 원본 유형에 따른 클라우드 저장소 유형입니다. 지원되는 값은 `S3`, `DLZ`, `GCS` 및 `SFTP`입니다.</li><li>`baseConnectionId`: 기본 연결의 ID이며 원본 공급자에서 제공됩니다. **,** 또는 `cloudType`의 `S3` 값을 사용하는 경우 이 값은 `GCS`required`SFTP`입니다. 자세한 내용은 [소스 커넥터 개요](../../sources/home.md)li>를 참조하십시오.</ul> |
| `ttlInDays` | 정수 | 외부 대상에 대한 데이터 만료(일 단위). 이 값은 1부터 90까지 설정할 수 있습니다. 기본적으로 데이터 만료는 30일로 설정됩니다. |
| `audienceType` | 문자열 | 외부 대상의 대상 유형입니다. 현재 `people`만 지원됩니다. |
| `originName` | 문자열 | **필수** 대상자의 원본입니다. 이는 대상자가 어디에서 오는지 설명합니다. 외부 대상의 경우 `CUSTOM_UPLOAD`을(를) 사용해야 합니다. |
| `namespace` | 문자열 | 대상자를 위한 네임스페이스입니다. 기본적으로 이 값은 `CustomerAudienceUpload`(으)로 설정됩니다. |
| `labels` | 문자열 배열 | 외부 대상에 적용되는 액세스 제어 레이블입니다. 사용 가능한 액세스 제어 레이블에 대한 자세한 내용은 [데이터 사용 레이블 용어집](/help/data-governance/labels/reference.md)에 있습니다. |
| `tags` | 문자열 배열 | 외부 대상에 적용할 태그입니다. 태그에 대한 자세한 내용은 [태그 관리 가이드](/help/administrative-tags/ui/managing-tags.md)에서 확인할 수 있습니다. |

+++

**응답**

성공적인 응답은 새로 생성된 외부 대상의 세부 정보와 함께 HTTP 상태 202를 반환합니다.

+++ 외부 대상을 만들 때의 샘플 응답입니다.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `operationId` | 문자열 | 작업의 ID입니다. 그런 다음 이 ID를 사용하여 대상자의 생성 상태를 검색할 수 있습니다. |
| `operationDetails` | 오브젝트 | 외부 대상을 만들기 위해 제출한 요청의 세부 정보가 포함된 객체입니다. |
| `name` | 문자열 | 외부 대상의 이름입니다. |
| `description` | 문자열 | 외부 대상에 대한 설명입니다. |
| `fields` | 오브젝트 배열 | 필드 및 해당 데이터 유형 목록. 이 배열은 외부 대상자에 필요한 필드를 결정합니다. |
| `sourceSpec` | 오브젝트 | 외부 대상자가 있는 정보가 포함된 객체입니다. |
| `ttlInDays` | 정수 | 외부 대상에 대한 데이터 만료(일 단위). 이 값은 1부터 90까지 설정할 수 있습니다. 기본적으로 데이터 만료는 30일로 설정됩니다. |
| `audienceType` | 문자열 | 외부 대상의 대상 유형입니다. |
| `originName` | 문자열 | **필수** 대상자의 원본입니다. 이는 대상자가 어디에서 오는지 설명합니다. |
| `namespace` | 문자열 | 대상자를 위한 네임스페이스입니다. |
| `labels` | 문자열 배열 | 외부 대상에 적용되는 액세스 제어 레이블입니다. 사용 가능한 액세스 제어 레이블에 대한 자세한 내용은 [데이터 사용 레이블 용어집](/help/data-governance/labels/reference.md)에 있습니다. |


+++

## 대상자 만들기 상태 가져오기 {#retrieve-status}

`/external-audiences/operations` 끝점에 대한 GET 요청을 만들고 외부 대상 만들기 응답에서 받은 작업의 ID를 제공하여 외부 대상 제출 상태를 검색할 수 있습니다.

**API 형식**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{OPERATION_ID}` | 검색할 작업의 `id` 값입니다. |

**요청**

+++ 외부 대상의 작업 상태를 검색하기 위한 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 외부 대상의 작업 상태에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 외부 대상의 작업 상태를 가져올 때의 샘플 응답입니다.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "path": "activation/sample-source/example.csv",
            "type": "file",
            "sourceType": "Cloud Storage",
            "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `operationId` | 문자열 | 검색 중인 작업의 ID입니다. |
| `status` | 문자열 | 작업의 상태입니다. `SUCCESS`, `FAILED`, `PROCESSING` 값 중 하나일 수 있습니다. |
| `operationDetails` | 오브젝트 | 대상자의 세부 정보를 포함하는 객체입니다. |
| `audienceId` | 문자열 | 작업에서 제출 중인 외부 대상의 ID입니다. |
| `createdBy` | 문자열 | 외부 대상을 만든 사용자의 ID입니다. |
| `createdAt` | 긴 에포크 타임스탬프 | 외부 대상 만들기 요청이 제출된 타임스탬프(초). |
| `updatedBy` | 문자열 | 대상자를 마지막으로 업데이트한 사용자의 ID입니다. |
| `updatedAt` | 긴 에포크 타임스탬프 | 대상이 마지막으로 업데이트된 타임스탬프(초)입니다. |

+++

## 외부 대상 업데이트 {#update-audience}

>[!NOTE]
>
>다음 끝점을 사용하려면 외부 대상의 `audienceId`이(가) 있어야 합니다. `audienceId` 끝점에 대한 성공적인 호출에서 `GET /external-audiences/operations/{OPERATION_ID}`을(를) 가져올 수 있습니다.

`/external-audience` 끝점에 대한 PATCH 요청을 만들고 요청 경로에 대상자의 ID를 제공하여 외부 대상의 필드를 업데이트할 수 있습니다.

이 끝점을 사용할 때 다음 필드를 업데이트할 수 있습니다.

- 대상자 설명
- 필드 수준 액세스 제어 레이블
- 대상자 수준 액세스 제어 레이블

이 끝점을 사용하여 필드를 업데이트하면 요청한 필드의 내용이 **대체**&#x200B;됩니다.

**API 형식**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**요청**

+++ 외부 대상자의 설명을 업데이트하기 위한 샘플 요청입니다.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `description` | 문자열 | 외부 대상에 대해 업데이트된 설명. |

또한 다음 매개 변수를 업데이트할 수 있습니다.

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `labels` | 배열 | 대상에 대해 업데이트된 액세스 레이블 목록이 포함된 배열입니다. 사용 가능한 액세스 제어 레이블에 대한 자세한 내용은 [데이터 사용 레이블 용어집](/help/data-governance/labels/reference.md)에 있습니다. |
| `fields` | 오브젝트 배열 | 외부 대상에 대한 필드 및 관련 레이블이 포함된 배열입니다. PATCH 요청에 나열된 필드만 업데이트됩니다. 사용 가능한 액세스 제어 레이블에 대한 자세한 내용은 [데이터 사용 레이블 용어집](/help/data-governance/labels/reference.md)에 있습니다. |
| `ttlInDays` | 정수 | 외부 대상에 대한 데이터 만료(일 단위). 이 값은 1부터 90까지 설정할 수 있습니다. |

+++

**응답**

성공적인 응답은 업데이트된 외부 대상의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 외부 대상자의 설명을 업데이트할 때의 샘플 응답입니다.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## 대상자 수집 시작 {#start-audience-ingestion}

>[!IMPORTANT]
>
>이전 대상 수집이 이미 진행 중인 경우 외부 대상에 대한 새 수집을 **시작할 수 없습니다**.

>[!NOTE]
>
>다음 끝점을 사용하려면 외부 대상의 `audienceId`이(가) 있어야 합니다. `audienceId` 끝점에 대한 성공적인 호출에서 `GET /external-audiences/operations/{OPERATION_ID}`을(를) 가져올 수 있습니다.

대상 ID를 제공하는 동안 다음 엔드포인트에 POST 요청을 하여 대상 수집을 시작할 수 있습니다.

**API 형식**

```http
POST /external-audience/{AUDIENCE_ID}/run
```

**요청**

다음 요청은 외부 대상에 대해 수집 실행을 트리거합니다.

+++ 대상자 수집을 시작하는 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/run \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Epoch 타임스탬프 | **필수** 처리할 파일을 선택하기 위해 흐름을 실행할 시작 시간을 지정하는 범위입니다. |
| `dataFilterEndTime` | Epoch 타임스탬프 | 처리할 파일을 선택하기 위해 플로우를 실행할 종료 시간을 지정하는 범위입니다. |
| `differentialIngestion` | 부울 | 마지막 수집 이후의 차이 또는 전체 대상 수집에 따라 수집이 부분 수집인지 여부를 결정하는 필드입니다. 기본적으로 이 값은 `true`입니다. |

+++

**응답**

성공적인 응답은 수집 실행에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 대상자 수집을 시작할 때의 샘플 응답입니다.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `audienceName` | 문자열 | 수집 실행을 시작하는 대상자의 이름입니다. |
| `audienceId` | 문자열 | 대상자의 ID입니다. |
| `runId` | 문자열 | 시작한 수집 실행의 ID입니다. |
| `differentialIngestion` | 부울 | 마지막 수집 이후의 차이점을 기반으로 수집이 부분 수집인지 전체 대상 수집인지 결정하는 필드입니다. |
| `dataFilterStartTime` | Epoch 타임스탬프 | 처리된 파일을 선택하기 위한 플로우 실행의 시작 시간을 지정하는 범위입니다. |
| `dataFilterEndTime` | Epoch 타임스탬프 | 처리된 파일을 선택하기 위해 흐름이 실행되는 종료 시간을 지정하는 범위입니다. |
| `createdAt` | 긴 에포크 타임스탬프 | 외부 대상 만들기 요청이 제출된 타임스탬프(초). |
| `createdBy` | 문자열 | 외부 대상을 만든 사용자의 ID입니다. |

+++

## 특정 대상자 수집 상태 검색 {#retrieve-ingestion-status}

대상과 실행 ID를 모두 제공하면서 다음 끝점에 GET 요청을 하여 대상 수집 상태를 검색할 수 있습니다.

**API 형식**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**요청**

다음 요청은 외부 대상자에 대한 수집 상태를 검색합니다.

+++ 외부 대상의 수집 상태를 검색하는 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 외부 대상 수집에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 외부 대상의 수집을 검색할 때의 샘플 응답입니다.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `audienceName` | 문자열 | 대상자의 이름입니다. |
| `audienceId` | 문자열 | 대상자의 ID입니다. |
| `runId` | 문자열 | 수집 실행의 ID입니다. |
| `status` | 문자열 | 수집 실행의 상태입니다. 가능한 상태는 `SUCCESS` 및 `FAILED`입니다. |
| `differentialIngestion` | 부울 | 마지막 수집 이후의 차이점을 기반으로 수집이 부분 수집인지 전체 대상 수집인지 결정하는 필드입니다. |
| `dataFilterStartTime` | Epoch 타임스탬프 | 처리된 파일을 선택하기 위한 플로우 실행의 시작 시간을 지정하는 범위입니다. |
| `dataFilterEndTime` | Epoch 타임스탬프 | 처리된 파일을 선택하기 위해 흐름이 실행되는 종료 시간을 지정하는 범위입니다. |
| `createdAt` | 긴 에포크 타임스탬프 | 외부 대상 만들기 요청이 제출된 타임스탬프(초). |
| `createdBy` | 문자열 | 외부 대상을 만든 사용자의 ID입니다. |
| `details` | 오브젝트 배열 | 수집 실행의 세부 사항이 포함된 객체입니다. <ul><li>`stage`: 수집 실행 단계입니다. 데이터 레이크 수집과 프로필 수집을 나타내는 `DATASET_INGEST` 또는 `PROFILE_STORE_INGEST`일 수 있습니다.</li><li>`status`: 단계에 있는 수집 상태입니다. 가능한 상태는 `SUCCESS` 및 `FAILED`입니다.</li><li>`flowRunId`: 스테이지에서 실행 중인 수집 흐름의 ID입니다.</li></ul> |

+++

## 대상자 수집 상태 나열 {#list-ingestion-statuses}

대상 ID를 제공하는 동안 다음 끝점에 GET 요청을 하여 선택한 외부 대상에 대한 모든 수집 상태를 검색할 수 있습니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다.

**API 형식**

다음 끝점은 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 결과에 초점을 맞추는 데 도움이 되도록 사용하는 것이 좋습니다.

```http
GET /external-audience/{AUDIENCE_ID}/runs
GET /external-audience/{AUDIENCE_ID}/runs?{QUERY_PARAMETERS}
```

**쿼리 매개 변수**

+++ 사용 가능한 쿼리 매개 변수 목록입니다.

| 매개변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `limit` | 응답에서 반환되는 최대 항목 수입니다. 이 값의 범위는 1에서 40까지입니다. 기본적으로 제한은 20으로 설정됩니다. | `limit=30` |
| `sortBy` | 반환된 항목이 정렬되는 순서입니다. `name` 또는 `ingestionTime`별로 정렬할 수 있습니다. 또한 `-` 기호를 추가하여 **오름차순** 순서 대신 **내림차순** 순서로 정렬할 수 있습니다. 기본적으로 항목은 `ingestionTime`을(를) 기준으로 내림차순으로 정렬됩니다. | `sortBy=name` |
| `property` | 표시되는 대상자 수집 실행을 결정하는 필터입니다. 다음 속성을 필터링할 수 있습니다. <ul><li>`name`: 대상 이름별로 필터링할 수 있습니다. 이 속성을 사용하는 경우 `=`, `!=`, `=contains` 또는 `!=contains`을(를) 사용하여 비교할 수 있습니다. </li><li>`ingestionTime`: 수집 시간별로 필터링할 수 있습니다. 이 속성을 사용하는 경우 `>=` 또는 `<=`을(를) 사용하여 비교할 수 있습니다.</li><li>`status`: 수집 실행 상태를 기준으로 필터링할 수 있습니다. 이 속성을 사용하는 경우 `=`, `!=`, `=contains` 또는 `!=contains`을(를) 사용하여 비교할 수 있습니다. </li></ul> | `property=ingestionTime<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++

**요청**

다음 요청은 외부 대상에 대한 모든 수집 상태를 검색합니다.

+++ 대상자 수집 상태 목록을 가져올 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 지정된 외부 대상에 대한 수집 상태 목록과 함께 HTTP 상태 200을 반환합니다.

+++ 대상자 수집 상태 목록을 검색할 때의 샘플 응답입니다.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}",
            "details": [
                {
                    "stage": "DATASET_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                },
                {
                    "stage": "PROFILE_STORE_INGEST",
                    "status": "SUCCESS",
                    "flowRunId": "{FLOW_RUN_ID}"
                }
            ]
        }
    ],
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
}
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `runs` | 오브젝트 | 수집 목록이 포함된 개체는 대상에 속하며 실행됩니다. 이 개체에 대한 자세한 내용은 [수집 상태 검색 섹션](#retrieve-ingestion-status)을 참조하십시오. |
| `_page` | 오브젝트 | 결과 목록에 대한 페이지 매김 정보가 포함된 객체입니다. |

+++

## 외부 대상 삭제 {#delete-audience}

대상 ID를 제공하는 동안 다음 엔드포인트에 DELETE 요청을 하여 외부 대상을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**요청**

다음 요청은 지정된 외부 대상을 삭제합니다.

+++ 외부 대상 삭제에 대한 샘플 요청입니다.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 빈 응답 본문과 함께 HTTP 상태 204를 반환합니다.

## 다음 단계 {#next-steps}

이 안내서를 읽은 후에는 Experience Platform API를 사용하여 외부 대상을 만들고, 관리하고, 삭제하는 방법을 더 잘 이해할 수 있습니다. Experience Platform UI로 외부 대상을 사용하는 방법을 알아보려면 [대상 포털 설명서](../ui/audience-portal.md)를 읽어 보십시오.

## 부록 {#appendix}

다음 섹션에서는 외부 대상 API를 사용할 때 사용할 수 있는 오류 코드를 나열합니다.

| 플랫폼 오류 코드 | 상태 코드 | 메시지 | 설명 |
| ------------------- | ----------- | ------- | ----------- |
| 100910- | 400 | `BAD_REQUEST` | 요청을 확인하는 동안 오류가 발생하여 잘못된 요청이 발생했습니다. |
| 100911- | 400 | `BAD_REQUEST` | 잘못된 토큰이 입력되었습니다. |
| 100920- | 401 | `UNAUTHORIZED` | 헤더가 누락되었습니다. |
| 100921- | 401 | `UNAUTHORIZED` | 잘못된 `imsOrgId`이(가) 입력되었습니다. |
| 100922- | 401 | `UNAUTHORIZED` | 외부 대상 API를 사용할 수 있는 권한이 없습니다. |
| 100940- | 404 | `NOT_FOUND` | 요청한 대상자를 찾을 수 없습니다. |
| 100950- | 409 | `DUPLICATE_RESOURCE` | 대상이 이미 있습니다. |
| 100960- | 422 | `UNPROCESSABLE_ENTITY` | 요청 구조는 유효하지만 논리적 또는 의미 체계 오류로 인해 처리할 수 없습니다. |
| 100970- | 500 | `INTERNAL_SERVER_ERROR` | 시스템에서 요청을 처리하는 도중 문제가 발생했습니다. |
| 100970-502 | 502 | `BAD_GATEWAY` | 다운스트림 종속성 문제가 있습니다. |
