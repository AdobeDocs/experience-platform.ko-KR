---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;스키마;스키마;스키마;스키마;스키마;스키마;스키마 만들기
solution: Experience Platform
title: 스키마 레지스트리 API를 사용하여 스키마 만들기
type: Tutorial
description: 이 자습서에서는 스키마 레지스트리 API를 사용하여 표준 클래스를 사용하여 스키마를 구성하는 단계를 안내합니다.
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 6a69dd0bf8945dfef5ac73ee11a0ed6603ee4b9b
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# 를 사용하여 스키마 만들기 [!DNL Schema Registry] API

다음 [!DNL Schema Registry] 이(가) [!DNL Schema Library] Adobe Experience Platform 내에서 사용할 수 있습니다. 다음 [!DNL Schema Library] Adobe이 사용할 수 있는 리소스를 포함합니다. [!DNL Experience Platform] 사용자가 사용하는 애플리케이션을 소유한 파트너 및 공급업체 레지스트리는 사용 가능한 모든 라이브러리 리소스에 액세스할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Schema Registry] 표준 클래스를 사용하여 스키마를 구성하는 단계를 안내하는 API입니다. 에서 사용자 인터페이스를 사용하려면 [!DNL Experience Platform], [스키마 편집기 자습서](create-schema-ui.md) 는 스키마 편집기에서 유사한 작업을 수행하는 단계별 지침을 제공합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

이 자습서를 시작하기 전에 [개발자 안내서](../api/getting-started.md) 를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보 [!DNL Schema Registry] API. 여기에는 다음이 포함됩니다 `{TENANT_ID}`, &quot;컨테이너&quot;의 개념 및 요청을 수행하는 데 필요한 헤더입니다(에는 `Accept` 헤더 및 가능한 값).

이 자습서에서는 소매 충성도 프로그램의 구성원과 관련된 데이터를 설명하는 충성도 멤버 스키마를 구성하는 단계를 안내합니다. 시작하기 전에 를 미리 볼 수 있습니다 [전체 충성도 멤버 스키마](#complete-schema) 맹장에서요

## 표준 클래스로 스키마 작성

스키마는 수집하려는 데이터의 블루프린트로 생각할 수 있습니다 [!DNL Experience Platform]. 각 스키마는 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다. 즉, 스키마를 정의하기 위해 필드 그룹을 추가할 필요는 없지만, 대부분의 경우 필드 그룹이 하나 이상 사용됩니다.

### 클래스 할당

스키마 구성 프로세스는 클래스 선택과 함께 시작됩니다. 이 클래스는 데이터의 주요 행동 측면(레코드 및 시계열)과 수집할 데이터를 설명하는 데 필요한 최소 필드를 정의합니다.

이 자습서에서 만드는 스키마는 [!DNL XDM Individual Profile] 클래스 이름을 지정합니다. [!DNL XDM Individual Profile] 는 레코드 동작을 정의하기 위해 Adobe에서 제공하는 표준 클래스입니다. 동작에 대한 자세한 내용은 [스키마 구성 기본 사항](../schema/composition.md).

클래스를 할당하기 위해 테넌트 컨테이너에 새 스키마를 만들기(POST)하기 위해 API 호출이 수행됩니다. 이 호출에는 스키마가 구현할 클래스가 포함됩니다. 각 스키마는 하나의 클래스만 구현할 수 있습니다.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

요청에는 `allOf` 를 참조하는 속성 `$id` A. 이 속성은 스키마가 구현할 &quot;기본 클래스&quot;를 정의합니다. 이 예제에서 기본 클래스는 [!DNL XDM Individual Profile] 클래스 이름을 지정합니다. 다음 `$id` 의 [!DNL XDM Individual Profile] 클래스는 `$ref` 의 필드 `allOf` 아래에 배열되어 있습니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
  "type": "object",
  "title": "Loyalty Members",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile"
    }
  ]
}'
```

**응답**

성공적인 요청은 를 포함하여 새로 생성된 스키마의 세부 사항이 포함된 응답 본문을 사용하여 HTTP 응답 상태 201(생성됨)을 반환합니다. `$id`, `meta:altIt`, 및 `version`. 이러한 값은 읽기 전용이며 [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/tenantId/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_tenantId.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310304048,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_tenantId"
}
```

### 스키마 조회

새로 만든 스키마를 보려면 `meta:altId` 또는 URL을 인코딩했습니다 `$id` 스키마의 URI입니다.

**API 형식**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 검색할 스키마 중 하나입니다. |

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**응답**

