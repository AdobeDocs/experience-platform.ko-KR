---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 소스 커넥터 및 API를 통해 외부 데이터베이스 또는 NoSQL 시스템에서 데이터 수집
topic: overview
translation-type: tm+mt
source-git-commit: 00764a59629eb8a5a06ac28ad446084b0bdb2293

---


# 소스 커넥터 및 API를 통해 외부 데이터베이스 또는 NoSQL 시스템에서 데이터 수집

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 데이터베이스 또는 NoSQL 시스템에서 데이터를 검색하고 소스 커넥터 및 API를 통해 플랫폼에 데이터를 인제스트하는 단계를 다룹니다.

## 시작하기

이 자습서에서는 파일의 경로 및 구조를 포함하여 플랫폼에 가져오려는 파일에 대한 정보와 유효한 기본 연결을 통해 타사 데이터베이스 또는 NoSQL 시스템에 액세스해야 합니다. 이 정보가 없는 경우 이 자습서를 시작하기 전에 Flow Service API를 사용하여 데이터베이스 또는 NoSQL 시스템을 [탐색하는](../explore/database-nosql.md) 자습서를 참조하십시오.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 제대로 이해하고 있어야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의](../../../../xdm/schema/composition.md)기본 사항:스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 레지스트리 개발자 안내서](../../../../xdm/api/getting-started.md):스키마 레지스트리 API에 대한 호출을 성공적으로 수행하기 위해 알아야 하는 중요한 정보를 포함합니다. 여기에는 사용자 `{TENANT_ID}`및 &quot;컨테이너&quot;의 개념, 요청을 수행하는 데 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).
* [카탈로그 서비스](../../../../catalog/home.md):Catalog는 Experience Platform의 데이터 위치 및 계열에 대한 기록 시스템입니다.
* [일괄 처리](../../../../ingestion/batch-ingestion/overview.md):일괄 처리 통합 API를 사용하면 데이터를 Experience Platform에 일괄 처리 파일로 인제스트할 수 있습니다.
* [샌드박스](../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션은 Flow Service API를 사용하여 데이터베이스 또는 NoSQL 시스템에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속한 리소스를 비롯하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 임시 XDM 클래스 및 스키마 만들기

소스 커넥터를 통해 외부 데이터를 플랫폼으로 가져오려면 원시 소스 데이터에 대해 애드혹 XDM 클래스 및 스키마를 만들어야 합니다.

애드혹 클래스 및 스키마를 만들려면 [애드혹 스키마 자습서에](../../../../xdm/tutorials/ad-hoc.md)설명된 단계를 따릅니다. 애드혹 클래스를 만들 때 소스 데이터에 있는 모든 필드에 대해 요청 본문 내에 설명해야 합니다.

임시 스키마를 만들 때까지 개발자 안내서에 설명된 단계를 계속 수행합니다. 임시 스키마의 고유 식별자(`$id`)를 입수하고 저장한 다음 이 자습서의 다음 단계로 진행합니다.

## 소스 연결 만들기 {#source}

임시 XDM 스키마를 만든 경우 이제 Flow Service API에 대한 POST 요청을 사용하여 소스 연결을 만들 수 있습니다. 소스 연결은 기본 연결, 소스 데이터 파일 및 소스 데이터를 설명하는 스키마에 대한 참조로 구성됩니다.

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection for database or NoSQL",
        "baseConnectionId": "54c22133-3a01-4d3b-8221-333a01bd3b03",
        "description": "Source Connection for database or NoSQL to ingest test1.Mytable",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c8c2b32d6f6a53d5ffc7212c37b3a9369282404a7bd551e8",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "test1.Mytable"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | 데이터베이스 또는 NoSQL 시스템에 대한 기본 연결의 ID입니다. |
| `data.schema.id` | 임시 `$id` XDM 스키마 |
| `params.path` | 소스 파일의 경로입니다. |
| `connectionSpec.id` | 데이터베이스 또는 NoSQL 시스템의 연결 사양 ID입니다. |

**응답**

성공적인 응답은 새로 만든 소스 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 타겟 연결을 만들려면 이후 단계에서 필요합니다.

```json
{
    "id": "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8",
    "etag": "\"1600f153-0000-0200-0000-5e4710880000\""
}
```

## 대상 XDM 스키마 만들기 {#target}

이전 단계에서는 임시 XDM 스키마를 만들어 소스 데이터를 구조화합니다. 소스 데이터를 플랫폼에서 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마도 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 플랫폼 데이터 집합을 만듭니다. 이 대상 XDM 스키마는 XDM 개별 프로필 클래스도 확장합니다.

대상 XDM 스키마는 스키마 레지스트리 API에 대한 POST 요청을 수행하여 만들 [수 있습니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). 경험 플랫폼에서 사용자 인터페이스를 사용하려는 경우 스키마 편집기 자습서에서 [](../../../../xdm/tutorials/create-schema-ui.md) 스키마 편집기에서 유사한 작업을 수행하기 위한 단계별 지침을 제공합니다.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

다음 예제 요청은 XDM 개별 프로필 클래스를 확장하는 XDM 스키마를 만듭니다.

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
        "title": "Target schema for database or NoSQL",
        "description": "Target schema for database or NoSQL",
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
    }'
