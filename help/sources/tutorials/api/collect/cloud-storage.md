---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 소스 커넥터 및 API를 통해 클라우드 스토리지 데이터 수집
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 1%

---


# 소스 커넥터 및 API를 통해 클라우드 스토리지 데이터 수집

이 자습서에서는 타사 클라우드 저장소에서 데이터를 검색하고 소스 커넥터 및 API를 통해 플랫폼으로 가져오는 단계를 다룹니다.

## 시작하기

이 자습서에서는 파일의 경로 및 구조를 포함하여 플랫폼에 가져오려는 파일에 대한 정보와 유효한 기본 연결을 통해 타사 클라우드 스토리지에 액세스해야 합니다. 이 정보가 없는 경우 이 튜토리얼을 시작하기 전에 Flow Service API를 사용하여 타사 클라우드 스토리지 [를 탐색하는 방법을](../explore/cloud-storage.md) 참조하십시오.

또한 이 튜토리얼을 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 제대로 이해해야 합니다.

- [XDM(Experience Data Model) 시스템](../../../../xdm/home.md): 고객 경험 데이터를 구성하는 표준 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 레지스트리 개발자 가이드](../../../../xdm/api/getting-started.md): 스키마 레지스트리 API에 대한 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보를 포함합니다. 여기에는 사용자 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청 시 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).
- [카탈로그 서비스](../../../../catalog/home.md): Catalog는 Experience Platform 내의 데이터 위치 및 계열에 대한 기록 시스템입니다.
- [일괄 처리](../../../../ingestion/batch-ingestion/overview.md): 일괄 처리 통합 API를 사용하면 데이터를 일괄 처리 파일로 경험 플랫폼에 인제스트할 수 있습니다.
- [샌드박스](../../../../sandboxes/home.md): 경험 플랫폼은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 클라우드 스토리지에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 경험 플랫폼 문제 해결 안내서에서 예제 API 호출 [](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기를 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 경험 플랫폼 API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증: 무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

- 컨텐츠 유형: `application/json`

## 임시 XDM 클래스 및 스키마 만들기

소스 커넥터를 통해 외부 데이터를 플랫폼으로 가져오려면 원시 소스 데이터에 대해 임시 XDM 클래스 및 스키마를 만들어야 합니다.

애드혹 클래스 및 스키마를 만들려면 [애드혹 스키마 자습서에 설명된 단계를 따릅니다](../../../../xdm/tutorials/ad-hoc.md). 애드혹 클래스를 만들 때 소스 데이터에 있는 모든 필드는 요청 본문 내에 설명되어야 합니다.

임시 스키마를 만들 때까지 개발자 안내서에 설명된 단계를 계속 수행합니다. 임시 스키마의 고유한 식별자(`$id`)를 입수하고 저장한 다음 이 자습서의 다음 단계로 진행합니다.

## 소스 연결 만들기 {#source}

임시 XDM 스키마를 만든 경우 이제 Flow Service API에 대한 POST 요청을 사용하여 소스 연결을 만들 수 있습니다. 소스 연결은 기본 연결, 소스 데이터 파일 및 소스 데이터를 설명하는 스키마에 대한 참조로 구성됩니다.

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
        "name": "Source Connection for a cloud storage",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "description": "Source Connection to ingest data.csv",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/140c03de81b959db95879033945cfd4c",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/some/path/data.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| 속성 | 설명 |
| --- | --- |
| `baseConnectionId` | 클라우드 스토리지 시스템에 대한 기본 연결의 ID. |
| `data.schema.id` | 임시 XDM 스키마의 ID입니다. |
| `params.path` | 소스 파일의 경로입니다. |

**응답**

성공적인 응답은 새로 만든 소스 연결의 고유 식별자(`id`)를 반환합니다. 이 값은 나중에 대상 연결을 만들기 위해 필요에 따라 저장합니다.

```json
{
    "id": "9a603322-19d2-4de9-89c6-c98bd54eb184"
}
```

## 대상 XDM 스키마 만들기 {#target}

이전 단계에서는 소스 데이터를 구조화하기 위해 임시 XDM 스키마를 만들었습니다. 소스 데이터를 플랫폼에서 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 플랫폼 데이터 세트를 만듭니다.

경험 플랫폼에서 사용자 인터페이스를 사용하려는 경우 스키마 편집기 자습서 [](../../../../xdm/tutorials/create-schema-ui.md) 는 스키마 편집기에서 유사한 작업을 수행하기 위한 단계별 지침을 제공합니다.

**API 형식**

```http
POST /schemaregistry/tenant/schemas
```

**요청**

다음 예제 요청에서는 XDM 개별 프로필 클래스를 확장하는 XDM 스키마를 만듭니다.

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
        "title": "Target schema for cloud storage source connector",
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
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**응답**

성공적인 응답은 고유한 식별자(`$id`)를 포함하여 새로 만든 스키마의 세부 정보를 반환합니다. 이 ID를 나중에 대상 데이터 세트, 매핑 및 데이터 흐름을 만들려면 필요에 따라 저장합니다.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
    "meta:altId": "{TENANT_ID}.schemas.417a33eg81a221bd10495920574gfa2d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for cloud storage source connector",
    "description": "",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "meta:registryMetadata": {
        "eTag": "6m/FrIlXYU2+yH6idbcmQhKSlMo="
    }
}
```

## 대상 데이터 세트 만들기

페이로드 내의 대상 스키마의 ID를 제공하여 카탈로그 서비스 API에 대한 POST 요청을 수행하여 대상 데이터 집합을 만들 수 있습니다.

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
        "name": "Target Dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `schemaRef.id` | 대상 XDM 스키마의 ID입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 형식 `"@/datasets/{DATASET_ID}"`입니다. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다. 타겟 데이터 집합 ID를 나중에 타겟 연결 및 데이터 흐름을 만드는 데 필요한 만큼 저장합니다.

```json
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 데이터 집합 기본 연결 만들기

