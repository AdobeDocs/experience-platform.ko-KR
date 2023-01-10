---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;스키마;스키마 만들기
solution: Experience Platform
title: 스키마 API 끝점
description: 스키마 레지스트리 API의 /schema 종단점을 사용하면 경험 애플리케이션 내에서 XDM 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 4%

---

# 스키마 끝점

스키마는 Adobe Experience Platform에 수집하려는 데이터의 블루프린트로 생각할 수 있습니다. 각 스키마는 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. 다음 `/schemas` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 경험 애플리케이션 내의 스키마를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 스키마 목록 검색 {#list}

모든 스키마를 `global` 또는 `tenant` 컨테이너에 GET 요청 `/global/schemas` 또는 `/tenant/schemas`각각 입니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리에서 결과를 300개 항목으로 제한합니다. 이 제한 이상의 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 의 섹션을 참조하십시오. [쿼리 매개 변수](./appendix.md#query) 자세한 내용은 부록 문서에서 확인하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 스키마를 포함하는 컨테이너: `global` Adobe 생성 스키마 또는 `tenant` 에 대해 사용할 수 있습니다. |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [부록 문서](./appendix.md#query) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 스키마에서 스키마 목록을 검색합니다 `tenant` 컨테이너, `orderby` 결과를 정렬 기준으로 하는 쿼리 매개 변수 `title` 속성을 사용합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 `Accept` 헤더가 전송되었습니다. 다음 `Accept` 스키마를 나열할 때 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본과 함께 각 리소스에 대한 전체 JSON 스키마 반환 `$ref` 및 `allOf` 포함됩니다. (제한: 300) |

{style=&quot;table-layout:auto&quot;}

**응답**

위의 요청에서는 `application/vnd.adobe.xed-id+json` `Accept` 헤더. 따라서 응답에는 `title`, `$id`, `meta:altId`, 및 `version` 각 스키마에 대한 속성입니다. 다른 `Accept` 헤더 (`application/vnd.adobe.xed+json`)은 각 스키마의 모든 속성을 반환합니다. 적절한 `Accept` 헤더에서 사용할 수 있습니다.

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## 스키마 조회 {#lookup}

경로에 스키마의 ID가 포함된 GET 요청을 수행하여 특정 스키마를 찾을 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 스키마가 들어 있는 컨테이너입니다. `global` Adobe이 생성한 스키마 또는 `tenant` 를 사용하도록 선택할 수 있습니다. |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 검색할 스키마 중 하나입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 지정된 스키마를 검색합니다 `meta:altId` 값을 지정한 경우 이해할 수 있도록 해줍니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 `Accept` 헤더가 전송되었습니다. 모든 조회 요청에는 `version` 에 포함됨 `Accept` 헤더. 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 원시 `$ref` 및 `allOf`에는 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 및 `allOf` 해결됨, 에는 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | 원시 `$ref` 및 `allOf`, 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 및 `allOf` 해결됨, 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 및 `allOf` 해결된 설명자가 포함되어 있습니다. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 및 `allOf` 해결됨, 에는 제목 및 설명이 있습니다. 사용되지 않는 필드는 `meta:status` 속성 `deprecated`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 스키마 세부 정보를 반환합니다. 반환되는 필드는 `Accept` 헤더가 전송되었습니다. 다양한 실험 `Accept` 헤더를 사용하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인하십시오.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 스키마 만들기 {#create}

스키마 작성 프로세스는 클래스를 할당하여 시작됩니다. 이 클래스는 데이터의 주요 행동 측면(레코드 또는 시계열)과 수집할 데이터를 설명하는 데 필요한 최소 필드를 정의합니다.

>[!NOTE]
>
>아래 예제 호출은 클래스 및 필드 그룹이 없는 최소 구성 요구 사항을 사용하여 API에서 스키마를 만드는 방법의 기본 예일 뿐입니다. 필드 그룹 및 데이터 유형을 사용하여 필드를 할당하는 방법을 포함하여 API에서 스키마를 만드는 방법에 대한 전체 단계는 다음을 참조하십시오. [스키마 만들기 자습서](../tutorials/create-schema-api.md).

**API 형식**

```http
POST /tenant/schemas
```

**요청**

요청에는 `allOf` 를 참조하는 속성 `$id` A. 이 속성은 스키마가 구현할 &quot;기본 클래스&quot;를 정의합니다. 이 예제에서 기본 클래스는 이전에 만든 &quot;속성 정보&quot; 클래스입니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `allOf` | 각 객체가 스키마가 구현하는 클래스 또는 필드 그룹을 참조하는 객체 배열입니다. 각 객체에는 단일 속성(`$ref`) 값을 나타내는 `$id` 새 스키마가 구현할 클래스 또는 필드 그룹의 이름입니다. 하나 이상의 추가 필드 그룹과 함께 클래스를 제공해야 합니다. 위의 예에서 `allOf` 배열은 스키마의 클래스입니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 HTTP 상태 201(작성됨) 및 를 포함하여 새로 만든 스키마의 세부 사항이 포함된 페이로드를 반환합니다. `$id`, `meta:altId`, 및 `version`. 이러한 값은 읽기 전용이며 [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

에 GET 요청 수행 [모든 스키마 나열](#list) 이제 테넌트 컨테이너에 새 스키마가 포함됩니다. 다음을 수행할 수 있습니다 [조회(GET) 요청](#lookup) url로 인코딩된 `$id` 새 스키마를 직접 보려면 URI를 사용하십시오.

스키마에 필드를 더 추가하려면 [PATCH 작업](#patch) 스키마 `allOf` 및 `meta:extends` 배열

## 스키마 업데이트 {#put}

기본적으로 리소스를 다시 작성하는 PUT 작업을 통해 전체 스키마를 바꿀 수 있습니다. PUT 요청을 통해 스키마를 업데이트할 때는 본문에 [새 스키마 만들기](#create) POST 요청.

>[!NOTE]
>
>전체 스키마를 대체하지 않고 스키마의 일부만 업데이트하려면 [스키마 일부 업데이트](#patch).

**API 형식**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 다시 쓸 스키마 중 하나입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 스키마를 대체하여 스키마를 변경합니다 `title`, `description`, 및 `allOf` 속성을 사용합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**응답**

성공적인 응답은 업데이트된 스키마의 세부 정보를 반환합니다.

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 스키마 일부 업데이트 {#patch}

PATCH 요청을 사용하여 스키마의 일부를 업데이트할 수 있습니다. 다음 [!DNL Schema Registry] 는 다음을 포함한 모든 표준 JSON 패치 작업을 지원합니다 `add`, `remove`, 및 `replace`. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 [PUT 작업을 사용하여 스키마 바꾸기](#put).

가장 일반적인 PATCH 작업 중 하나에는 아래 예와 같이 이전에 정의한 필드 그룹을 스키마에 추가하는 작업이 포함됩니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | URL로 인코딩되어 있습니다 `$id` URI 또는 `meta:altId` 업데이트할 스키마 입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청에서는 해당 필드 그룹의 `$id` 값 모두를 `meta:extends` 및 `allOf` 배열

요청 본문은 배열 형식을 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 객체에는 수행할 작업이 포함됩니다(`op`)에서 작업을 수행해야 하는 필드(`path`) 및 해당 작업에 포함해야 하는 정보(`value`).

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**응답**

응답이 두 작업이 모두 성공적으로 수행되었음을 표시합니다. 필드 그룹 `$id` 이(가) `meta:extends` 배열 및 참조(`$ref`)을 필드 그룹에 추가합니다. `$id` 이제 다음 위치에 표시됩니다. `allOf` 배열입니다.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 실시간 고객 프로필에서 사용할 스키마 활성화 {#union}

스키마에 참여하기 위해 [실시간 고객 프로필](../../profile/home.md), 다음을 추가해야 합니다. `union` 태그에 태그 지정 `meta:immutableTags` 배열입니다. 해당 스키마에 대한 PATCH 요청을 수행하면 이 작업을 수행할 수 있습니다.

>[!IMPORTANT]
>
>변경할 수 없는 태그는 설정되지만 제거되지 않은 태그입니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | URL로 인코딩되어 있습니다 `$id` URI 또는 `meta:altId` 활성화하려는 스키마 중 하나입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청에는 `meta:immutableTags` 배열에 단일 문자열 값을 제공하는 기존 스키마에 배열 `union` 을 활성화하여 프로필에서 사용할 수 있습니다.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**응답**

성공적인 응답은 다음을 보여주는 업데이트된 스키마의 세부 정보를 반환합니다 `meta:immutableTags` 배열이 추가되었습니다.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

이제 이 스키마 클래스에 대한 결합을 보고 스키마의 필드가 표시되는지 확인할 수 있습니다. 자세한 내용은 [노조의 종단점 안내서](./unions.md) 추가 정보.

## 스키마 삭제 {#delete}

스키마 레지스트리에서 스키마를 제거해야 하는 경우가 가끔 있습니다. 이 작업은 경로에 제공된 스키마 ID로 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | URL로 인코딩되어 있습니다 `$id` URI 또는 `meta:altId` 삭제할 스키마 중 하나입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

스키마에 대한 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. 다음을 포함해야 합니다 `Accept` 헤더이지만 스키마 레지스트리에서 스키마가 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 수신해야 합니다.
