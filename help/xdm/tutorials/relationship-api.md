---
keywords: Experience Platform;홈;인기 항목;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;관계;관계 설명자;관계 설명자;참조 ID;참조 ID
solution: Experience Platform
title: 스키마 레지스트리 API를 사용하여 두 스키마 간의 관계를 정의합니다.
description: 이 문서에서는 스키마 레지스트리 API를 사용하여 조직에서 정의한 2개의 스키마 간에 1대1 관계를 정의하는 자습서를 제공합니다.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 1%

---


# [!DNL Schema Registry] API를 사용하여 두 스키마 간의 관계를 정의합니다.

다양한 채널에서 고객과의 관계와 브랜드와의 상호 작용을 이해할 수 있는 기능은 Adobe Experience Platform에서 중요한 부분입니다. [!DNL Experience Data Model](XDM) 스키마 구조 내에서 이러한 관계를 정의하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

공용 스키마 및 [!DNL Real-time Customer Profile]을 사용하여 스키마 관계를 유추할 수 있지만 이는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속하는 두 스키마 간의 관계를 설정하려면 전용 관계 필드를 대상 스키마의 ID를 참조하는 소스 스키마에 추가해야 합니다.

이 문서에서는 [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)을 사용하여 조직에서 정의한 두 스키마 간의 1:1 관계를 정의하는 자습서를 제공합니다.

## 시작하기

이 자습서에서는 [!DNL Experience Data Model](XDM) 및 [!DNL XDM System]에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md):XDM 및 XDM 구현에 대한 개요입니다 [!DNL Experience Platform].
   * [스키마 컴포지션의 기본 사항](../schema/composition.md):XDM 스키마의 기본 블록 소개
