---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: 스키마 만들기
description: 스키마 레지스트리 API의 /schemas 끝점을 사용하면 경험 응용 프로그램 내에서 XDM 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 2%

---


# 스키마 끝점

스키마는 Adobe Experience Platform에 인제스트하려는 데이터의 청사진이라고 생각할 수 있습니다. 각 스키마는 클래스와 0개 이상의 혼합으로 구성됩니다. API의 `/schemas` 종단점을 사용하면 [!DNL Schema Registry] 경험 애플리케이션 내의 스키마를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에서 사용되는 API 끝점은 [[!DNL Schema Registry] API의 일부입니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml). 계속하기 전에 [시작하기 가이드](./getting-started.md) (관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서)와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 스키마 목록 검색 {#list}

GET을 각각 또는 `global` 로 요청하여 `tenant` 또는 `/global/schemas` 컨테이너 아래에 모든 스키마를 나열할 수 `/tenant/schemas`있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리는 결과 세트를 300개 항목으로 제한합니다. 이 제한을 넘는 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 또한 추가적인 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서의 [쿼리 매개 변수](./appendix.md#query) 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 스키마를 포함하는 컨테이너: `global` for Adobe 생성 스키마 또는 조직 `tenant` 이 소유한 스키마에 대해. |
| `{QUERY_PARAMS}` | 결과를 필터링하는 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록은 [부록 문서를](./appendix.md#query) 참조하십시오. |

**요청**

다음 요청은 쿼리 매개 변수를 사용하여 해당 `tenant` `orderby` `title` 속성별로 결과를 정렬하여 컨테이너에서 스키마 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다음 헤더는 스키마를 나열할 수 `Accept` 있습니다.

| `Accept` header | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원본 및 포함된 각 리소스에 대한 전체 JSON 스키마 `$ref` 를 `allOf` 반환합니다. (제한:300) |

**응답**

위의 요청에 `application/vnd.adobe.xed-id+json` 헤더가 사용되므로 응답에는 각 스키마에 대한 `Accept` , `title`및 `$id``meta:altId``version` 속성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 스키마의 모든 속성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

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

## 스키마 찾기 {#lookup}

경로에 스키마의 ID를 포함하는 GET 요청을 수행하여 특정 스키마를 찾을 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 스키마를 포함하는 컨테이너: `global` adobe에서 만든 스키마 또는 조직 `tenant` 이 소유한 스키마의 경우 |
| `{SCHEMA_ID}` | 조회하려는 스키마의 `meta:altId` 또는 URL 인코딩 `$id` . |

**요청**

다음 요청은 경로의 값으로 지정된 스키마를 `meta:altId` 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 모든 조회 요청은 헤더에 `version` 포함되어야 `Accept` 합니다. The following `Accept` headers are available:

| `Accept` header | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw 및 `$ref` 와 `allOf`함께 사용할 수 있으며 제목 및 설명이 포함되어 있습니다. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 그리고 `allOf` 해결되었습니다. 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 제목 또는 설명 `$ref` `allOf`이 없는 Raw |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 제목 또는 설명이 없는 문제를 `allOf` 해결했습니다. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 설명자가 포함된 `allOf` 문제를 해결했습니다. |

**응답**

성공적인 응답은 스키마의 세부 사항을 반환합니다. 반환되는 필드는 요청에 전송된 `Accept` 헤더에 따라 다릅니다. 다양한 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

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
  "imsOrg": "{IMS_ORG}",
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

스키마 구성 프로세스는 클래스를 할당하는 방식으로 시작됩니다. 이 클래스는 데이터(레코드 또는 시간 시리즈)의 주요 행동 측면과 인제스트할 데이터를 설명하는 데 필요한 최소 필드를 정의합니다.

>[!NOTE]
>
>아래 예제 호출은 클래스의 최소 구성 요구 사항과 믹신이 없는 API에서 스키마를 만드는 방법의 기본 예일 뿐입니다. 혼합과 데이터 형식을 사용하여 필드를 할당하는 방법을 포함하여 API에서 스키마를 만드는 방법에 대한 전체 단계는 [스키마 만들기 자습서를 참조하십시오](../tutorials/create-schema-api.md).

**API 형식**

```http
POST /tenant/schemas
```

**요청**

요청에는 클래스의 속성을 참조하는 `allOf` 속성 `$id` 이 포함되어야 합니다. 이 속성은 스키마가 구현할 &quot;기본 클래스&quot;를 정의합니다. 이 예에서 기본 클래스는 이전에 만든 &quot;속성 정보&quot; 클래스입니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `allOf` | 스키마 필드가 구현되는 클래스나 혼합을 참조하는 각 개체가 포함된 개체 배열 각 객체에는 새 스키마를 구현할 클래스 또는 믹스의 값`$ref``$id` 을 나타내는 단일 속성()이 포함됩니다. 0개 이상의 추가 혼합을 포함하여 하나의 클래스를 제공해야 합니다. 위의 예에서 배열의 단일 객체는 `allOf` 스키마의 클래스입니다. |

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과 새로 만든 스키마(예: `$id`, `meta:altId`및 `version`포함)의 세부 정보가 포함된 페이로드를 반환합니다. 이러한 값은 읽기 전용이며, [!DNL Schema Registry]

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
    "imsOrg": "{IMS_ORG}",
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

테넌트 컨테이너의 모든 스키마를 [나열하기 위한 GET 요청을](#list) 수행하면 이제 새 스키마가 포함됩니다. URL 인코딩 URI를 사용하여 [조회(GET) 요청을](#lookup) 수행하여 `$id` 새 스키마를 직접 볼 수 있습니다.

스키마에 필드를 추가하려면 [PATCH 작업을](#patch) 수행하여 스키마의 `allOf` 배열에 믹스를 추가할 수 `meta:extends` 있습니다.

## 스키마 업데이트 {#put}

PUT 작업을 통해 전체 스키마를 교체할 수 있으며, 기본적으로 리소스를 다시 작성할 수 있습니다. PUT 요청을 통해 스키마를 업데이트할 때 본문에는 POST 요청에 새 스키마를 [만들 때 필요한 모든](#create) 필드가 포함되어야 합니다.

>[!NOTE]
>
>전체 스키마 대신 스키마의 일부만 업데이트하려면 스키마 [의 부분 업데이트 섹션을 참조하십시오](#patch).

**API 형식**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다시 쓰려는 스키마의 `meta:altId` 또는 URL 인코딩 `$id` . |

**요청**

다음 요청은 기존 스키마를 대체하여 해당 스키마 `title`, `description`및 `allOf` 속성을 변경합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

## 스키마의 부분 업데이트 {#patch}

PATCH 요청을 사용하여 스키마의 일부를 업데이트할 수 있습니다. 이 [!DNL Schema Registry] 는 `add`, `remove`및 `replace`등 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서를 참조하십시오](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>개별 필드를 업데이트하지 않고 전체 리소스를 새 값으로 대체하려면 PUT 작업을 사용하여 스키마 [교체 섹션을 참조하십시오](#put).

가장 일반적인 PATCH 작업 중 하나는 아래 예제와 같이 이전에 정의된 혼합을 스키마에 추가하는 것입니다.

**API 형식**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 업데이트할 스키마의 URL 인코딩 `$id` URI `meta:altId` 입니다. |

**요청**

아래 예제 요청에서는 해당 혼합의 값을 배열과 배열 모두에 추가하여 새 혼합을 스키마에 `$id` `meta:extends` `allOf` 추가합니다.

요청 본문은 배열 형태를 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경을 나타냅니다. 각 객체에는 수행할 작업(`op`)과 작업을 수행할 필드(`path`)와 해당 작업에 포함되어야 하는 정보(`value`)가 포함됩니다.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

이 응답에는 두 작업이 성공적으로 수행되었음을 보여줍니다. 혼합이 배열 `$id` 에 추가되고 혼합에 대한 참조( `meta:extends` )가`$ref`이제 배열에 `$id` `allOf` 표시됩니다.

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
    "imsOrg": "{IMS_ORG}",
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

스키마를 [실시간 고객 프로필에](../../profile/home.md)참가하려면 `union` 스키마의 `meta:immutableTags` 배열에 태그를 추가해야 합니다. 문제의 스키마에 대한 PATCH 요청을 수행하여 이 작업을 수행할 수 있습니다.

>[!IMPORTANT]
>
>변경할 수 없는 태그는 설정하려 하지만 제거되지 않는 태그입니다.

**API 형식**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 활성화할 스키마의 URL 인코딩 `$id` URI `meta:altId` 입니다. |

**요청**

아래 예제 요청에서는 기존 스키마에 `meta:immutableTags` 배열을 추가하여 배열에 단일 문자열 값을 제공하여 Profile에서 사용할 수 있도록 `union` 합니다.

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

성공적인 응답으로 업데이트된 스키마의 세부 정보를 반환하여 배열이 추가되었음을 `meta:immutableTags` 표시합니다.

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
    "imsOrg": "{IMS_ORG}",
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

이제 이 스키마의 클래스에 대한 결합을 확인하여 스키마의 필드가 표현되어 있는지 확인할 수 있습니다. See the [unions endpoint guide](./unions.md) for more information.

## 스키마 삭제 {#delete}

스키마 레지스트리에서 스키마를 제거해야 하는 경우도 있습니다. 이는 경로에 제공된 스키마 ID를 사용하여 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 삭제할 스키마의 URL 인코딩 `$id` URI `meta:altId` 입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

스키마에 대한 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. 요청에 헤더를 포함해야 하지만 스키마 레지스트리에서 스키마가 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 받아야 합니다. `Accept`