응답 형식은 `Accept` 헤더와 함께 전송됩니다. 다양한 테스트를 해 보십시오 `Accept` 헤더를 확인해 보십시오.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310304048,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:allFieldAccess": true
}
```

### 필드 그룹 추가 {#add-a-field-group}

충성도 멤버 스키마가 만들어지고 확인되었으므로 필드 그룹을 추가할 수 있습니다.

선택한 스키마의 클래스에 따라 사용할 수 있는 다른 표준 필드 그룹이 있습니다. 각 필드 그룹에는 `intendedToExtend` 해당 필드 그룹이 호환되는 클래스를 정의하는 필드입니다.

필드 그룹은 동일한 정보를 캡처해야 하는 모든 스키마에서 재사용할 수 있는 &quot;이름&quot; 또는 &quot;주소&quot;와 같은 개념을 정의합니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 필드 그룹을 추가할 스키마 중 하나입니다. |

**요청**

이 요청은 충성도 멤버 스키마를 업데이트하여 [[!UICONTROL 인구 통계 세부 정보] 필드 그룹](../field-groups/profile/demographic-details.md) (`profile-person-details`).

다음을 추가하여 `profile-person-details` 이제 충성도 멤버 스키마는 이름, 성 및 생일과 같은 충성도 프로그램 구성원에 대한 인구 통계 정보를 캡처합니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**응답**

응답에는 `meta:extends` 배열 및 포함 `$ref` 의 필드 그룹으로 `allOf` 속성을 사용합니다.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
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
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673310912096,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "b480f28a35f356b237fc129e796074a3f33a7a67df273f6a8beaee1ec6465540",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### 필드 그룹 추가

충성도 멤버 스키마에는 다른 필드 그룹을 사용하여 단계를 반복하여 추가할 수 있는 두 개의 표준 필드 그룹이 더 필요합니다.

>[!TIP]
>
>사용 가능한 모든 필드 그룹을 검토하여 각 필드에 포함된 필드를 숙지하는 것이 좋습니다. 각 &quot;global&quot; 및 &quot;tenant&quot; 컨테이너에 대해 요청을 수행하여 특정 클래스와 함께 사용할 수 있는 모든 필드 그룹을 나열하고 &quot;meta:intentToExtend&quot; 필드가 사용 중인 클래스와 일치하는 필드 그룹만 반환할 수 있습니다. 이 경우 [!DNL XDM Individual Profile] 클래스 [!DNL XDM Individual Profile] `$id` 이 사용됩니다.
>
>
```http
>GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>```

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 업데이트할 스키마 중 하나입니다. |

**요청**

이 요청은 다음 표준 필드 그룹 내에 필드를 포함하도록 충성도 멤버 스키마를 업데이트합니다.

* [[!UICONTROL 개인 연락처 세부 정보]](../field-groups/profile/personal-contact-details.md) (`profile-personal-details`): 집 주소, 이메일 주소 및 집 전화와 같은 연락처 정보를 추가합니다.
* [[!UICONTROL 충성도 세부 사항]](../field-groups/profile/loyalty-details.md) (`profile-loyalty-details`): 집 주소, 이메일 주소 및 집 전화와 같은 연락처 정보를 추가합니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"}}
      ]'  
```

**응답**

응답에는 `meta:extends` 배열 및 포함 `$ref` 의 필드 그룹으로 `allOf` 속성을 사용합니다.

충성도 멤버 스키마에는 이제 네 개가 포함되어야 합니다 `$ref` 의 값 `allOf` 배열: `profile`, `profile-person-details`, `profile-personal-details`, 및 `profile-loyalty-details` 아래와 같이 표시됩니다.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.2",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
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
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673311559934,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "1de5ed1a07e3478719952f0a8c94d5e5390d5a9a998761adb4cf1989137fd6ea",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### 새 필드 그룹 정의

표준 [!UICONTROL 충성도 세부 사항] 필드 그룹은 스키마에 유용한 충성도 관련 필드를 제공하며, 표준 필드 그룹에 포함되지 않은 추가 충성도 필드가 있습니다.

이러한 필드를 추가하려면 `tenant` 컨테이너. 이러한 필드 그룹은 조직에 고유하며 조직 외부의 다른 사람이 보거나 편집할 수 없습니다.

새 필드 그룹을 생성(POST)하려면, 요청에 가 포함되어야 합니다 `meta:intendedToExtend` 를 포함하는 필드 `$id` 필드 그룹이 호환되는 기본 클래스(예: 필드 그룹이 포함할 속성)의 경우

모든 사용자 지정 속성은 `TENANT_ID` 다른 필드 그룹 또는 필드와의 충돌을 피하려면 다음을 수행하십시오.

**API 형식**

```http
POST /tenant/fieldgroups
```

**요청**

이 요청은 네 개의 충성도 프로그램별 필드를 포함하는 &quot;충성도&quot; 개체가 있는 새 필드 그룹을 만듭니다. &quot;충성도Id&quot;, &quot;충성도Level&quot;, &quot;충성도Points&quot; 및 &quot;memberSince&quot;

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Tier",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Captures info about the current loyalty tier of a customer.",
        "definitions": {
            "loyaltyTier": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "loyaltyTier": {
                      "type": "object",
                      "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier."
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier."
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                        }
                      }
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyaltyTier"
            }
        ]
    }'
