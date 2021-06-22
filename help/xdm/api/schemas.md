---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;스키마;스키마 만들기
solution: Experience Platform
title: 스키마 API 끝점
description: 스키마 레지스트리 API의 /schema 종단점을 사용하면 경험 애플리케이션 내에서 XDM 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
topic-legacy: developer guide
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: e4bf5bb77ac4186b24580329699d74d653310d93
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 4%

---

# 스키마 끝점

스키마는 Adobe Experience Platform에 수집하려는 데이터의 블루프린트로 생각할 수 있습니다. 각 스키마는 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. [!DNL Schema Registry] API의 `/schemas` 종단점을 사용하면 경험 애플리케이션 내의 스키마를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작

이 안내서에 사용된 API 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

## 스키마 목록 검색 {#list}

각각 `/global/schemas` 또는 `/tenant/schemas`에 GET 요청을 하여 `global` 또는 `tenant` 컨테이너 아래에 모든 스키마를 나열할 수 있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리에서 결과를 300개 항목으로 제한합니다. 이 제한 이상의 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환된 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서에서 [쿼리 매개 변수](./appendix.md#query)의 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 스키마를 포함하는 컨테이너:Adobe 생성 스키마의 경우 `global`, 조직이 소유한 스키마의 경우 `tenant`. |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록에 대해서는 [부록 document](./appendix.md#query) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `tenant` 컨테이너에서 스키마 목록을 검색하여 `orderby` 쿼리 매개 변수를 사용하여 결과를 `title` 속성으로 정렬합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 스키마를 나열할 때 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이 포함된 각 리소스에 대한 전체 JSON 스키마를 반환합니다. (제한:300) |

{style=&quot;table-layout:auto&quot;}

**응답**

위의 요청에서 `application/vnd.adobe.xed-id+json` `Accept` 헤더를 사용하므로 응답에는 각 스키마에 대한 `title`, `$id`, `meta:altId` 및 `version` 속성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 스키마의 모든 특성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

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
| `{CONTAINER_ID}` | 검색할 스키마가 들어 있는 컨테이너입니다.Adobe이 만든 스키마의 경우 `global` 또는 조직이 소유한 스키마의 `tenant`. |
| `{SCHEMA_ID}` | 조회하려는 스키마의 `meta:altId` 또는 URL로 인코딩된 `$id`. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 경로의 `meta:altId` 값으로 지정된 스키마를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 모든 조회 요청에는 `Accept` 헤더에 `version`이 포함되어야 합니다. 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`이 있는 Raw에는 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 그리고  `allOf` 해결됨 에는 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | `$ref` 및 `allOf` 가 있는 원시 형식의 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 그리고  `allOf` 해결되었습니다. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 그리고  `allOf` 설명자가 포함된 문제가 해결되었습니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 스키마 세부 정보를 반환합니다. 반환되는 필드는 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다른 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인하십시오.

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

스키마 작성 프로세스는 클래스를 할당하여 시작됩니다. 이 클래스는 데이터의 주요 행동 측면(레코드 또는 시계열)과 수집할 데이터를 설명하는 데 필요한 최소 필드를 정의합니다.

>[!NOTE]
>
>아래 예제 호출은 클래스 및 필드 그룹이 없는 최소 구성 요구 사항을 사용하여 API에서 스키마를 만드는 방법의 기본 예일 뿐입니다. 필드 그룹 및 데이터 유형을 사용하여 필드를 할당하는 방법을 포함하여 API에서 스키마를 만드는 방법에 대한 전체 단계는 [스키마 만들기 자습서](../tutorials/create-schema-api.md)를 참조하십시오.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

요청에는 클래스의 `$id`을 참조하는 `allOf` 특성이 포함되어야 합니다. 이 속성은 스키마가 구현할 &quot;기본 클래스&quot;를 정의합니다. 이 예제에서 기본 클래스는 이전에 만든 &quot;속성 정보&quot; 클래스입니다.

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
| `allOf` | 각 객체가 스키마가 구현하는 클래스 또는 필드 그룹을 참조하는 객체 배열입니다. 각 객체에는 새 스키마가 구현할 클래스 또는 필드 그룹의 `$id`을 나타내는 단일 속성(`$ref`)이 포함되어 있습니다. 하나 이상의 추가 필드 그룹과 함께 클래스를 제공해야 합니다. 위의 예에서 `allOf` 배열의 단일 개체는 스키마의 클래스입니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적으로 응답하면 `$id`, `meta:altId` 및 `version`를 포함하여 새로 만든 스키마의 세부 정보가 들어 있는 페이로드 및 HTTP 상태 201(생성됨)이 반환됩니다. 이러한 값은 읽기 전용이며 [!DNL Schema Registry]에 의해 지정됩니다.

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

이제 임차인 컨테이너에 있는 모든 스키마](#list)에 대해 GET 요청을 수행하면 새 스키마가 포함됩니다. [ URL로 인코딩된 `$id` URI를 사용하여 [조회(GET) 요청](#lookup)을 수행하여 새 스키마를 직접 볼 수 있습니다.

스키마에 필드를 더 추가하려면 [PATCH 작업](#patch)을 수행하여 스키마의 `allOf` 및 `meta:extends` 배열에 필드 그룹을 추가할 수 있습니다.

## 스키마 업데이트 {#put}

기본적으로 리소스를 다시 작성하는 PUT 작업을 통해 전체 스키마를 바꿀 수 있습니다. PUT 요청을 통해 스키마를 업데이트할 때 본문에는 POST 요청에 [새 스키마](#create)를 만들 때 필요한 모든 필드가 포함되어야 합니다.

>[!NOTE]
>
>전체 스키마를 대체하지 않고 스키마의 일부만 업데이트하려면 [스키마](#patch)의 일부를 업데이트하는 섹션을 참조하십시오.

**API 형식**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다시 쓸 스키마의 `meta:altId` 또는 URL로 인코딩된 `$id`. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 기존 스키마를 대체하여 `title`, `description` 및 `allOf` 속성을 변경합니다.

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

## 스키마 일부 업데이트 {#patch}

PATCH 요청을 사용하여 스키마의 일부를 업데이트할 수 있습니다. [!DNL Schema Registry]은 `add`, `remove` 및 `replace`를 비롯한 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 대체하려면 [PUT 작업을 사용하여 스키마를 바꾸는 섹션을 참조하십시오](#put).

가장 일반적인 PATCH 작업 중 하나에는 아래 예와 같이 이전에 정의한 필드 그룹을 스키마에 추가하는 작업이 포함됩니다.

**API 형식**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 업데이트할 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청은 해당 필드 그룹의 `$id` 값을 `meta:extends` 배열과 `allOf` 배열 모두에 추가하여 스키마에 새 필드 그룹을 추가합니다.

요청 본문은 배열 형식을 취하며 나열된 각 개체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 개체에는 수행할 작업(`op`)이 포함되어 있으며, (`path`)에서 작업을 수행해야 하는 필드와 해당 작업에 포함해야 하는 정보가 포함됩니다(`value`).

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

응답이 두 작업이 모두 성공적으로 수행되었음을 표시합니다. 필드 그룹 `$id`이 `meta:extends` 배열에 추가되었으며 필드 그룹 `$id`에 대한 참조(`$ref`)가 이제 `allOf` 배열에 나타납니다.

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

스키마가 [실시간 고객 프로필](../../profile/home.md)에 참여하려면 `union` 태그를 스키마의 `meta:immutableTags` 배열에 추가해야 합니다. 해당 스키마에 대한 PATCH 요청을 수행하면 이 작업을 수행할 수 있습니다.

>[!IMPORTANT]
>
>변경할 수 없는 태그는 설정되지만 제거되지 않은 태그입니다.

**API 형식**

```http
PATCH /tenant/schema/{SCHEMA_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 활성화할 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청은 기존 스키마에 `meta:immutableTags` 배열을 추가하여 배열에 프로필에 사용할 수 있도록 `union` 단일 문자열 값을 제공합니다.

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

성공적으로 응답하면 업데이트된 스키마의 세부 정보가 반환되어 `meta:immutableTags` 배열이 추가되었음을 나타냅니다.

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

이제 이 스키마 클래스에 대한 결합을 보고 스키마의 필드가 표시되는지 확인할 수 있습니다. 자세한 내용은 [결합 끝점 안내서](./unions.md)를 참조하십시오.

## 스키마 삭제 {#delete}

스키마 레지스트리에서 스키마를 제거해야 하는 경우가 가끔 있습니다. 이 작업은 경로에 제공된 스키마 ID로 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 삭제할 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

{style=&quot;table-layout:auto&quot;}

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

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

스키마에 대한 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. 요청에 `Accept` 헤더를 포함해야 하지만 스키마가 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.
