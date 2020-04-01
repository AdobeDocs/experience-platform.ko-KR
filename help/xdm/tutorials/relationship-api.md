---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스키마 레지스트리 API를 사용하여 두 스키마 간의 관계 정의
topic: tutorials
translation-type: tm+mt
source-git-commit: 7e867ee12578f599c0c596decff126420a9aca01

---


# 스키마 레지스트리 API를 사용하여 두 스키마 간의 관계 정의


Adobe Experience Platform은 고객 간의 관계와 다양한 채널에서 브랜드와의 상호 작용을 파악하는 데 중요한 역할을 합니다. XDM(Experience Data Model) 스키마 구조 내에서 이러한 관계를 정의하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

이 문서에서는 스키마 레지스트리 API를 사용하여 조직에서 정의한 두 스키마 간의 일대일 관계를 정의하는 [자습서를 제공합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## 시작하기

이 자습서에서는 XDM(Experience Data Model) 및 XDM 시스템에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 설명서를 참조하십시오.

* [경험 플랫폼의 XDM 시스템](../home.md):XDM 및 Experience Platform의 구현에 대한 개요입니다.
   * [스키마 컴포지션의](../schema/composition.md)기본 사항:XDM 스키마 구축 블록 소개
* [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.
* [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이 자습서를 시작하기 전에 스키마 레지스트리 API를 성공적으로 호출하려면 [개발자 안내서를](../api/getting-started.md) 참조하십시오. 여기에는 사용자 `{TENANT_ID}`및 &quot;컨테이너&quot;의 개념, 요청을 수행하는 데 필요한 헤더가 포함됩니다(수락 헤더와 가능한 값에 특별히 주의).

## 소스 및 대상 스키마 정의 {#define-schemas}

관계에 정의될 두 개의 스키마를 이미 만들었어야 합니다. 이 자습서는 조직의 현재 로열티 프로그램(&quot;충성도 멤버&quot; 스키마에서 정의됨)의 멤버와 자주 사용하는 호텔(&quot;호텔&quot; 스키마에서 정의됨) 간의 관계를 만듭니다.

스키마 관계는 **대상 스키마** 내의 다른 필드를 참조하는 필드를 갖는 **소스 스키마로**&#x200B;표시됩니다. 다음 단계에서 &quot;충성도 멤버&quot;는 소스 스키마로, &quot;호텔&quot;은 대상 스키마로 작동합니다.

두 스키마 간의 관계를 정의하려면 먼저 두 스키마 모두에 대한 `$id` 값을 가져와야 합니다. 스키마의 표시 이름(`title`)을 알고 있는 경우 스키마 레지스트리 API의 `$id` 끝점에 GET 요청을 함으로써 해당 `/tenant/schemas` 값을 찾을 수 있습니다.

**API 형식**

```http
GET /tenant/schemas
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE] 승인 헤더는 결과 스키마의 제목, ID 및 버전만 `application/vnd.adobe.xed-id+json` 반환합니다.

**응답**

성공적인 응답은 조직에서 정의한 스키마 목록(예: 해당 스키마, `name``$id``meta:altId`및 `version`포함)을 반환합니다.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

관계를 정의할 두 스키마 `$id` 값을 기록합니다. 이러한 값은 이후 단계에서 사용됩니다.

## 두 스키마에 대한 참조 필드 정의

스키마 레지스트리 내에서 관계 설명자는 SQL 테이블의 외래 키와 비슷하게 작동합니다.소스 스키마의 필드는 대상 스키마의 필드에 대한 참조 역할을 합니다. 관계를 정의할 때 각 스키마에는 다른 스키마에 대한 참조로 사용할 전용 필드가 있어야 합니다.

>[!IMPORTANT] 실시간 고객 프로파일에서 스키마를 사용하도록 설정하려면 대상 [스키마에](../../profile/home.md)대한 참조 필드가 **기본 ID여야 합니다**. 이 자습서의 후반부에 자세히 설명되어 있습니다.

두 스키마에 이 용도로 사용할 필드가 없으면 새 필드로 믹싱을 만들어 스키마에 추가해야 할 수 있습니다. 이 새 필드에는 &quot;string&quot;의 `type` 값이 있어야 합니다.

이 자습서의 목적을 위해 대상 스키마 &quot;호텔&quot;에 이미 다음 목적을 위한 필드가 포함되어 있습니다. `hotelId`Adobe 그러나 소스 스키마 &quot;충성도 멤버&quot;에 해당 필드가 없으며, 해당 `favoriteHotel``TENANT_ID` 네임스페이스 아래에 새 필드를 추가하는 새 혼합이 제공되어야 합니다.

### 새로운 믹서 만들기

스키마에 새 필드를 추가하려면 먼저 혼합에서 정의해야 합니다. 종단점에 대한 POST 요청을 만들어 새 혼합을 만들 수 `/tenant/mixins` 있습니다.

**API 형식**

```http
POST /tenant/mixins
```

**요청**

다음 요청은 추가되는 스키마의 `favoriteHotel` `TENANT_ID` 네임스페이스 아래에 필드를 추가하는 새 혼합을 만듭니다.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**응답**

성공적인 응답은 새로 만든 믹스의 세부 사항을 반환합니다.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `$id` | 읽기 전용 시스템에서 새 혼합의 고유 식별자를 생성했습니다. URI 형식을 취합니다. |

소스 `$id` 스키마에 혼합을 추가하는 다음 단계에서 사용할 믹스의 URI를 기록합니다.

### 소스 스키마에 혼합 추가

믹싱을 만든 후에는 `/tenant/schemas/{SCHEMA_ID}` 끝점에 PATCH 요청을 만들어 소스 스키마에 추가할 수 있습니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | URL 인코딩 URI `$id` 또는 소스 `meta:altId` 스키마의 URL. |

**요청**

다음 요청에서는 &quot;Favorite Hotel&quot; 혼합을 &quot;Loyality Members&quot; 스키마에 추가합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| 속성 | 설명 |
| --- | --- |
| `op` | 수행할 패치 작업. 이 요청은 `add` 작업을 사용합니다. |
| `path` | 새 리소스를 추가할 스키마 필드의 경로입니다. 스키마에 혼합을 추가할 때는 값이 `/allOf/-`되어야 합니다. |
| `value.$ref` | 추가할 `$id` 믹스의 내용입니다. |

**응답**

성공적인 응답은 업데이트된 스키마의 세부 사항을 반환합니다. 이 세부 정보에는 `$ref` 배열 아래에 추가된 믹스의 `allOf` 값이 포함됩니다.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## 두 스키마에 대한 기본 ID 필드 정의

>[!NOTE] 이 단계는 실시간 고객 프로필에 사용할 수 있도록 활성화되는 스키마에만 [필요합니다](../../profile/home.md). 스키마에 스키마 참여를 원하지 않거나 스키마에 이미 기본 ID가 정의되어 있는 경우 대상 스키마에 대한 참조 ID 설명자를 [](#create-descriptor) 만드는 다음 단계로 건너뛸 수 있습니다.

실시간 고객 프로필에서 스키마를 사용하도록 설정하려면 기본 ID가 정의되어 있어야 합니다. 또한 관계의 대상 스키마는 기본 ID를 참조 필드로 사용해야 합니다.

이 자습서의 목적을 위해 소스 스키마에는 이미 기본 ID가 정의되어 있지만 대상 스키마는 정의되어 있지 않습니다. ID 설명자를 만들어 스키마 필드를 기본 ID 필드로 표시할 수 있습니다. 이 작업은 `/tenant/descriptors` 끝점에 POST 요청을 수행하여 수행됩니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 대상 스키마 &quot;호텔&quot;의 `hotelId` 필드를 기본 ID 필드로 정의하는 새 ID 설명자를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `@type` | 생성할 설명자 유형입니다. ID 설명자의 `@type` 값은 입니다 `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | `$id` 이전 단계에서 [](#define-schemas)얻은 대상 스키마의 값입니다. |
| `xdm:sourceVersion` | 스키마의 버전 번호입니다. |
| `sourceProperty` | 스키마의 기본 ID로 사용할 특정 필드의 경로입니다. 이 경로는 &quot;/&quot;로 시작하고 하나로 끝나지 않고 &quot;속성&quot; 네임스페이스도 제외해야 합니다. 예를 들어 위의 요청은 `/_{TENANT_ID}/hotelId` 대신 `/properties/_{TENANT_ID}/properties/hotelId`사용됩니다. |
| `xdm:namespace` | ID 필드의 ID 네임스페이스입니다. `hotelId` 는 이 예제에서 ECID 값이므로 &quot;ECID&quot; 네임스페이스가 사용됩니다. 사용 가능한 네임스페이스 목록은 [ID 네임스페이스 개요를](../../identity-service/home.md) 참조하십시오. |
| `xdm:isPrimary` | ID 필드가 스키마의 기본 ID가 될지 여부를 결정하는 부울 속성입니다. 이 요청은 기본 ID를 정의하므로 이 값은 true로 설정됩니다. |

**응답**

성공적인 응답은 새로 만든 ID 설명자의 세부 정보를 반환합니다.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## 참조 ID 설명자 만들기

스키마 필드가 관계의 다른 스키마에서 참조로 사용되는 경우 해당 스키마 필드에 참조 ID 설명자가 적용되어야 합니다. &quot;충성도 `favoriteHotel` 멤버&quot;의 필드는 &quot;호텔&quot;의 `hotelId` 필드를 참조하므로 참조 ID 설명자를 `hotelId` 제공해야 합니다.

종단점에 대한 POST 요청을 수행하여 대상 스키마에 대한 참조 설명자를 `/tenant/descriptors` 만듭니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 대상 스키마 &quot;Hotels&quot;의 `hotelId` 필드에 대한 참조 설명자를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID"
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `xdm:sourceSchema` | 대상 `$id` 스키마의 URL입니다. |
| `xdm:sourceVersion` | 대상 스키마의 버전 번호입니다. |
| `sourceProperty` | 대상 스키마의 기본 ID 필드에 대한 경로입니다. |
| `xdm:identityNamespace` | 참조 필드의 ID 네임스페이스입니다. `hotelId` 는 이 예제에서 ECID 값이므로 &quot;ECID&quot; 네임스페이스가 사용됩니다. 사용 가능한 네임스페이스 목록은 [ID 네임스페이스 개요를](../../identity-service/home.md) 참조하십시오. |

**응답**

성공적인 응답은 대상 스키마에 대해 새로 만든 참조 설명자의 세부 정보를 반환합니다.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 관계 설명자 만들기 {#create-descriptor}

관계 설명자는 소스 스키마와 대상 스키마 간에 일대일 관계를 설정합니다. 종단점에 대한 POST 요청을 수행하여 새 관계 설명자를 만들 수 `/tenant/descriptors` 있습니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 &quot;충성도 멤버&quot;를 소스 스키마로, &quot;기존 충성도 멤버&quot;를 대상 스키마로 사용하여 새 관계 설명자를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `@type` | 생성할 설명자 유형입니다. 관계 설명자의 `@type` 값은 입니다 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 소스 `$id` 스키마의 URL입니다. |
| `xdm:sourceVersion` | 소스 스키마의 버전 번호입니다. |
| `sourceProperty`: | 소스 스키마의 참조 필드에 대한 경로입니다. |
| `xdm:destinationSchema` | 대상 `$id` 스키마의 URL입니다. |
| `xdm:destinationVersion` | 대상 스키마의 버전 번호입니다. |
| `destinationProperty`: | 대상 스키마의 참조 필드에 대한 경로입니다. |

### 응답

성공적인 응답은 새로 만든 관계 설명자의 세부 정보를 반환합니다.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## 다음 단계

이 튜토리얼을 따라 두 스키마 간에 일대일 관계를 성공적으로 만들었습니다. 스키마 레지스트리 API를 사용한 설명자 작업에 대한 자세한 내용은 스키마 레지스트리 [개발자 안내서를](../api/getting-started.md)참조하십시오. UI에서 스키마 관계를 정의하는 방법에 대한 단계는 스키마 편집기를 사용하여 스키마 관계를 [정의하는 자습서를 참조하십시오](relationship-ui.md).