---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;스키마;관계;관계 설명자;관계 설명자;참조 ID;참조 ID;
title: 스키마 레지스트리 API를 사용하여 두 스키마 간의 관계 정의
description: 이 문서에서는 스키마 레지스트리 API를 사용하여 조직에서 정의한 두 스키마 간의 일대일 관계를 정의하는 자습서를 제공합니다.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 1%

---

# [!DNL Schema Registry] API를 사용하여 두 스키마 간의 관계 정의

Adobe Experience Platform에서는 다양한 채널에서 고객과 브랜드와의 상호 작용 간의 관계를 이해하는 기능이 중요합니다. [!DNL Experience Data Model]&#x200B;(XDM) 스키마 구조 내에서 이러한 관계를 정의하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

유니온 스키마와 [!DNL Real-Time Customer Profile]을(를) 사용하여 스키마 관계를 유추할 수 있지만 이는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속하는 두 스키마 간의 관계를 설정하려면 별도의 **참조 스키마**&#x200B;의 ID를 나타내는 **소스 스키마**&#x200B;에 전용 관계 필드를 추가해야 합니다.

>[!NOTE]
>
>스키마 레지스트리 API가 참조 스키마를 &quot;대상 스키마&quot;로 참조합니다. [데이터 준비 매핑 집합](../../data-prep/mapping-set.md)의 대상 스키마 또는 [대상 연결](../../destinations/home.md)에 대한 스키마와 혼동하지 마십시오.

이 문서에서는 [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)을(를) 사용하여 조직에서 정의한 두 스키마 간의 일대일 관계를 정의하는 자습서를 제공합니다.

## 시작하기

이 자습서에서는 [!DNL Experience Data Model]&#x200B;(XDM) 및 [!DNL XDM System]을(를) 이해하고 있어야 합니다. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md): XDM 및 [!DNL Experience Platform]의 구현에 대한 개요입니다.
   * [스키마 컴포지션 기본 사항](../schema/composition.md): XDM 스키마 빌딩 블록 소개.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

이 자습서를 시작하기 전에 [개발자 안내서](../api/getting-started.md)에서 [!DNL Schema Registry] API를 성공적으로 호출하기 위해 알아야 할 중요한 정보를 검토하십시오. 여기에는 `{TENANT_ID}`, &quot;컨테이너&quot; 개념 및 요청을 하는 데 필요한 헤더가 포함됩니다([!DNL Accept] 헤더 및 가능한 값에 특별한 주의를 기울임).

## 소스 및 참조 스키마 정의 {#define-schemas}

관계에 정의될 두 개의 스키마를 이미 생성했을 것으로 예상됩니다. 이 자습서에서는 조직의 현재 충성도 프로그램(&quot;[!DNL Loyalty Members]&quot; 스키마에 정의됨) 구성원과 즐겨 찾는 호텔(&quot;[!DNL Hotels]&quot; 스키마에 정의됨) 간의 관계를 만듭니다.