```

**응답**

성공적인 요청은 HTTP 응답 상태 201(생성됨)을 반환하며 이 반환에는 다음을 포함하여 새로 만든 필드 그룹의 세부 사항이 포함됩니다 `$id`, `meta:altIt`, 및 `version`. 이러한 값은 읽기 전용이며 [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Captures info about the current loyalty tier of a customer.",
    "definitions": {
        "loyaltyTier": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyTier": {
                            "type": "object",
                            "properties": {
                                "id": {
                                    "title": "Loyalty Tier Identifier",
                                    "type": "string",
                                    "description": "Loyalty Tier Identifier.",
                                    "meta:xdmType": "string"
                                },
                                "effectiveDate": {
                                    "title": "Effective Date",
                                    "type": "string",
                                    "format": "date-time",
                                    "description": "Date the member joined their current loyalty tier.",
                                    "meta:xdmType": "date-time"
                                },
                                "currentThreshold": {
                                    "title": "Current Point Threshold",
                                    "type": "integer",
                                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                                    "meta:xdmType": "int"
                                },
                                "nextThreshold": {
                                    "title": "Next Point Threshold",
                                    "type": "integer",
                                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                                    "meta:xdmType": "int"
                                }
                            },
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673313004645,
        "repo:lastModifiedDate": 1673313004645,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### 스키마에 사용자 지정 필드 그룹 추가

이제 다음 기간 동안 동일한 단계를 수행할 수 있습니다 [표준 필드 그룹 추가](#add-a-field-group) 이렇게 새로 만든 필드 그룹을 스키마에 추가하려면

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 스키마 입니다. |

**요청**

이 요청은 충성도 구성원 스키마를 업데이트(PATCH)하여 새로운 &quot;충성도 계층&quot; 필드 그룹 내에 필드를 포함합니다.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"}}
      ]'
```

**응답**

이제 응답에 에 새 추가된 필드 그룹이 표시되므로 필드 그룹이 성공적으로 추가되었음을 확인할 수 있습니다 `meta:extends` 배열 및 포함 `$ref` 의 필드 그룹으로 `allOf` 속성을 사용합니다.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
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
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### 현재 스키마 보기

이제 GET 요청을 수행하여 현재 스키마를 보고 추가된 필드 그룹이 스키마 전체 구조에 어떻게 기여했는지 확인할 수 있습니다.

**API 형식**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 스키마 입니다. |

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**응답**

