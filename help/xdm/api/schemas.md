---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;스키마;스키마;만들기
solution: Experience Platform
title: 스키마 API 엔드포인트
description: 스키마 레지스트리 API의 /schemas 끝점을 사용하면 experience 애플리케이션 내에서 XDM 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: dc5ac5427e1eeef47434c3974235a1900d29b085
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 3%

---

# 스키마 엔드포인트

스키마는 Adobe Experience Platform에 수집하려는 데이터에 대한 블루프린트로 간주할 수 있습니다. 각 스키마는 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. `/schemas` API의 [!DNL Schema Registry] 끝점을 사용하면 경험 응용 프로그램 내에서 스키마를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작

이 가이드에 사용된 API 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 스키마 목록 검색 {#list}

각각 `global` 또는 `tenant`에 GET 요청을 수행하여 `/global/schemas` 또는 `/tenant/schemas` 컨테이너에 모든 스키마를 나열할 수 있습니다.

>[!NOTE]
>
>리소스를 나열할 때 스키마 레지스트리는 결과 세트를 300개 항목으로 제한합니다. 이 제한을 초과하는 리소스를 반환하려면 페이징 매개 변수를 사용해야 합니다. 또한 추가 쿼리 매개 변수를 사용하여 결과를 필터링하고 반환되는 리소스 수를 줄이는 것이 좋습니다. 자세한 내용은 부록 문서의 [쿼리 매개 변수](./appendix.md#query)에 대한 섹션을 참조하십시오.

**API 형식**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 매개변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 스키마를 저장하는 컨테이너입니다. Adobe에서 만든 스키마의 경우 `global`, 조직에서 소유한 스키마의 경우 `tenant`. |
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 사용 가능한 매개 변수 목록은 [부록 문서](./appendix.md#query)를 참조하십시오. |

{style="table-layout:auto"}

**요청**

다음 요청은 `tenant` 쿼리 매개 변수를 사용하여 `orderby` 특성별로 결과를 정렬하여 `title` 컨테이너에서 스키마 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 스키마를 나열하는 데 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 만드는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본 `$ref` 및 `allOf`이(가) 포함된 각 리소스에 대해 전체 JSON 스키마를 반환합니다. (제한: 300) |

{style="table-layout:auto"}

**응답**

위의 요청에서 `application/vnd.adobe.xed-id+json` `Accept` 헤더를 사용했으므로 응답에는 각 스키마에 대한 `title`, `$id`, `meta:altId` 및 `version` 특성만 포함됩니다. 다른 `Accept` 헤더(`application/vnd.adobe.xed+json`)를 사용하면 각 스키마의 모든 특성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 `Accept` 헤더를 선택합니다.

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

경로에 스키마 ID를 포함하는 GET 요청을 수행하여 특정 스키마를 조회할 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 검색할 스키마를 저장하는 컨테이너입니다. Adobe에서 만든 스키마의 경우 `global`, 조직에서 소유한 스키마의 경우 `tenant`. |
| `{SCHEMA_ID}` | 조회할 스키마의 `meta:altId` 또는 URL로 인코딩된 `$id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 경로의 `meta:altId` 값으로 지정된 스키마를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 모든 조회 요청에는 `version` 헤더에 `Accept`이(가) 포함되어야 합니다. 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`이(가) 있는 Raw에 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 및 `allOf`이(가) 확인되었으며 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | `$ref` 및 `allOf`이(가) 포함된 원시 버전이며 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 및 `allOf`이(가) 해결되었습니다. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 및 `allOf` 해결됨, 설명자가 포함됨. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 및 `allOf`이(가) 확인되었으며 제목 및 설명이 있습니다. 사용되지 않는 필드는 `meta:status`의 `deprecated` 특성으로 표시됩니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 스키마의 세부 정보를 반환합니다. 반환되는 필드는 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 다른 `Accept` 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

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

스키마 작성 프로세스는 클래스를 할당함으로써 시작됩니다. 클래스는 데이터(레코드 또는 시계열)의 주요 행동 측면과 수집할 데이터를 설명하는 데 필요한 최소 필드를 정의합니다.

클래스 또는 필드 그룹 없이 스키마를 만드는 방법에 대한 지침(관계형 스키마)은 [관계형 스키마 만들기](#create-relational-schema) 섹션을 참조하십시오.

>[!NOTE]
>
>아래 예제 호출은 클래스의 최소 구성 요구 사항을 사용하고 필드 그룹을 포함하지 않고 API에서 스키마를 만드는 방법의 기본 예제일 뿐입니다. 필드 그룹 및 데이터 형식을 사용하여 필드를 할당하는 방법을 포함하여 API에서 스키마를 만드는 방법에 대한 전체 단계는 [스키마 만들기 자습서](../tutorials/create-schema-api.md)를 참조하십시오.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

요청의 `allOf`을(를) 참조하는 `$id` 특성이 포함되어 있어야 합니다. 이 속성은 스키마가 구현할 &quot;기본 클래스&quot;를 정의합니다. 이 예제에서 기본 클래스는 이전에 만든 &quot;Property Information&quot; 클래스입니다.

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
| `allOf` | 각 객체가 스키마가 구현하는 필드가 있는 클래스 또는 필드 그룹을 참조하는 객체의 배열입니다. 각 개체에는 새 스키마가 구현할 클래스 또는 필드 그룹의 `$ref`을(를) 나타내는 값을 가진 단일 속성(`$id`)이 있습니다. 추가 필드 그룹이 0개 이상인 하나의 클래스를 제공해야 합니다. 위의 예에서 `allOf` 배열의 단일 개체는 스키마의 클래스입니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 HTTP 상태 201(생성됨)과 `$id`, `meta:altId` 및 `version`을(를) 포함하여 새로 생성된 스키마의 세부 정보가 포함된 페이로드를 반환합니다. 이 값은 읽기 전용이며 [!DNL Schema Registry]에 의해 할당됩니다.

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

이제 테넌트 컨테이너에 [모든 스키마를 나열](#list)하기 위한 GET 요청을 수행하면 새 스키마가 포함됩니다. URL로 인코딩된 [&#x200B; URI를 사용하여 &#x200B;](#lookup)조회(GET) 요청`$id`을 수행하여 새 스키마를 직접 볼 수 있습니다.

스키마에 필드를 추가하려면 [PATCH 작업](#patch)을 수행하여 스키마의 `allOf` 및 `meta:extends` 배열에 필드 그룹을 추가할 수 있습니다.

## 관계 스키마 만들기 {#create-relational-schema}

>[!AVAILABILITY]
>
>Adobe Journey Optimizer **오케스트레이션된 캠페인** 라이선스 소유자는 Data Mirror 및 관계형 스키마를 사용할 수 있습니다. 또한 라이선스 및 기능 활성화에 따라 Customer Journey Analytics 사용자를 위한 **제한된 릴리스**(으)로도 사용할 수 있습니다. 액세스하려면 Adobe 담당자에게 문의하십시오.

>[!NOTE]
>
>이전 버전의 Adobe Experience Platform API 설명서에서는 관계형 스키마를 모델 기반 스키마라고 했습니다. 기능은 그대로 유지됩니다. 명확성을 위해 용어만 변경되었습니다.

`/schemas` 끝점에 대한 POST 요청을 수행하여 관계형 스키마를 만듭니다. 관계형 스키마는 **클래스 또는 필드 그룹 없이**&#x200B;구조화된 관계형 스타일 데이터를 저장합니다. 스키마에서 필드를 직접 정의하고 논리 비헤이비어 태그를 사용하여 스키마를 관계식으로 식별합니다.

>[!IMPORTANT]
>
>관계형 스키마를 만들려면 `meta:extends`을(를) `"https://ns.adobe.com/xdm/data/adhoc-v2"`(으)로 설정하십시오. **논리적 동작 식별자**&#x200B;입니다(실제 동작 또는 클래스가 아님). **에서 클래스 또는 필드 그룹을** not`allOf`참조하지 말고 **에서 클래스 또는 필드 그룹을** not`meta:extends`하세요.

먼저 `POST /tenant/schemas`을(를) 사용하여 스키마를 만듭니다. [설명자 API(`POST /tenant/descriptors`)](../api/descriptors.md)를 사용하여 필요한 설명자를 추가하십시오.

- [기본 키 설명자](../api/descriptors.md#primary-key-descriptor): 기본 키 필드는 **루트 수준**&#x200B;에 있어야 하며 **필요에 따라 표시**&#x200B;해야 합니다.
- 기본 키가 있는 경우 [버전 설명자](../api/descriptors.md#version-descriptor): **필수**.
- [관계 설명자](../api/descriptors.md#relationship-descriptor): 선택 사항이며 조인을 정의합니다. 수집 시 카디널리티가 적용되지 않습니다.
- [타임스탬프 설명자](../api/descriptors.md#timestamp-descriptor): 시계열 스키마의 경우 기본 키는 타임스탬프 필드를 포함하는 **합성** 키여야 합니다.

>[!NOTE]
>
>UI 스키마 편집기에서 버전 설명자와 타임스탬프 설명자가 각각 &quot;[!UICONTROL Version identifier]&quot; 및 &quot;[!UICONTROL Timestamp identifier]&quot;(으)로 표시됩니다.

>[!CAUTION]
>
>관계형 스키마가 **유니온 스키마와 호환되지 않습니다**. 관계형 스키마를 사용할 때는 `union` 태그를 `meta:immutableTags`에 적용하지 마십시오. 이 구성은 UI에서 차단되지만 현재 API에 의해 차단되지 않습니다. 유니온 스키마 동작에 대한 자세한 내용은 [유니온 끝점 안내서](./unions.md)를 참조하십시오.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

```shell
curl --request POST \
  --url https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
  "title": "marketing.customers",
  "type": "object",
  "description": "Schema of the Marketing Customers table.",
  "definitions": {
    "customFields": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "meta:xdmType": "object"
    }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record"
}
'
```

### 본문 속성 요청

| 속성 | 유형 | 설명 |
| ------------------------------- | ------ | --------------------------------------------------------- |
| `title` | 문자열 | 스키마의 표시 이름입니다. |
| `description` | 문자열 | 스키마의 목적에 대한 간략한 설명. |
| `type` | 문자열 | 관계형 스키마에 대해 `"object"`이어야 합니다. |
| `definitions` | 오브젝트 | 스키마 필드를 정의하는 루트 수준 개체를 포함합니다. |
| `definitions.<name>.properties` | 오브젝트 | 필드 이름 및 데이터 유형. |
| `allOf` | 배열 | 루트 수준 개체 정의를 참조합니다(예: `#/definitions/marketing_customers`). |
| `meta:extends` | 배열 | 관계형 스키마를 식별하려면 `"https://ns.adobe.com/xdm/data/adhoc-v2"`을(를) 포함해야 합니다. |
| `meta:behaviorType` | 문자열 | `"record"`(으)로 설정합니다. 적절하고 활성화된 경우에만 `"time-series"`을(를) 사용합니다. |

>[!IMPORTANT]
>
>관계형 스키마에 대한 스키마 진화는 표준 스키마와 동일한 추가 규칙을 따릅니다. PATCH 요청으로 새 필드를 추가할 수 있습니다. 데이터 집합에 데이터가 수집되지 않은 경우에만 필드 이름 변경 또는 제거와 같은 변경 내용이 허용됩니다.

**응답**

요청이 성공하면 **HTTP 201(생성됨)** 및 생성된 스키마가 반환됩니다.

>[!NOTE]
>
>관계형 스키마는 사전 시드된 필드(예: id, timestamp 또는 eventType)를 상속하지 않습니다. 스키마에서 모든 필수 필드를 명시적으로 정의합니다.

**응답 예**

```json
{
  "$id": "https://ns.adobe.com/<TENANT_ID>/schemas/<SCHEMA_UUID>",
  "meta:altId": "_<SCHEMA_ALT_ID>",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "marketing.customers",
  "description": "Schema of the Marketing Customers table.",
  "type": "object",
  "definitions": {
    "marketing_customers": {
      "type": "object",
      "properties": {
        "customer_id": {
          "title": "Customer ID",
          "description": "Primary key of the customer table.",
          "type": "string",
          "minLength": 1
        },
        "name": {
          "title": "Name",
          "description": "Name of the customer.",
          "type": "string"
        },
        "email": {
          "title": "Email",
          "description": "Email of the customer.",
          "type": "string",
          "format": "email",
          "minLength": 1
        }
      },
      "required": ["customer_id"]
    }
  },
  "allOf": [
    { "$ref": "#/definitions/marketing_customers" }
  ],
  "meta:extends": ["https://ns.adobe.com/xdm/data/adhoc-v2"],
  "meta:behaviorType": "record",
  "meta:containerId": "tenant"
}
```

### 응답 본문 속성

| 속성 | 유형 | 설명 |
| ------------------- | ------ | -------------------------- |
| `$id` | 문자열 | 생성된 스키마의 고유 URL. 후속 API 호출에 사용됩니다. |
| `meta:altId` | 문자열 | 스키마에 대한 대체 식별자. |
| `meta:resourceType` | 문자열 | 리소스 종류(항상 `"schemas"`). |
| `version` | 문자열 | 생성 시 할당된 스키마 버전. |
| `title` | 문자열 | 스키마의 표시 이름입니다. |
| `description` | 문자열 | 스키마의 목적에 대한 간략한 설명. |
| `type` | 문자열 | 스키마 유형. |
| `definitions` | 오브젝트 | 스키마에 사용되는 재사용 가능한 객체 또는 필드 그룹을 정의합니다. 일반적으로 기본 데이터 구조를 포함하며 스키마 루트를 정의하기 위해 `allOf` 배열에서 참조됩니다. |
| `allOf` | 배열 | 하나 이상의 정의를 참조하여 스키마의 루트 개체를 지정합니다(예: `#/definitions/marketing_customers`). |
| `meta:extends` | 배열 | 스키마를 관계형(`adhoc-v2`)으로 식별합니다. |
| `meta:behaviorType` | 문자열 | 동작 유형(`record` 또는 `time-series`(활성화된 경우). |
| `meta:containerId` | 문자열 | 스키마가 저장된 컨테이너입니다(예: `tenant`). |

필드를 만든 후 관계형 스키마에 필드를 추가하려면 [PATCH 요청](#patch)을 하세요. 관계형 스키마는 상속되거나 자동으로 발전하지 않습니다. 데이터 집합에 데이터가 수집되지 않은 경우에만 필드 이름 변경 또는 삭제와 같은 구조 변경이 허용됩니다. 데이터가 존재하면 **추가 변경**(예: 새 필드 추가)만 지원됩니다.

루트 정의 또는 루트 `properties` 내에 새 루트 수준 필드를 추가할 수 있지만 기존 필드의 제거, 이름 변경 또는 유형을 변경할 수는 없습니다.

>[!CAUTION]
>
>스키마를 사용하여 데이터 세트를 초기화하면 스키마 구현이 제한됩니다. 데이터가 수집되면 필드를 삭제하거나 수정할 수 없으므로 필드 이름과 유형을 미리 신중하게 계획하십시오.

## 스키마 업데이트 {#put}

PUT 작업을 통해 전체 스키마를 바꿀 수 있으며, 기본적으로 리소스를 다시 작성할 수 있습니다. PUT 요청을 통해 스키마를 업데이트할 때 본문에는 POST 요청에서 [새 스키마를 만들 때](#create)에 필요한 모든 필드가 포함되어야 합니다.

>[!NOTE]
>
>스키마의 일부를 완전히 바꾸는 대신 일부만 업데이트하려면 [스키마의 일부 업데이트](#patch)의 섹션을 참조하십시오.

**API 형식**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다시 쓸 스키마의 `meta:altId` 또는 URL로 인코딩된 `$id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 기존 스키마를 대체하여 `title`, `description` 및 `allOf` 특성을 변경합니다.

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

성공한 응답은 업데이트된 스키마의 세부 정보를 반환합니다.

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

## 스키마의 일부 업데이트 {#patch}

PATCH 요청을 사용하여 스키마의 일부를 업데이트할 수 있습니다. [!DNL Schema Registry]은(는) `add`, `remove` 및 `replace`을(를) 포함한 모든 표준 JSON 패치 작업을 지원합니다. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

>[!NOTE]
>
>개별 필드를 업데이트하는 대신 전체 리소스를 새 값으로 바꾸려면 [PUT 작업을 사용하여 스키마 바꾸기](#put)에 대한 섹션을 참조하십시오.

가장 일반적인 PATCH 작업 중 하나는 아래 예제에서 알 수 있듯이 이전에 정의된 필드 그룹을 스키마에 추가하는 것입니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 업데이트할 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`입니다. |

{style="table-layout:auto"}

**요청**

아래 예제 요청에서는 해당 필드 그룹의 `$id` 값을 `meta:extends` 및 `allOf` 배열 모두에 추가하여 스키마에 새 필드 그룹을 추가합니다.

요청 본문은 배열 형식을 취하며, 나열된 각 객체는 개별 필드에 대한 특정 변경 사항을 나타냅니다. 각 개체에는 수행할 작업(`op`), 작업을 수행할 필드(`path`) 및 해당 작업에 포함할 정보(`value`)가 포함됩니다.

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

응답은 두 작업이 모두 성공적으로 수행되었음을 보여 줍니다. 필드 그룹 `$id`이(가) `meta:extends` 배열에 추가되었으며 필드 그룹 `$ref`에 대한 참조(`$id`)가 이제 `allOf` 배열에 나타납니다.

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

스키마가 [실시간 고객 프로필](../../profile/home.md)에 참여하려면 스키마의 `union` 배열에 `meta:immutableTags` 태그를 추가해야 합니다. 해당 스키마에 대해 PATCH 요청을 수행하면 이를 수행할 수 있습니다.

>[!IMPORTANT]
>
>변경할 수 없는 태그는 설정되지만 제거하지 않는 태그입니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | URL로 인코딩된 `$id` URI 또는 활성화할 스키마의 `meta:altId`입니다. |

{style="table-layout:auto"}

**요청**

아래 예제 요청에서는 기존 스키마에 `meta:immutableTags` 배열을 추가하여 배열에 `union`의 단일 문자열 값을 제공하여 프로필에서 사용할 수 있도록 합니다.

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

성공한 응답은 업데이트된 스키마의 세부 정보를 반환하여 `meta:immutableTags` 배열이 추가되었음을 나타냅니다.

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

이제 이 스키마의 클래스에 대한 유니온을 보고 스키마의 필드가 표시되는지 확인할 수 있습니다. 자세한 내용은 [유니온 끝점 안내서](./unions.md)를 참조하십시오.

## 스키마 삭제 {#delete}

스키마 레지스트리에서 스키마를 제거해야 하는 경우가 있습니다. 이 작업은 경로에 제공된 스키마 ID로 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 삭제할 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`입니다. |

{style="table-layout:auto"}

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

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

스키마에 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. `Accept` 헤더를 요청에 포함해야 하지만 스키마가 스키마 레지스트리에서 제거되었기 때문에 HTTP 상태 404(찾을 수 없음)를 수신해야 합니다.