스키마 관계는 **참조 스키마** 내의 다른 필드를 참조하는 필드가 있는 **소스 스키마**&#x200B;로 표시됩니다. 다음 단계에서 &quot;[!DNL Loyalty Members]&quot;은(는) 소스 스키마가 되고 &quot;[!DNL Hotels]&quot;은(는) 참조 스키마로 작동합니다.

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마에 기본 ID가 정의되어 있어야 하며 [!DNL Real-Time Customer Profile]에 대해 사용할 수 있어야 합니다. 스키마를 적절하게 구성하는 방법에 대한 지침이 필요한 경우 스키마 만들기 자습서에서 [프로필에 사용할 스키마 활성화](./create-schema-api.md#profile)에 대한 섹션을 참조하십시오.

두 스키마 간의 관계를 정의하려면 먼저 두 스키마에 대한 `$id` 값을 얻어야 합니다. 스키마의 표시 이름(`title`)을 알고 있는 경우 [!DNL Schema Registry] API의 `/tenant/schemas` 끝점에 대한 GET 요청을 수행하여 해당 `$id` 값을 찾을 수 있습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>[!DNL Accept] 헤더 `application/vnd.adobe.xed-id+json`은(는) 결과 스키마의 제목, ID 및 버전만 반환합니다.

**응답**

응답이 성공하면 조직에서 정의한 스키마 목록(예: `name`, `$id`, `meta:altId` 및 `version`)이 반환됩니다.

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

관계를 정의할 두 스키마의 `$id` 값을 기록합니다. 이 값은 이후 단계에서 사용됩니다.

## 소스 스키마에 대한 참조 필드 정의

[!DNL Schema Registry] 내에서 관계 설명자는 관계형 데이터베이스 테이블의 외래 키와 유사하게 작동합니다. 소스 스키마의 필드는 참조 스키마의 기본 ID 필드에 대한 참조로 사용됩니다. 소스 스키마에 이 용도로 사용할 필드가 없는 경우 새 필드로 스키마 필드 그룹을 만들고 스키마에 추가해야 할 수 있습니다. 이 새 필드에는 `type` 값 `string`이(가) 있어야 합니다.

>[!IMPORTANT]
>
>소스 스키마는 기본 ID를 참조 필드로 사용할 수 없습니다.

이 자습서에서 참조 스키마 &quot;[!DNL Hotels]&quot;에는 스키마의 기본 ID 역할을 하는 `hotelId` 필드가 포함되어 있습니다. 그러나 원본 스키마 &quot;[!DNL Loyalty Members]&quot;에는 `hotelId`에 대한 참조로 사용할 전용 필드가 없으므로 스키마에 새 필드를 추가하려면 사용자 지정 필드 그룹을 만들어야 합니다. `favoriteHotel`.

>[!NOTE]
>
>소스 스키마에 참조 필드로 사용할 전용 필드가 이미 있는 경우 [참조 설명자 만들기](#reference-identity)의 단계로 건너뛸 수 있습니다.

### 새 필드 그룹 만들기

스키마에 새 필드를 추가하려면 먼저 필드 그룹에서 정의해야 합니다. `/tenant/fieldgroups` 끝점에 대한 POST 요청을 수행하여 새 필드 그룹을 만들 수 있습니다.

**API 형식**

```http
POST /tenant/fieldgroups
```

**요청**

다음 요청은 추가되는 스키마의 `_{TENANT_ID}` 네임스페이스 아래에 `favoriteHotel` 필드를 추가하는 새 필드 그룹을 만듭니다.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
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

응답이 성공하면 새로 만든 필드 그룹의 세부 정보가 반환됩니다.

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
    "description": "Favorite hotel field group for the Loyalty Members schema.",
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
| `$id` | 시스템이 새 필드 그룹의 읽기 전용 고유 식별자입니다. URI 형식을 사용합니다. |

{style="table-layout:auto"}

소스 스키마에 필드 그룹을 추가하는 다음 단계에서 사용할 필드 그룹의 `$id` URI를 기록하십시오.

### 소스 스키마에 필드 그룹 추가

필드 그룹을 만든 후에는 `/tenant/schemas/{SCHEMA_ID}` 끝점에 PATCH 요청을 만들어 소스 스키마에 추가할 수 있습니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 소스 스키마의 URL 인코딩 `$id` URI 또는 `meta:altId`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 &quot;[!DNL Favorite Hotel]&quot; 필드 그룹을 &quot;[!DNL Loyalty Members]&quot; 스키마에 추가합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | 새 리소스를 추가할 스키마 필드의 경로. 스키마에 필드 그룹을 추가할 때 값은 &quot;/allOf/-&quot;여야 합니다. |
| `value.$ref` | 추가할 필드 그룹의 `$id`입니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 업데이트된 스키마의 세부 정보를 반환합니다. 여기에는 이제 `allOf` 배열 아래에 추가된 필드 그룹의 `$ref` 값이 포함됩니다.

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
    "imsOrg": "{ORG_ID}",
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

## 참조 ID 설명자 만들기 {#reference-identity}

스키마 필드는 관계에서 다른 스키마에 대한 참조로 사용되는 경우 해당 필드에 참조 ID 설명자가 적용되어야 합니다. &quot;[!DNL Loyalty Members]&quot;의 `favoriteHotel` 필드가 &quot;[!DNL Hotels]&quot;의 `hotelId` 필드를 참조하므로 `favoriteHotel`에 참조 ID 설명자를 지정해야 합니다.

`/tenant/descriptors` 끝점에 대한 POST 요청을 수행하여 소스 스키마에 대한 참조 설명자를 만듭니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 소스 스키마 &quot;[!DNL Loyalty Members]&quot;의 `favoriteHotel` 필드에 대한 참조 설명자를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| 매개변수 | 설명 |
| --- | --- |
| `@type` | 정의 중인 설명자 유형. 참조 설명자의 경우 값은 `xdm:descriptorReferenceIdentity`이어야 합니다. |
| `xdm:sourceSchema` | 소스 스키마의 `$id` URL입니다. |
| `xdm:sourceVersion` | 소스 스키마의 버전 번호입니다. |
| `sourceProperty` | 참조 스키마의 기본 ID를 참조하는 데 사용할 소스 스키마 필드의 경로. |
| `xdm:identityNamespace` | 참조 필드의 ID 네임스페이스. 참조 스키마의 기본 ID와 동일한 네임스페이스여야 합니다. 자세한 내용은 [ID 네임스페이스 개요](../../identity-service/home.md)를 참조하십시오. |

{style="table-layout:auto"}

**응답**

성공한 응답은 소스 필드에 대해 새로 생성된 참조 설명자의 세부 정보를 반환합니다.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 관계 설명자 만들기 {#create-descriptor}

관계 설명자는 소스 스키마와 참조 스키마 간의 일대일 관계를 설정합니다. 소스 스키마의 해당 필드에 대한 참조 ID 설명자를 정의한 후에는 `/tenant/descriptors` 끝점에 대한 POST 요청을 수행하여 새 관계 설명자를 만들 수 있습니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 &quot;[!DNL Loyalty Members]&quot;을(를) 소스 스키마로 사용하고 &quot;[!DNL Hotels]&quot;을(를) 참조 스키마로 사용하는 새 관계 설명자를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

| 매개변수 | 설명 |
| --- | --- |
| `@type` | 생성할 설명자 유형. 관계 설명자의 `@type` 값은 `xdm:descriptorOneToOne`입니다. |
| `xdm:sourceSchema` | 소스 스키마의 `$id` URL입니다. |
| `xdm:sourceVersion` | 소스 스키마의 버전 번호입니다. |
| `xdm:sourceProperty` | 소스 스키마의 참조 필드 경로. |
| `xdm:destinationSchema` | 참조 스키마의 `$id` URL. |
| `xdm:destinationVersion` | 참조 스키마의 버전 번호입니다. |
| `xdm:destinationProperty` | 참조 스키마의 기본 ID 필드 경로. |

{style="table-layout:auto"}

### 응답

성공한 응답은 새로 생성된 관계 설명자의 세부 정보를 반환합니다.

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

이 자습서에 따라 두 스키마 간의 일대일 관계를 생성했습니다. [!DNL Schema Registry] API를 사용하여 설명자를 사용하는 방법에 대한 자세한 내용은 [스키마 레지스트리 개발자 안내서](../api/descriptors.md)를 참조하십시오. UI에서 스키마 관계를 정의하는 방법에 대한 단계는 [스키마 편집기를 사용하여 스키마 관계 정의](relationship-ui.md)에 대한 자습서를 참조하십시오.
