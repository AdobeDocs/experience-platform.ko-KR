---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;스키마;스키마;스키마;관계;관계;관계 설명자;관계 설명자;참조 ID;참조 ID;
title: 스키마 레지스트리 API를 사용하여 두 스키마 간의 관계를 정의합니다.
description: 이 문서에서는 스키마 레지스트리 API를 사용하여 조직에서 정의한 두 스키마 간에 일대일 관계를 정의하는 자습서를 제공합니다.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 2%

---

# 를 사용하여 두 스키마 간의 관계를 정의합니다 [!DNL Schema Registry] API

다양한 채널에서 고객과의 관계와 브랜드와의 상호 작용을 파악하는 기능은 Adobe Experience Platform의 중요한 부분입니다. 구조 내에서 이러한 관계 정의 [!DNL Experience Data Model] (XDM) 스키마를 사용하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다.

스키마 관계는 결합 스키마 및 [!DNL Real-Time Customer Profile]이는 동일한 클래스를 공유하는 스키마에만 적용됩니다. 다른 클래스에 속한 두 스키마 간의 관계를 설정하려면 전용 관계 필드를 **소스 스키마**- 별도의 **참조 스키마**.

>[!NOTE]
>
>스키마 레지스트리 API는 참조 스키마를 &quot;대상 스키마&quot;로 참조합니다. 이러한 스키마는 의 대상 스키마와 혼동하지 않습니다 [데이터 준비 매핑 세트](../../data-prep/mapping-set.md) 또는 스키마 [대상 연결](../../destinations/home.md).