```

**응답**

성공적인 응답은 고유 식별자(`$id`)를 포함하여 새로 만든 스키마의 세부 정보를 반환합니다. 이 ID 파섹

```json
{
    "$id": "https://ns.adobe.com/{TENANT}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:altId": "_{TENANT}.schemas.a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for database or NoSQL",
    "type": "object",
    "description": "Target schema for database or NoSQL",
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
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
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
        "https://ns.adobe.com/xdm/common/extensible"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1581716110281,
        "repo:lastModifiedDate": 1581716110281,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "6360f2175b40462ff25ec8735dc93a7e3af6a8faadd80a1cc500a59721e1a424"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## 타겟 데이터 세트 만들기

페이로드 내의 대상 스키마의 ID를 제공하여 카탈로그 [서비스 API에](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)대한 POST 요청을 수행하여 대상 데이터 집합을 만들 수 있습니다.

**API 형식**

```http
POST /dataSets
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
        "name": "Target Dataset for database or NoSQL",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `schemaRef.id` | 대상 XDM 스키마의 ID입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 집합의 ID가 들어 있는 배열을 형식으로 `"@/datasets/{DATASET_ID}"`반환합니다. 데이터 집합 ID는 API 호출에서 데이터 집합을 참조하는 데 사용되는 읽기 전용, 시스템 생성 문자열입니다. 타겟 데이터 집합 ID를 나중에 타겟 연결 및 데이터 흐름 만들기 위해 필요에 따라 저장합니다.

```json
[
    "@/dataSets/5e47161fa49bb818ad7f47bd"
]
```

## 데이터 집합 기본 연결 만들기

외부 데이터를 플랫폼에 인제스트하려면 먼저 Experience Platform 데이터 세트 기본 연결을 확보해야 합니다.

데이터 집합 기본 연결을 만들려면 [데이터 집합 기본 연결 자습서에](../create-dataset-base-connection.md)설명된 단계를 따릅니다.

데이터 세트 기본 연결을 만들 때까지 개발자 안내서에 설명된 단계를 계속 수행합니다. 고유 식별자(`$id`)를 입수하여 저장한 다음 다음 단계에서 기본 연결 ID로 사용하여 대상 연결을 만듭니다.

## 대상 연결 만들기

이제 데이터 집합 기본 연결에 대한 고유한 식별자, 대상 스키마 및 대상 데이터 집합을 가집니다. 이러한 식별자를 사용하여 Flow Service API를 사용하여 대상 연결을 만들어 인바운드 소스 데이터를 포함할 데이터 세트를 지정할 수 있습니다.

**API 형식**

```http
POST /targetConnections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection for database or NoSQL",
        "description": "Target Connection for database or NoSQL",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e47161fa49bb818ad7f47bd"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `baseConnectionId` | 데이터 집합 기본 연결의 ID입니다. |
| `data.schema.id` | 대상 `$id` XDM 스키마의 내용입니다. |
| `params.dataSetId` | 대상 데이터 집합의 ID입니다. |
| `connectionSpec.id` | 타사 데이터베이스의 연결 사양 ID입니다. |

>[!NOTE] 대상 연결을 만들 때는 타사 소스 커넥터의 기본 연결과 `id` 반대로 기본 연결에 데이터 집합 기본 연결 값을 사용해야 합니다.

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`)를 반환합니다. 이 값은 이후 단계에서 데이터 흐름을 만들려면 필요합니다.

```json
{
    "id": "4f3845b6-87d9-4702-b845-b687d9270297",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 집합으로 인제스트하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다. 이것은 요청 페이로드 내에 정의된 데이터 매핑이 있는 전환 서비스 API에 대한 POST 요청을 수행하여 수행됩니다.

**API 형식**

```http
POST /mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name",
                "sourceAttribute": "Name",
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
                "sourceAttribute": "email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `xdmSchema` | 대상 `$id` XDM 스키마의 내용입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 ID는 나중에 데이터 흐름을 만들려면 필요합니다.

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
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/efea012ad5deefcdf51afd23ceb3583f",
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
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## 데이터 흐름 사양 조회 {#specs}

데이터 흐름(Dataflow)은 소스에서 데이터를 수집하여 Platform으로 가져와야 합니다. 데이터 흐름을 만들려면 먼저 Flow Service API에 대한 GET 요청을 수행하여 데이터 흐름 사양을 얻어야 합니다. 데이터 흐름 사양은 외부 데이터베이스 또는 NoSQL 시스템에서 데이터를 수집하는 책임을 집니다.

**API 형식**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터베이스 또는 NoSQL 시스템에서 Platform으로 데이터를 가져오는 작업을 담당하는 데이터 흐름 세부 항목의 세부 정보를 반환합니다. 이 ID는 새 데이터 흐름을 만들려면 다음 단계에서 필요합니다.

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "transformationSpecs": [
                {
                    "name": "Copy",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "properties": {
                            "deltaColumn": {
                                "type": "object",
                                "properties": {
                                    "name": {
                                        "type": "string"
                                    },
                                    "dateFormat": {
                                        "type": "string"
                                    },
                                    "timezone": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "name"
                                ]
                            }
                        },
                        "required": [
                            "deltaColumn"
                        ]
                    }
                },
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

데이터 흐름을 만드는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이 시점에서 다음과 같은 필수 값을 준비해야 합니다.

* [소스 연결 ID](#source)
* [대상 연결 ID](#target)
* [매핑 ID](#mapping)
* [데이터 흐름 사양 ID](#specs)

데이터 흐름(Dataflow)은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에서 이전에 언급된 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

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
        "name": "Dataflow between database or NoSQL Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8"
        ],
        "targetConnectionIds": [
            "4f3845b6-87d9-4702-b845-b687d9270297"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
                    "mappingVersion": "0"
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
| -------- | ----------- |
| `flowSpec.id` | 데이터베이스 또는 NoSQL 시스템과 연결된 데이터 흐름 사양 ID입니다. |
| `sourceConnectionIds` | 데이터베이스 또는 NoSQL 시스템과 연결된 소스 연결 ID입니다. |
| `targetConnectionIds` | 데이터베이스 또는 NoSQL 시스템과 연결된 대상 연결 ID입니다. |
| `transformations.params.mappingId` | 데이터베이스 또는 NoSQL 시스템과 연결된 매핑 ID입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 흐름(`id`)의 ID를 반환합니다.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## 다음 단계

이 자습서를 따라 데이터베이스 또는 NoSQL 시스템에서 데이터를 수집하기 위한 소스 커넥터를 만들었습니다. 이제 실시간 고객 프로필 및 데이터 과학 작업 공간과 같은 다운스트림 플랫폼 서비스에서 들어오는 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../profile/home.md)
* [데이터 과학 작업 공간 개요](../../../../data-science-workspace/home.md)