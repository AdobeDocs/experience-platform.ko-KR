---
keywords: Experience Platform;홈;인기 항목;데이터 소스 연결
solution: Experience Platform
title: Flow Service API를 사용하여 제3자 클라우드 스토리지 시스템에서 쪽모이 세공 데이터를 인제스트
topic: 개요
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 제3자 클라우드 스토리지 시스템에서 Apache Timeline 데이터를 인제스트하는 단계를 안내합니다.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 타사 클라우드 스토리지 시스템에서 쪽모이 세공 데이터를 인제스트

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 타사 클라우드 스토리지 시스템에서 쪽모이 세공 데이터를 인제스트하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [소스](../../home.md): [!DNL Experience Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
- [샌드박스](../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 제3자 클라우드 스토리지에서 Partiented 데이터를 성공적으로 인제스트하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- `x-sandbox-name: `{SANDBOX_NAME}&#39;

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

- `Content-Type: application/json`

## 연결 만들기

[!DNL Platform] API를 사용하여 쪽모이 세공 데이터를 인제스트하려면 액세스 중인 제3자 클라우드 스토리지 소스에 대한 유효한 연결을 보유하고 있어야 합니다. 작업할 저장소에 대한 연결이 아직 없는 경우 다음 자습서를 통해 연결을 만들 수 있습니다.

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud 스토어](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

연결의 고유 식별자(`$id`)를 얻고 저장한 다음 이 자습서의 다음 단계로 진행합니다.

## 대상 스키마 만들기

소스 데이터를 [!DNL Platform]에서 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마도 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 [!DNL Platform] 데이터 집합을 만듭니다.

[!DNL Experience Platform]에서 사용자 인터페이스를 사용하려면 [스키마 편집기 자습서](../../../xdm/tutorials/create-schema-ui.md)에서 스키마 편집기에서 유사한 작업을 수행하기 위한 단계별 지침을 제공합니다.

**API 형식**

```http
POST /schemaregistry/tenant/schemas
```

**요청**

다음 예제 요청에서는 XDM [!DNL Individual Profile] 클래스를 확장하는 XDM 스키마를 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**응답**

성공적인 응답은 고유 식별자(`$id`)를 포함하여 새로 만든 스키마의 세부 정보를 반환합니다. 이 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{IMS_ORG}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 소스 연결 {#source} 만들기

대상 XDM 스키마가 생성되면 이제 [!DNL Flow Service] API에 대한 POST 요청을 사용하여 소스 연결을 만들 수 있습니다. 소스 연결은 API에 대한 연결, 소스 데이터 형식 및 이전 단계에서 검색된 대상 XDM 스키마에 대한 참조로 구성됩니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | 클라우드 스토리지를 나타내는 API에 대한 연결입니다. |
| `data.schema.id` | 이전 단계에서 대상 xdm 스키마를 검색한 경우 (`$id`). |
| `params.path` | 소스 파일의 경로입니다. |

**응답**

성공적인 응답은 새로 만든 소스 연결의 고유 식별자(`id`)를 반환합니다. 대상 연결을 만들기 위해 이 값을 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## 데이터 집합 기본 연결 만들기

외부 데이터를 [!DNL Platform]에 인제스트하려면 먼저 [!DNL Experience Platform] 데이터 세트 기본 연결을 취득해야 합니다.

데이터 집합 기본 연결을 만들려면 [데이터 집합 기본 연결 자습서](./create-dataset-base-connection.md)에 설명된 단계를 따릅니다.

데이터 세트 기본 연결을 만들 때까지 개발자 안내서에 설명된 단계를 계속 수행합니다. 고유 식별자(`$id`)를 가져와 저장하고 다음 단계에서 이것을 기본 연결 ID로 사용하여 대상 연결을 만듭니다.

## 대상 데이터 세트 만들기

대상 데이터 집합은 페이로드 내의 대상 스키마의 ID를 제공하여 [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)에 POST 요청을 수행하여 만들 수 있습니다.

**API 형식**

```http
POST /catalog/dataSets
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `schemaRef.id` | 대상 XDM 스키마의 ID입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트의 ID가 포함된 배열을 `"@/datasets/{DATASET_ID}"` 형식으로 반환합니다. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다. 타겟 데이터 세트 ID를 저장합니다. 이 ID는 이후 단계에서 필요에 따라 타겟 연결 및 데이터 흐름을 만듭니다.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## 대상 연결 {#target} 만들기

이제 데이터 집합 기본 연결, 대상 스키마 및 대상 데이터 집합에 대한 고유한 식별자가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 소스 데이터를 포함할 데이터 세트를 지정할 수 있습니다.

**API 형식**

```http
POST /targetConnections
```

**요청**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | 데이터 집합 기본 연결의 ID입니다. |
| `data.schema.id` | 대상 XDM 스키마의 `$id`. |
| `params.dataSetId` | 대상 데이터 세트의 ID입니다. |
| `connectionSpec.id` | 클라우드 스토리지에 대한 연결 사양 ID. |

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`)를 반환합니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## 데이터 흐름 만들기

제3자 클라우드 저장소에서 쪽모이 세공 데이터를 인제스트하는 마지막 단계는 데이터 흐름을 만드는 것입니다. 현재 다음과 같은 필수 값이 준비되었습니다.

- [원본 연결 ID](#source)
- [Target 연결 ID](#target)

데이터 플로우는 소스에서 데이터를 예약하고 수집하는 작업을 수행합니다. 페이로드 내에서 이전에 언급한 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `sourceConnectionIds` | 이전 단계에서 검색된 소스 연결 ID. |
| `targetConnectionIds` | 이전 단계에서 대상 연결 ID를 검색했습니다. |

**응답**

성공적인 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## 다음 단계

이 튜토리얼을 따라 소스 커넥터를 만들어 제3자 클라우드 스토리지 시스템에서 쪽모이 세공 데이터를 정기적으로 수집합니다. 이제 [!DNL Real-time Customer Profile] 및 [!DNL Data Science Workspace] 등의 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../profile/home.md)
- [데이터 과학 작업 공간 개요](../../../data-science-workspace/home.md)