이 문서에서는 다음을 사용하여 조직에서 정의한 두 스키마 간의 일대일 관계를 정의하는 자습서를 제공합니다 [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 시작하기

이 자습서에서는 을(를) 제대로 이해하고 있어야 합니다 [!DNL Experience Data Model] (XDM) 및 [!DNL XDM System]. 이 자습서를 시작하기 전에 다음 설명서를 검토하십시오.

* [Experience Platform의 XDM 시스템](../home.md): XDM 및 의 구현에 대한 개요입니다 [!DNL Experience Platform].
   * [스키마 작성 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소 소개.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

이 자습서를 시작하기 전에 [개발자 안내서](../api/getting-started.md) 를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보 [!DNL Schema Registry] API. 여기에는 다음이 포함됩니다 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청을 수행하는 데 필요한 헤더입니다(에는 [!DNL Accept] 헤더 및 가능한 값).

## 소스 및 참조 스키마 정의 {#define-schemas}

이미 관계에 정의될 두 개의 스키마를 생성한 것으로 예상됩니다. 이 자습서에서는 조직의 현재 충성도 프로그램(&quot;에 정의됨)의 멤버 간에 관계를 만듭니다[!DNL Loyalty Members]&quot; 스키마) 및 해당 즐겨찾기 호텔([!DNL Hotels]&quot; 스키마)를 만듭니다.

스키마 관계는 **소스 스키마** 다음 위치에서 다른 필드를 참조하는 필드 사용 **참조 스키마**. 다음에 나오는 단계에서, &quot;[!DNL Loyalty Members]&quot; 은 소스 스키마이고 &quot;[!DNL Hotels]는 참조 스키마 역할을 합니다.

>[!IMPORTANT]
>
>관계를 설정하려면 두 스키마에 기본 ID가 정의되어 있어야 하며 [!DNL Real-Time Customer Profile]. 의 섹션을 참조하십시오. [프로필에서 사용할 스키마 활성화](./create-schema-api.md#profile) 스키마 만들기 자습서에서 스키마를 구성하는 방법에 대한 지침이 필요한 경우 스키마 만들기 자습서에서 를 참조하십시오.

두 스키마 간의 관계를 정의하려면 먼저 를 획득해야 합니다 `$id` 두 스키마 값. 표시 이름(`title`) 스키마를 찾을 수 있습니다 `$id` 에 GET 요청을 수행하여 값을 `/tenant/schemas` 의 엔드포인트 [!DNL Schema Registry] API.

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
>다음 [!DNL Accept] 헤더 `application/vnd.adobe.xed-id+json` 결과 스키마의 제목, ID 및 버전만 반환합니다.

**응답**

성공적인 응답은 조직에서 정의한 스키마 목록(예: 해당 스키마)을 반환합니다 `name`, `$id`, `meta:altId`, 및 `version`.

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

레코드 `$id` 관계를 정의하려는 두 스키마 값. 이러한 값은 이후 단계에서 사용됩니다.

## 소스 스키마에 대한 참조 필드 정의

내 [!DNL Schema Registry], 관계 설명자는 관계형 데이터베이스 테이블의 외래 키와 비슷하게 작동합니다. 소스 스키마의 필드는 참조 스키마의 기본 id 필드에 대한 참조 역할을 합니다. 소스 스키마에 이러한 용도로 사용할 필드가 없는 경우, 새 필드로 스키마 필드 그룹을 만들어 스키마에 추가해야 할 수 있습니다. 이 새 필드에는 `type` 값 `string`.

>[!IMPORTANT]
>
>소스 스키마는 기본 ID를 참조 필드로 사용할 수 없습니다.

이 자습서에서는 참조 스키마 &quot;[!DNL Hotels]&quot;에 가 포함되어 있습니다 `hotelId` 스키마의 기본 id로 사용되는 필드입니다. 그러나 소스 스키마 &quot;[!DNL Loyalty Members]&quot;에 대한 참조로 사용할 전용 필드가 없습니다 `hotelId`를 지정하는 경우, 스키마에 새 필드를 추가하려면 사용자 지정 필드 그룹을 만들어야 합니다. `favoriteHotel`.

>[!NOTE]
>
>소스 스키마에 참조 필드로 사용할 전용 필드가 이미 있는 경우, 단계를 건너뛸 수 있습니다 [참조 설명자 만들기](#reference-identity).

### 새 필드 그룹 만들기

스키마에 새 필드를 추가하려면 먼저 필드 그룹에서 정의해야 합니다. 에 POST 요청을 만들어 새 필드 그룹을 만들 수 있습니다 `/tenant/fieldgroups` 엔드포인트.

**API 형식**

```http
POST /tenant/fieldgroups
```

**요청**

다음 요청은 를 추가하는 새 필드 그룹을 만듭니다 `favoriteHotel` 아래의 필드 `_{TENANT_ID}` 가 추가되는 모든 스키마의 네임스페이스입니다.

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

성공적인 응답은 새로 만든 필드 그룹의 세부 정보를 반환합니다.

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
| `$id` | 읽기 전용 시스템에서 새 필드 그룹의 고유 식별자를 생성했습니다. URI 형식을 취합니다. |

{style=&quot;table-layout:auto&quot;}

레코드 `$id` 소스 스키마에 필드 그룹을 추가하는 다음 단계에서 사용할 필드 그룹의 URI입니다.

### 소스 스키마에 필드 그룹 추가

필드 그룹을 만든 후에는 필드에 PATCH 요청을 수행하여 소스 스키마에 추가할 수 있습니다 `/tenant/schemas/{SCHEMA_ID}` 엔드포인트.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | URL로 인코딩되어 있습니다 `$id` URI 또는 `meta:altId` 소스 스키마 중 하나입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 &quot;[!DNL Favorite Hotel]&quot; 필드 그룹을 &quot;[!DNL Loyalty Members]&quot; 스키마.

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
| `op` | 수행할 PATCH 작업입니다. 이 요청에서는 `add` 작업. |
| `path` | 새 리소스를 추가할 스키마 필드의 경로입니다. 필드 그룹을 스키마에 추가할 때 값은 &quot;/allOf/-&quot;여야 합니다. |
| `value.$ref` | 다음 `$id` 추가할 필드 그룹의 이름입니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 이제 다음을 포함하는 업데이트된 스키마의 세부 정보를 반환합니다 `$ref` 아래에 추가된 필드 그룹의 값 `allOf` 배열입니다.

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

스키마 필드가 관계의 다른 스키마에 대한 참조로 사용되는 경우 해당 스키마에 적용된 참조 ID 설명자가 있어야 합니다. 다음 이후 `favoriteHotel` 필드의 &quot;[!DNL Loyalty Members]&quot; `hotelId` 필드의 &quot;[!DNL Hotels]&quot;, `favoriteHotel` 참조 ID 설명자를 제공해야 합니다.

에 POST 요청을 수행하여 소스 스키마에 대한 참조 설명자를 만듭니다. `/tenant/descriptors` 엔드포인트.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청에서는 `favoriteHotel` 소스 스키마 &quot;[!DNL Loyalty Members]&quot;.

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

| 매개 변수 | 설명 |
| --- | --- |
| `@type` | 정의되는 설명자의 유형입니다. 참조 설명자의 경우 값은 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 다음 `$id` 소스 스키마의 URL입니다. |
| `xdm:sourceVersion` | 소스 스키마의 버전 번호입니다. |
| `sourceProperty` | 참조 스키마의 기본 ID를 참조하는 데 사용할 소스 스키마의 필드 경로입니다. |
| `xdm:identityNamespace` | 참조 필드의 ID 네임스페이스입니다. 이것은 참조 스키마의 기본 ID와 동일한 네임스페이스여야 합니다. 자세한 내용은 [id 네임스페이스 개요](../../identity-service/home.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 소스 필드에 대해 새로 생성된 참조 설명자의 세부 정보를 반환합니다.

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

관계 설명자는 소스 스키마와 참조 스키마 간에 일대일 관계를 설정합니다. 소스 스키마의 해당 필드에 대한 참조 ID 설명자를 정의한 후에는 `/tenant/descriptors` 엔드포인트.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 &quot;[!DNL Loyalty Members]&quot; 를 소스 스키마로 사용하고 &quot;[!DNL Hotels]&quot; 를 참조 스키마로 사용합니다.

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

| 매개 변수 | 설명 |
| --- | --- |
| `@type` | 생성할 설명자 유형입니다. 다음 `@type` 관계 설명자의 값은 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 다음 `$id` 소스 스키마의 URL입니다. |
| `xdm:sourceVersion` | 소스 스키마의 버전 번호입니다. |
| `xdm:sourceProperty` | 소스 스키마에 있는 참조 필드의 경로입니다. |
| `xdm:destinationSchema` | 다음 `$id` 참조 스키마의 URL입니다. |
| `xdm:destinationVersion` | 참조 스키마의 버전 번호입니다. |
| `xdm:destinationProperty` | 참조 스키마의 기본 ID 필드에 대한 경로입니다. |

{style=&quot;table-layout:auto&quot;}

### 응답

성공한 응답은 새로 만든 관계 설명자의 세부 정보를 반환합니다.

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

이 자습서를 따라 두 스키마 간에 일대일 관계를 성공적으로 만들었습니다. 를 사용하여 설명자를 사용하는 방법에 대한 자세한 정보 [!DNL Schema Registry] API인 경우 [스키마 레지스트리 개발자 안내서](../api/descriptors.md). UI에서 스키마 관계를 정의하는 방법에 대한 단계는 [스키마 편집기를 사용하여 스키마 관계 정의](relationship-ui.md).