* [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

이 자습서를 시작하기 전에 [!DNL Schema Registry] API를 성공적으로 호출하기 위해 알아야 할 중요한 정보는 [개발자 안내서](../api/getting-started.md)를 참조하십시오. 여기에는 `{TENANT_ID}`, &quot;컨테이너&quot; 개념 및 요청 시 필요한 헤더가 포함됩니다(특히 [!DNL Accept] 헤더와 가능한 값에 주의).

## 소스 및 대상 스키마 정의 {#define-schemas}

관계에 정의할 2개의 스키마를 이미 생성한 것으로 예상됩니다. 이 자습서는 조직의 현재 로열티 프로그램(&quot;[!DNL Loyalty Members]&quot; 스키마에 정의됨)의 구성원과 즐겨찾기 호텔(&quot;[!DNL Hotels]&quot; 스키마에 정의됨) 간의 관계를 만듭니다.

스키마 관계는 **대상 스키마** 내의 다른 필드를 참조하는 필드가 있는 **소스 스키마**&#x200B;로 표현됩니다. 다음 단계에서 &quot;[!DNL Loyalty Members]&quot;은 소스 스키마로, &quot;[!DNL Hotels]&quot;은 대상 스키마로 작동합니다.

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마 모두 기본 ID를 정의했고 [!DNL Real-time Customer Profile]에 대해 활성화되어야 합니다. 스키마 구성 방법에 대한 지침이 필요한 경우 스키마 만들기 자습서에서 [프로필](./create-schema-api.md#profile)에서 사용할 스키마 활성화 섹션을 참조하십시오.

두 스키마 간의 관계를 정의하려면 먼저 두 스키마 모두에 대해 `$id` 값을 가져와야 합니다. 스키마의 표시 이름(`title`)을 알고 있는 경우 [!DNL Schema Registry] API의 `/tenant/schemas` 끝점에 GET 요청을 하여 해당 `$id` 값을 찾을 수 있습니다.

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

>[!NOTE]
>
>[!DNL Accept] 헤더 `application/vnd.adobe.xed-id+json`는 결과 스키마의 제목, ID 및 버전만 반환합니다.

**응답**

성공적인 응답은 `name`, `$id`, `meta:altId` 및 `version`을(를) 포함하여 조직에서 정의한 스키마 목록을 반환합니다.

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

관계를 정의할 2개의 스키마의 `$id` 값을 기록합니다. 이러한 값은 이후 단계에서 사용됩니다.

## 소스 스키마에 대한 참조 필드 정의

[!DNL Schema Registry] 내에서 관계 설명자는 관계형 데이터베이스 테이블의 외래 키와 비슷하게 작동합니다.소스 스키마의 필드는 대상 스키마의 기본 ID 필드에 대한 참조로 사용됩니다. 소스 스키마에 이 용도로 사용할 필드가 없으면 새 필드로 믹싱을 만들어 스키마에 추가해야 할 수 있습니다. 이 새 필드에는 &quot;[!DNL string]&quot;의 `type` 값이 있어야 합니다.

>[!IMPORTANT]
>
>대상 스키마와 달리 소스 스키마는 기본 ID를 참조 필드로 사용할 수 없습니다.

이 자습서에서는 대상 스키마 &quot;[!DNL Hotels]&quot;에 스키마의 기본 ID로 사용되는 `hotelId` 필드가 포함되어 있으므로 참조 필드로도 작동합니다. 그러나 소스 스키마 &quot;[!DNL Loyalty Members]&quot;에 참조로 사용할 전용 필드가 없으므로 새 필드를 스키마에 추가하는 새 믹신이 주어져야 합니다.`favoriteHotel`.

>[!NOTE]
>
>소스 스키마에 참조 필드로 사용할 전용 필드가 이미 있는 경우 [참조 설명자](#reference-identity)를 만드는 단계를 건너뛸 수 있습니다.

### 새 믹서 만들기

스키마에 새 필드를 추가하려면 먼저 혼합에서 정의해야 합니다. `/tenant/mixins` 끝점에 POST 요청을 하여 새 믹싱을 만들 수 있습니다.

**API 형식**

```http
POST /tenant/mixins
```

**요청**

다음 요청은 새로 추가되는 스키마의 `_{TENANT_ID}` 네임스페이스 아래에 `favoriteHotel` 필드를 추가하는 새 믹스를 만듭니다.

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

성공적인 응답은 새로 만든 믹싱의 세부 정보를 반환합니다.

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
| `$id` | 읽기 전용 시스템에서 새 혼합의 고유 식별자를 생성했습니다. URI 형식을 사용합니다. |

소스 스키마에 혼합을 추가하는 다음 단계에서 사용할 믹신의 `$id` URI를 기록합니다.

### 소스 스키마에 믹싱 추가

믹싱을 만든 후에는 `/tenant/schemas/{SCHEMA_ID}` 끝점에 PATCH 요청을 하여 소스 스키마에 추가할 수 있습니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 소스 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`. |

**요청**

다음 요청은 &quot;[!DNL Favorite Hotel]&quot; 믹싱을 &quot;[!DNL Loyalty Members]&quot; 스키마에 추가합니다.

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
| `op` | 수행할 PATCH 작업입니다. 이 요청은 `add` 작업을 사용합니다. |
| `path` | 새 리소스를 추가할 스키마 필드의 경로입니다. 스키마에 혼합을 추가할 때 값은 &quot;/allOf/-&quot;여야 합니다. |
| `value.$ref` | 추가할 혼합의 `$id`. |

**응답**

성공적인 응답은 업데이트된 스키마의 세부 정보를 반환합니다. 이 세부 정보에는 이제 `allOf` 배열 아래에 추가된 믹스의 `$ref` 값이 포함됩니다.

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

## 참조 ID 설명자 {#reference-identity} 만들기

스키마 필드가 관계의 다른 스키마에서 참조로 사용되는 경우 스키마 필드에 참조 ID 설명자가 적용되어야 합니다. &quot;[!DNL Loyalty Members]&quot;의 `favoriteHotel` 필드가 &quot;[!DNL Hotels]&quot;의 `hotelId` 필드를 참조하므로 `hotelId`에 참조 ID 설명자가 있어야 합니다.

`/tenant/descriptors` 끝점에 POST 요청을 하여 대상 스키마에 대한 참조 설명자를 만듭니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 대상 스키마 &quot;[!DNL Hotels]&quot;에 있는 `hotelId` 필드에 대한 참조 설명자를 만듭니다.

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
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| 매개 변수 | 설명 |
| --- | --- |
| `@type` | 정의할 설명자 유형입니다. 참조 설명자의 경우 값은 &quot;xdm:descriptorReferenceIdentity&quot;여야 합니다. |
| `xdm:sourceSchema` | 대상 스키마의 `$id` URL. |
| `xdm:sourceVersion` | 대상 스키마의 버전 번호입니다. |
| `sourceProperty` | 대상 스키마의 기본 ID 필드에 대한 경로입니다. |
| `xdm:identityNamespace` | 참조 필드의 ID 네임스페이스입니다. 이 네임스페이스는 스키마의 기본 ID로 필드를 정의할 때 사용되는 네임스페이스와 같아야 합니다. 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/home.md)를 참조하십시오. |

**응답**

성공적인 응답은 대상 스키마에 대해 새로 만든 참조 설명자의 세부 정보를 반환합니다.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 관계 설명자 {#create-descriptor} 만들기

관계 설명자는 소스 스키마와 대상 스키마 간에 일대일 관계를 설정합니다. 대상 스키마에 대한 참조 설명자를 정의한 후에는 `/tenant/descriptors` 끝점에 POST 요청을 수행하여 새 관계 설명자를 만들 수 있습니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 &quot;[!DNL Loyalty Members]&quot;을 소스 스키마로, &quot;[!DNL Legacy Loyalty Members]&quot;을 대상 스키마로 사용하는 새 관계 설명자를 만듭니다.

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
| `@type` | 생성할 설명자 유형입니다. 관계 설명자에 대한 `@type` 값은 &quot;xdm:descriptorOneToOne&quot;입니다. |
| `xdm:sourceSchema` | 소스 스키마의 `$id` URL. |
| `xdm:sourceVersion` | 소스 스키마의 버전 번호입니다. |
| `xdm:sourceProperty` | 소스 스키마의 참조 필드에 대한 경로입니다. |
| `xdm:destinationSchema` | 대상 스키마의 `$id` URL. |
| `xdm:destinationVersion` | 대상 스키마의 버전 번호입니다. |
| `xdm:destinationProperty` | 대상 스키마의 참조 필드에 대한 경로입니다. |

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

이 튜토리얼을 따라 두 스키마 간에 1:1 관계를 성공적으로 만들었습니다. [!DNL Schema Registry] API를 사용하는 설명자 작업에 대한 자세한 내용은 [스키마 레지스트리 개발자 안내서](../api/descriptors.md)를 참조하십시오. UI에서 스키마 관계를 정의하는 방법에 대한 단계는 [스키마 편집기](relationship-ui.md)를 사용하여 스키마 관계 정의에 대한 자습서를 참조하십시오.