를 사용하여 `application/vnd.adobe.xed-full+json; version=1` `Accept` header. 모든 속성을 표시하는 전체 스키마를 볼 수 있습니다. 이러한 속성은 스키마를 구성하는 데 사용된 클래스 및 필드 그룹에서 제공하는 필드입니다. 아래 예제 응답에서는 공간에 대해 최근에 추가된 필드만 표시됩니다. 모든 속성 및 해당 속성을 포함하여 전체 스키마를 [부록](#appendix) 이 문서의 끝 부분.

아래 `"properties"`를 클릭하면 `_{TENANT_ID}` 사용자 지정 필드 그룹을 추가할 때 만든 네임스페이스입니다. 해당 네임스페이스 내에는 &quot;충성도&quot; 개체 및 필드 그룹을 만들 때 정의된 필드가 있습니다.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "properties": {
        "_{TENANT_ID}": {
            "type": "object",
            "properties": {
                "loyaltyTier": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier.",
                            "meta:xdmType": "string"
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier.",
                            "meta:xdmType": "date-time"
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                            "meta:xdmType": "int"
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                            "meta:xdmType": "int"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "meta:xdmType": "object"
        }
    },
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:allFieldAccess": true
}
```

### 데이터 유형 만들기

만든 충성도 계층 필드 그룹에는 다른 스키마에서 유용할 수 있는 특정 속성이 포함되어 있습니다. 예를 들어, 데이터를 경험 이벤트의 일부로 수집하거나 다른 클래스를 구현하는 스키마에서 사용할 수 있습니다. 이 경우 다른 곳에서 정의를 다시 사용하기 쉽게 하기 위해 객체 계층을 데이터 유형으로 저장하는 것이 적절합니다.

데이터 유형을 사용하면 객체 계층을 한 번 정의할 수 있으며 다른 스칼라 유형에 대해 마찬가지로 필드에서 해당 계층을 참조할 수 있습니다.

즉, 데이터 유형을 사용하면 필드의 &quot;유형&quot;으로 추가하여 스키마에서 어느 곳에나 포함할 수 있으므로 필드 그룹보다 유연성이 높은 다중 필드 구조를 일관되게 사용할 수 있습니다.

**API 형식**

```http
POST /tenant/datatypes
```

**요청**

데이터 유형을 정의할 필요는 없습니다 `meta:extends` 또는 `meta:intendedToExtend` 필드 및 필드는 충돌을 방지하기 위해 테넌트 ID 아래에 중첩될 필요가 없습니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Tier",
        "type": "object",
        "description": "Loyalty Tier data type",
        "definitions": {
            "loyaltyTier": {
                "type": "object",
                "properties": {
                    "id": {
                        "title": "Loyalty Tier Identifier",
                        "type": "string",
                        "description": "Loyalty Tier Identifier."
                    },
                    "effectiveDate": {
                        "title": "Effective Date",
                        "type": "string",
                        "format": "date-time",
                        "description": "Date the member joined their current loyalty tier."
                    },
                    "currentThreshold": {
                        "title": "Current Point Threshold",
                        "type": "integer",
                        "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                    },
                    "nextThreshold": {
                        "title": "Next Point Threshold",
                        "type": "integer",
                        "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                    }
                }
            }
        },
        "allOf": [
            {
            "$ref": "#/definitions/loyaltyTier"
            }
        ]
      }'
```

**응답**

성공적인 요청은 다음을 포함하여 새로 만든 데이터 유형의 세부 사항이 포함된 응답 본문과 함께 HTTP 응답 상태 201(생성됨)을 반환합니다 `$id`, `meta:altIt`, 및 `version`. 이러한 값은 읽기 전용이며 [!DNL Schema Registry].

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
    "meta:altId": "_{TENANT_ID}.datatypes.c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
    "meta:resourceType": "datatypes",
    "version": "1.0",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Loyalty Tier data type",
    "definitions": {
        "loyaltyTier": {
            "type": "object",
            "properties": {
                "id": {
                    "title": "Loyalty Tier Identifier",
                    "type": "string",
                    "description": "Loyalty Tier Identifier.",
                    "meta:xdmType": "string"
                },
                "effectiveDate": {
                    "title": "Effective Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined their current loyalty tier.",
                    "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                    "title": "Current Point Threshold",
                    "type": "integer",
                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                    "meta:xdmType": "int"
                },
                "nextThreshold": {
                    "title": "Next Point Threshold",
                    "type": "integer",
                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                    "meta:xdmType": "int"
                }
            },
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673378256699,
        "repo:lastModifiedDate": 1673378256699,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "8afba84c0c9a68126a7a1389f8523a1112bdf4405badc6dcddbbb4a0e18f5cdb",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

URL 인코딩을 사용하여 조회(GET) 요청을 수행할 수 있습니다 `$id` 새 데이터 유형을 직접 보려면 URI를 사용하십시오. 에 를 포함해야 합니다 `version` 다음 위치에서 `Accept` 조회 요청에 대한 헤더입니다.

### 스키마에 데이터 유형 사용

충성도 계층 데이터 유형이 만들어졌으므로 이제 다음을 업데이트(PATCH)할 수 있습니다 `loyaltyTier` 이전에 해당 필드에 있던 필드 대신 데이터 유형을 참조하도록 만든 필드 그룹의 필드입니다.

**API 형식**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{FIELD_GROUP_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` 업데이트할 필드 그룹의 이름입니다. |

**요청**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "op": "replace",
            "path": "/definitions/loyaltyTier/properties/_{TENANT_ID}/properties",
            "value": {
                "loyaltyTier": {
                    "title": "Loyalty Tier",
                    "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
                    "description": "Loyalty tier info"
                }
            }
        }
    ]
```

**응답**

이제 응답에 참조( )가 포함됩니다.`$ref`)을 추가하여 이전에 정의한 필드 대신 &quot;충성도&quot; 개체에 있는 데이터 유형을 지정합니다.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
    "meta:resourceType": "mixins",
    "version": "1.1",
    "title": "Loyalty Tier",
    "type": "object",
    "description": "Captures info about the current loyalty tier of a customer.",
    "definitions": {
        "loyaltyTier": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "loyaltyTier": {
                            "title": "Loyalty Tier",
                            "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
                            "description": "Loyalty tier info",
                            "type": "object",
                            "meta:xdmType": "object"
                        }
                    },
                    "meta:xdmType": "object"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/loyaltyTier",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673313004645,
        "repo:lastModifiedDate": 1673378970276,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "4df8fa56d00991590364606bb2e219e1ea8f5717a51c0e6ae57ca956830b6a27",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

지금 스키마를 조회하기 위해 GET 요청을 수행하는 경우, `loyaltyTier` 속성은 다음 데이터 형식에 대한 참조를 보여 줍니다. `meta:referencedFrom`:

```JSON
"_{TENANT_ID}": {
    "type": "object",
    "meta:xdmType": "object",
    "properties": {
        "loyaltyTier": {
            "title": "Loyalty Tier",
            "description": "Loyalty tier info",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "id": {
                    "title": "Loyalty Tier Identifier",
                    "type": "string",
                    "description": "Loyalty Tier Identifier.",
                    "meta:xdmType": "string"
                },
                "effectiveDate": {
                    "title": "Effective Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date the member joined their current loyalty tier.",
                    "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                    "title": "Current Point Threshold",
                    "type": "integer",
                    "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                    "meta:xdmType": "int"
                },
                "nextThreshold": {
                    "title": "Next Point Threshold",
                    "type": "integer",
                    "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                    "meta:xdmType": "int"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
        }
    }
}
```

### ID 설명자 정의

스키마는에 데이터를 수집하는 데 사용됩니다 [!DNL Experience Platform]. 이 데이터는 궁극적으로 여러 서비스에서 사용되어 한 개인을 하나의 통합된 보기로 만듭니다. 이 프로세스를 지원하기 위해 키 필드를 &quot;ID&quot;로 표시할 수 있으며, 데이터 섭취 시 해당 필드의 데이터가 해당 개인의 &quot;Identity Graph&quot;에 삽입됩니다. 그런 다음 그래프 데이터에 [[!DNL Real-Time Customer Profile]](../../profile/home.md) 및 기타 [!DNL Experience Platform] 각 개별 고객에 대한 결합된 보기를 제공하는 서비스.

일반적으로 &quot;ID&quot;로 표시된 필드는 다음과 같습니다. 이메일 주소, 전화 번호, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM ID 또는 기타 고유한 ID 필드. 적절한 ID 필드일 수 있으므로 조직에 고유한 식별자를 고려합니다.

ID 설명자는 `sourceProperty` 의 `sourceSchema` 는 ID로 간주해야 하는 고유 식별자입니다.

설명자 작업에 대한 자세한 내용은 [스키마 레지스트리 개발자 안내서](../api/getting-started.md).

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청에서는 `personalEmail.address` 충성도 멤버 스키마의 필드입니다. 이것은 [!DNL Experience Platform] 충성도 멤버의 이메일 주소를 식별자로 사용하여 개인에 대한 정보를 함께 결합하는 데 도움이 되도록 합니다. 또한 이 호출은 를 설정하여 이 필드를 스키마의 기본 ID로 설정합니다 `xdm:isPrimary` to `true`: [실시간 고객 프로필에서 사용할 스키마 활성화](#profile).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE]
>
>사용 가능한 &quot;xdm:namespace&quot; 값을 나열하거나 [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). xdm:property의 값은 사용된 &quot;xdm:namespace&quot;에 따라 &quot;xdm:code&quot; 또는 &quot;xdm:id&quot;일 수 있습니다.

**응답**

성공한 응답은 새로 만든 설명자를 포함하여 해당 설명자의 세부 정보가 포함된 응답 본문을 사용하여 HTTP 상태 201(생성됨)을 반환합니다 `@id`. 다음 `@id` 는 [!DNL Schema Registry] 및 는 API에서 설명자를 참조하는 데 사용됩니다.

```JSON
{
    "@id": "719a4391897c097786efbaa6d4262bb928a1cd88540344c6",
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/personalEmail/address",
    "imsOrg": "{ORG_ID}",
    "version": "1",
    "xdm:namespace": "Email",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

## 에서 사용할 스키마 활성화 [!DNL Real-Time Customer Profile] {#profile}

스키마에 기본 ID 설명자가 적용되면, 사용자가 사용할 충성도 멤버 스키마를 활성화할 수 있습니다 [!DNL Real-Time Customer Profile] 추가 `union` 태그에 다음 코드 행을 추가하여 `meta:immutableTags` 속성을 사용합니다.

>[!NOTE]
>
>조합 보기 작업에 대한 자세한 내용은 [노조](../api/unions.md) 에서 [!DNL Schema Registry] 개발자 안내서.

### 추가 `union` 태그

병합된 결합 보기에 스키마를 포함하려면 `union` 태그에 태그를 추가해야 합니다. `meta:immutableTags` 스키마 속성입니다. 이 작업은 스키마를 업데이트하고 를 추가하기 위한 PATCH 요청을 통해 수행됩니다 `meta:immutableTags` 값이 인 배열 `union`.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩됨 `$id` Profile에 대해 활성화한 스키마 중 하나입니다. |

**요청**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**응답**

응답에는 작업이 성공적으로 수행되었음을 나타내며, 이제 스키마에 최상위 속성이 포함됩니다. `meta:immutableTags`: 값 &quot;union&quot;이 포함된 배열입니다.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
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
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673380280074,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### 결합 스키마 나열

이제 스키마를 [!DNL XDM Individual Profile] 합집합. 동일한 합계의 일부인 모든 스키마 목록을 보려면 쿼리 매개 변수를 사용하여 GET 요청을 수행하여 응답을 필터링할 수 있습니다.

사용 `property` 쿼리 매개 변수를 사용하면 `meta:immutableTags` 필드가 있는 필드 `meta:class` 다음과 같음 `$id` 의 [!DNL XDM Individual Profile] 클래스가 반환됩니다.

**API 형식**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**요청**

아래 예제 요청은 의 일부인 모든 스키마를 반환합니다 [!DNL XDM Individual Profile] 합집합.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답은 두 요구 사항을 모두 충족하는 스키마만 포함하는 필터링된 스키마 목록입니다. 여러 쿼리 매개 변수를 사용할 때는 AND 관계를 가정합니다. 목록 응답의 형식은 `Accept` 헤더가 전송되었습니다.

```JSON
{
    "results": [
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d29a200b5deb6cfb55d3b865ef627f33",
            "meta:altId": "_{TENANT_ID}.schemas.d29a200b5deb6cfb55d3b865ef627f33",
            "version": "1.2",
            "title": "Profile Schema"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/5d70026f5522fc60b3c81f6523b83c86",
            "meta:altId": "_{TENANT_ID}.schemas.5d70026f5522fc60b3c81f6523b83c86",
            "version": "1.3",
            "title": "CRM Onboarding"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
            "meta:altId": "_{TENANT_ID}.schemas.653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
            "version": "1.1",
            "title": "Profile consents"
        },
        {
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
            "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
            "version": "1.4",
            "title": "Loyalty Members"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 4
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```

## 다음 단계

이 자습서를 따라 표준 필드 그룹과 정의한 필드 그룹을 모두 사용하여 스키마를 구성했습니다. 이제 이 스키마를 사용하여 데이터 세트를 만들고 레코드 데이터를 Adobe Experience Platform에 수집할 수 있습니다.

이 자습서 전체에서 만들어진 전체 충성도 멤버 스키마는 다음에 나오는 부록에서 사용할 수 있습니다. 스키마를 살펴보면 필드 그룹이 전체 구조에 어떻게 기여하고 데이터 수집을 위해 사용할 수 있는 필드를 확인할 수 있습니다.

두 개 이상의 스키마를 생성한 후에는 관계 설명자를 사용하여 관계 관계를 정의할 수 있습니다. 다음에 대한 자습서를 참조하십시오. [두 스키마 간의 관계 정의](relationship-api.md) 추가 정보. 레지스트리에서 모든 작업(GET, POST, PUT, PATCH 및 DELETE)을 수행하는 방법에 대한 자세한 예는 [스키마 레지스트리 개발자 안내서](../api/getting-started.md) 를 사용하도록 선택할 수 있습니다.

## 부록 {#appendix}

다음 정보는 API 자습서를 보완합니다.

## 전체 충성도 멤버 스키마 {#complete-schema}

이 자습서 전체에서 소매 충성도 프로그램의 구성원을 설명하기 위해 스키마가 작성됩니다.

스키마는 [!DNL XDM Individual Profile] 클래스와 는 여러 필드 그룹을 결합합니다. 표준 을 사용하여 충성도 멤버에 대한 정보를 캡처합니다 [!DNL Demographic Details], [!UICONTROL 개인 연락처 세부 정보], 및 [!UICONTROL 충성도 세부 사항] 필드 그룹뿐만 아니라 자습서 중에 정의된 사용자 지정 충성도 계층 필드 그룹을 통해 필드 그룹을 만듭니다.

다음은 완료된 충성도 멤버 스키마를 JSON 형식으로 보여 줍니다.

+++전체 스키마 보기

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "properties": {
        "_{TENANT_ID}": {
            "type": "object",
            "properties": {
                "loyaltyTier": {
                    "title": "Loyalty Tier",
                    "description": "Loyalty tier info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "id": {
                            "title": "Loyalty Tier Identifier",
                            "type": "string",
                            "description": "Loyalty Tier Identifier.",
                            "meta:xdmType": "string"
                        },
                        "effectiveDate": {
                            "title": "Effective Date",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined their current loyalty tier.",
                            "meta:xdmType": "date-time"
                        },
                        "currentThreshold": {
                            "title": "Current Point Threshold",
                            "type": "integer",
                            "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                            "meta:xdmType": "int"
                        },
                        "nextThreshold": {
                            "title": "Next Point Threshold",
                            "type": "integer",
                            "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                            "meta:xdmType": "int"
                        }
                    },
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
                }
            },
            "meta:xdmType": "object"
        },
        "_id": {
            "title": "Identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "A unique identifier for the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "@id"
        },
        "_repo": {
            "properties": {
                "createDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:immutable": true,
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "repo:createDate"
                },
                "modifyDate": {
                    "type": "string",
                    "format": "date-time",
                    "meta:usereditable": false,
                    "examples": [
                        "2004-10-23T12:00:00-06:00"
                    ],
                    "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "repo:modifyDate"
                }
            },
            "type": "object",
            "meta:xdmType": "object",
            "meta:xedConverted": true
        },
        "billingAddress": {
            "title": "Billing Address",
            "description": "Billing postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:billingAddress"
        },
        "createdByBatchID": {
            "title": "Created by batch identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The dataset files in Catalog which has been originating the creation of the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:createdByBatchID"
        },
        "faxPhone": {
            "title": "Fax Phone",
            "description": "Fax phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:faxPhone"
        },
        "homeAddress": {
            "title": "Home Address",
            "description": "A home postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:homeAddress"
        },
        "homePhone": {
            "title": "Home Phone",
            "description": "Home phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:homePhone"
        },
        "loyalty": {
            "type": "object",
            "description": "Captures details related to the customer's loyalty rewards.",
            "properties": {
                "joinDate": {
                    "title": "Program Join Date",
                    "type": "string",
                    "format": "date-time",
                    "description": "Date which the visitor registered for the loyalty program.",
                    "meta:xdmType": "date-time",
                    "meta:xdmField": "xdm:joinDate"
                },
                "loyaltyID": {
                    "title": "Program ID",
                    "type": "array",
                    "items": {
                        "type": "string",
                        "meta:xdmType": "string"
                    },
                    "description": "The loyalty program ID(s) associated with a specific user, if they are enrolled in the client's loyalty program.",
                    "meta:xdmType": "array",
                    "meta:xdmField": "xdm:loyaltyID"
                },
                "points": {
                    "title": "Program Points Balance",
                    "type": "number",
                    "description": "Current balance of the loyalty points/awards in a visitor's loyalty account.",
                    "meta:xdmType": "number",
                    "meta:xdmField": "xdm:points"
                },
                "pointsExpiration": {
                    "title": "Points Expiration",
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "pointsExpirationDate": {
                                "type": "string",
                                "format": "date-time",
                                "description": "Date on which the given portion of the loyalty points expire.",
                                "meta:xdmType": "date-time",
                                "meta:xdmField": "xdm:pointsExpirationDate"
                            },
                            "pointsExpiring": {
                                "title": "Points Expiring",
                                "type": "number",
                                "description": "Point balance expiring as of the associated expiration date.",
                                "meta:xdmType": "number",
                                "meta:xdmField": "xdm:pointsExpiring"
                            }
                        },
                        "meta:xdmType": "object"
                    },
                    "meta:xdmType": "array",
                    "meta:xdmField": "xdm:pointsExpiration"
                },
                "pointsRedeemed": {
                    "title": "Points Redeemed",
                    "type": "number",
                    "description": "Amount of points applied toward a purchase or otherwise redeemed.",
                    "meta:xdmType": "number",
                    "meta:xdmField": "xdm:pointsRedeemed"
                },
                "program": {
                    "title": "Program Name",
                    "type": "string",
                    "description": "This should define the loyalty progam in which a visitor is enrolled.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:program"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "Captures the visitor's loyalty progam status, such as active, disabled, or suspended.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "tier": {
                    "title": "Tier",
                    "type": "string",
                    "description": "Captures the loyalty progam tier in which a visitor is enrolled.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:tier"
                },
                "upgradeDate": {
                    "title": "Program Name",
                    "type": "string",
                    "description": "Date which the customer was upgraded to the next tier level.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:upgradeDate"
                }
            },
            "meta:xdmType": "object",
            "meta:xdmField": "xdm:loyalty"
        },
        "mailingAddress": {
            "title": "Mailing Address",
            "description": "Mailing postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:mailingAddress"
        },
        "mobilePhone": {
            "title": "Mobile Phone",
            "description": "Mobile phone number.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "countryCode": {
                    "title": "Country Calling Code",
                    "type": "string",
                    "description": "Country calling code (CC) as defined by E.164.",
                    "minLength": 1,
                    "maxLength": 3,
                    "pattern": "^[0-9]{1,3}?$",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "extension": {
                    "title": "Extension",
                    "type": "string",
                    "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:extension"
                },
                "number": {
                    "title": "Number",
                    "type": "string",
                    "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:number"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the phone number.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "validity": {
                    "title": "Validity",
                    "type": "string",
                    "description": "A level of technical correctness of the phone number.",
                    "meta:enum": {
                        "consistent": "Consistent",
                        "inconsistent": "Inconsistent",
                        "incomplete": "Incomplete",
                        "successfullyUsed": "Successfully used"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:validity"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
            "meta:xdmField": "xdm:mobilePhone"
        },
        "modifiedByBatchID": {
            "title": "Modified by batch identifier",
            "type": "string",
            "format": "uri-reference",
            "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "birthDate": {
                    "title": "Birth date(YYYY-MM-DD)",
                    "type": "string",
                    "format": "date",
                    "description": "The full date a person was born.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:birthDate"
                },
                "birthDayAndMonth": {
                    "title": "Birth date (MM-DD)",
                    "type": "string",
                    "pattern": "[0-1][0-9]-[0-9][0-9]",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:birthDayAndMonth"
                },
                "birthYear": {
                    "title": "Birth year",
                    "type": "integer",
                    "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date.",
                    "minimum": 1,
                    "maximum": 32767,
                    "meta:xdmType": "short",
                    "meta:xdmField": "xdm:birthYear"
                },
                "gender": {
                    "title": "Gender",
                    "type": "string",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Non-specific"
                    },
                    "description": "Gender identity of the person.\n",
                    "default": "not_specified",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:gender"
                },
                "maritalStatus": {
                    "title": "Marital Status",
                    "type": "string",
                    "enum": [
                        "married",
                        "single",
                        "divorced",
                        "widowed",
                        "not_specified"
                    ],
                    "meta:enum": {
                        "married": "Married",
                        "single": "Single",
                        "divorced": "Divorced",
                        "widowed": "Widowed",
                        "not_specified": "Not Specified"
                    },
                    "description": "Describes a person's relationship with a significant other.",
                    "default": "not_specified",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:maritalStatus"
                },
                "name": {
                    "title": "Full name",
                    "description": "The person's full name.",
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "courtesyTitle": {
                            "title": "Courtesy title",
                            "type": "string",
                            "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:courtesyTitle"
                        },
                        "firstName": {
                            "title": "First name",
                            "type": "string",
                            "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:firstName"
                        },
                        "fullName": {
                            "title": "Full name",
                            "type": "string",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:fullName"
                        },
                        "lastName": {
                            "title": "Last name",
                            "type": "string",
                            "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:lastName"
                        },
                        "middleName": {
                            "title": "Middle name",
                            "type": "string",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:middleName"
                        },
                        "suffix": {
                            "title": "Suffix",
                            "type": "string",
                            "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "xdm:suffix"
                        }
                    },
                    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
                    "meta:xdmField": "xdm:name"
                },
                "nationality": {
                    "title": "Nationality",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:nationality"
                },
                "taxId": {
                    "title": "Tax ID",
                    "type": "string",
                    "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
                    "meta:status": "deprecated",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:taxId"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The type of individual in different business contexts like B2C.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:type"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
            "meta:xdmField": "xdm:person"
        },
        "personID": {
            "title": "Person ID",
            "description": "Unique identifier of Person/Profile fragment.",
            "type": "string",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:personID"
        },
        "personalEmail": {
            "title": "Personal Email",
            "description": "A personal email address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "address": {
                    "title": "Address",
                    "type": "string",
                    "format": "email",
                    "description": "The technical address, for example, 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:address",
                    "minLength": 1
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Additional display information that maybe available, for example, Microsoft Outlook rich address controls display 'John Smith smithjr@company.uk', 'John Smith' part is data that would be placed in the label.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary email indicator. A profile can have only one `primary` email address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the email address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "type": {
                    "title": "Type",
                    "type": "string",
                    "description": "The way the account relates to the person for example 'work' or 'personal'.",
                    "meta:enum": {
                        "unknown": "Unknown",
                        "personal": "Personal",
                        "work": "Work",
                        "education": "Education"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:type"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
            "meta:xdmField": "xdm:personalEmail",
            "required": [
                "address"
            ]
        },
        "repositoryCreatedBy": {
            "title": "Created by user identifier",
            "type": "string",
            "description": "User ID of who created the record.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
            "title": "Modified by user identifier",
            "type": "string",
            "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
            "meta:xdmType": "string",
            "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "shippingAddress": {
            "title": "Shipping Address",
            "description": "Shipping postal address.",
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "_id": {
                    "title": "Coordinates ID",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The unique identifier of the coordinates.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                },
                "_repo": {
                    "properties": {
                        "createDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:immutable": true,
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:createDate"
                        },
                        "modifyDate": {
                            "type": "string",
                            "format": "date-time",
                            "meta:usereditable": false,
                            "examples": [
                                "2004-10-23T12:00:00-06:00"
                            ],
                            "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
                            "meta:xdmType": "date-time",
                            "meta:xdmField": "repo:modifyDate"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "_schema": {
                    "properties": {
                        "description": {
                            "title": "Description",
                            "type": "string",
                            "description": "A description of what the coordinates identify.",
                            "meta:xdmType": "string",
                            "meta:xdmField": "schema:description"
                        },
                        "elevation": {
                            "title": "Elevation",
                            "type": "number",
                            "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:elevation"
                        },
                        "latitude": {
                            "title": "Latitude",
                            "type": "number",
                            "minimum": -90,
                            "maximum": 90,
                            "description": "The signed vertical coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:latitude"
                        },
                        "longitude": {
                            "title": "Longitude",
                            "type": "number",
                            "minimum": -180,
                            "maximum": 180,
                            "description": "The signed horizontal coordinate of a geographic point.",
                            "meta:xdmType": "number",
                            "meta:xdmField": "schema:longitude"
                        }
                    },
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:xedConverted": true
                },
                "city": {
                    "title": "City",
                    "type": "string",
                    "description": "The name of the city.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:city"
                },
                "country": {
                    "title": "Country",
                    "type": "string",
                    "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:country"
                },
                "countryCode": {
                    "title": "Country code",
                    "type": "string",
                    "pattern": "^[A-Z]{2}$",
                    "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:countryCode"
                },
                "createdByBatchID": {
                    "title": "Created by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The dataset files in Catalog which has been originating the creation of the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:createdByBatchID"
                },
                "dmaID": {
                    "title": "Designated market area",
                    "type": "integer",
                    "description": "The Nielsen media research designated market area.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:dmaID"
                },
                "label": {
                    "title": "Label",
                    "type": "string",
                    "description": "Free form name of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:label"
                },
                "lastVerifiedDate": {
                    "title": "Last verified date",
                    "type": "string",
                    "format": "date",
                    "description": "The date that the address was last verified as still associated to the person.",
                    "meta:xdmType": "date",
                    "meta:xdmField": "xdm:lastVerifiedDate"
                },
                "modifiedByBatchID": {
                    "title": "Modified by batch identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:modifiedByBatchID"
                },
                "msaID": {
                    "title": "Metropolitan statistical area",
                    "type": "integer",
                    "description": "The metropolitan statistical area in the United States where the observation occurred.",
                    "meta:xdmType": "int",
                    "meta:xdmField": "xdm:msaID"
                },
                "postOfficeBox": {
                    "title": "Post office box",
                    "type": "string",
                    "description": "Post office box of the address.",
                    "maxLength": 20,
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postOfficeBox"
                },
                "postalCode": {
                    "title": "Postal code",
                    "type": "string",
                    "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:postalCode"
                },
                "primary": {
                    "title": "Primary",
                    "type": "boolean",
                    "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
                    "meta:xdmType": "boolean",
                    "meta:xdmField": "xdm:primary"
                },
                "region": {
                    "title": "Region",
                    "type": "string",
                    "description": "The region, county, or district portion of the address.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:region"
                },
                "repositoryCreatedBy": {
                    "title": "Created by user identifier",
                    "type": "string",
                    "description": "User ID of who created the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryCreatedBy"
                },
                "repositoryLastModifiedBy": {
                    "title": "Modified by user identifier",
                    "type": "string",
                    "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:repositoryLastModifiedBy"
                },
                "state": {
                    "title": "State",
                    "type": "string",
                    "description": "The name of the State. This is a free-form field.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:state"
                },
                "stateProvince": {
                    "title": "State or province",
                    "type": "string",
                    "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
                    "examples": [
                        "US-CA",
                        "DE-BB",
                        "JP-13"
                    ],
                    "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:stateProvince"
                },
                "status": {
                    "title": "Status",
                    "type": "string",
                    "description": "An indication as to the ability to use the address.",
                    "default": "active",
                    "meta:enum": {
                        "active": "Active",
                        "incomplete": "Incomplete",
                        "pending_verification": "Pending verification",
                        "blacklisted": "Blacklisted",
                        "blocked": "Blocked"
                    },
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:status"
                },
                "statusReason": {
                    "title": "Status reason",
                    "type": "string",
                    "description": "A description of the current status.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:statusReason"
                },
                "street1": {
                    "title": "Street 1",
                    "type": "string",
                    "description": "Primary street level information, apartment number, street number, and street name.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street1"
                },
                "street2": {
                    "title": "Street 2",
                    "type": "string",
                    "description": "Optional street information second line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street2"
                },
                "street3": {
                    "title": "Street 3",
                    "type": "string",
                    "description": "Optional street information third line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street3"
                },
                "street4": {
                    "title": "Street 4",
                    "type": "string",
                    "description": "Optional street information fourth line.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "xdm:street4"
                }
            },
            "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
            "meta:xdmField": "xdm:shippingAddress"
        }
    },
    "required": [
        "personalEmail"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673380280074,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:allFieldAccess": true
}
```

+++