외부 데이터를 플랫폼에 인제스트하려면 먼저 경험 플랫폼 데이터 세트 기본 연결을 확보해야 합니다.

데이터 집합 기본 연결을 만들려면 데이터 집합 [기본 연결 자습서에 설명된 단계를 따릅니다](../create-dataset-base-connection.md).

데이터 세트 기본 연결을 만들 때까지 개발자 안내서에 설명된 단계를 계속 수행합니다. 고유 식별자(`$id`)를 입수하고 저장하고 다음 단계에서 기본 연결 ID로 사용하여 대상 연결을 만듭니다.

## 대상 연결 만들기

이제 데이터 집합 기본 연결, 대상 스키마 및 대상 데이터 집합에 대한 고유한 식별자가 있습니다. 이러한 식별자를 사용하여 Flow Service API를 사용하여 대상 연결을 만들어 인바운드 소스 데이터를 포함할 데이터 세트를 지정할 수 있습니다.

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
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection",
        "description": "Target Connection for cloud storage data",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5c8c3c555033b814b69f947f"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | 데이터 집합 기본 연결의 ID입니다. |
| `data.schema.id` | 대상 XDM 스키마 `$id` 의 이름입니다. |
| `params.dataSetId` | 대상 데이터 집합의 ID입니다. |
| `connectionSpec.id` | 클라우드 스토리지에 대한 연결 사양 ID. |

>[!NOTE] 대상 연결을 만들 때는 타사 소스 커넥터의 기본 연결과 `id` 반대로 기본 연결에 Data Lake 기본 연결 값을 사용해야 합니다.

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`)를 반환합니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "4ee890c7-519c-4291-bd20-d64186b62da8",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 세트에 수집하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다. 이것은 요청 페이로드 내에 정의된 데이터 매핑과 함께 전환 서비스에 대한 POST 요청을 수행하여 수행됩니다.

**API 형식**

```http
POST /conversion/mappingSets
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Phone",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "Email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 속성 | 설명 |
| --- | --- |
| `xdmSchema` | 대상 XDM 스키마의 ID입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 값은 데이터 흐름 생성을 위해 나중 단계에서 필요하므로 저장합니다.

```json
{
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## 데이터 흐름 사양 검색 {#specs}

데이터 프롤은 소스에서 데이터를 수집하고 플랫폼으로 가져와야 합니다. 데이터 흐름을 만들려면 먼저 클라우드 스토리지 데이터 수집을 담당하는 데이터 흐름 사양을 얻어야 합니다.

**API 형식**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답으로 클라우드 스토리지의 데이터를 Platform으로 가져오는 작업을 담당하는 데이터 흐름 세부 항목의 세부 정보를 반환합니다. 새 데이터 흐름 `id` 을 만들려면 다음 단계에서 필요한 대로 필드 값을 저장합니다.

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            },
                            "mappingVersion": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "scheduleSpec": {
                "name": "PeriodicSchedule",
                "type": "Periodic",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "startTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
                        "interval"
                    ],
                    "if": {
                        "properties": {
                            "frequency": {
                                "const": "minute"
                            }
                        }
                    },
                    "then": {
                        "properties": {
                            "interval": {
                                "minimum": 15
                            }
                        }
                    },
                    "else": {
                        "properties": {
                            "interval": {
                                "minimum": 1
                            }
                        }
                    }
                }
            }
        }
    ]
}
```

## 데이터 흐름 만들기

클라우드 스토리지 데이터를 수집하는 마지막 단계는 데이터 흐름을 만드는 것입니다. 현재 다음과 같은 필수 값이 준비되었습니다.

- [원본 연결 ID](#source)
- [대상 연결 ID](#target)
- [매핑 ID](#mapping)
- [데이터 흐름 사양 ID](#specs)

데이터 프롤은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

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
        "name": "Dataflow between cloud storage and Platform",
        "description": "collecting data.csv",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "9a603322-19d2-4de9-89c6-c98bd54eb184"
        ],
        "targetConnectionIds": [
            "4ee890c7-519c-4291-bd20-d64186b62da8"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "mode": "append"
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `flowSpec.id` | 데이터 흐름 사양 ID |
| `sourceConnectionIds` | 원본 연결 ID |
| `targetConnectionIds` | 대상 연결 ID |
| `transformations.params.mappingId` | 매핑 ID |

**응답**

성공적인 응답은 새로 만든 데이터 흐름`id`의 ID를 반환합니다.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## 다음 단계

이 튜토리얼을 따라 소스 커넥터를 만들어 일정에 따라 클라우드 스토리지의 데이터를 수집합니다. 이제 실시간 고객 프로필 및 데이터 과학 작업 공간과 같은 다운스트림 플랫폼 서비스에서 들어오는 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../../profile/home.md)
- [데이터 과학 작업 공간 개요](../../../../data-science-workspace/home.md)

## 부록

다음 섹션에는 다른 클라우드 스토리지 소스 커넥터 및 해당 연결 사양이 나열됩니다.

### 연결 사양

| 커넥터 이름 | 연결 사양 |
| -------------- | --------------- |
| Amazon S3(S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| Amazon Kinesis(Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| Azure Blob(Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| Azure Data Lake Storage Gen2(ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| Azure 이벤트 허브(EventHub) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| Google 클라우드 스토리지 | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |