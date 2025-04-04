---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;
solution: Experience Platform
title: 스키마 레지스트리 API 시작하기
description: 이 문서에서는 스키마 레지스트리 API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1364'
ht-degree: 5%

---

# [!DNL Schema Registry] API 시작

[!DNL Schema Registry] API를 사용하면 다양한 XDM(Experience Data Model) 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 [!DNL Schema Registry] API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.

## 전제 조건

개발자 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해가 필요합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform]은(는) 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

XDM은 JSON 스키마 형식을 사용하여 수집된 고객 경험 데이터의 구조를 설명하고 유효성을 검사합니다. 따라서 이 기본 기술을 더 잘 이해하려면 [공식 JSON 스키마 설명서](https://json-schema.org/)를 검토하는 것이 좋습니다.

## 샘플 API 호출 읽기

[!DNL Schema Registry] API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

## 필수 헤더에 대한 값 수집

[!DNL Experience Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Schema Registry]에 속하는 리소스를 포함한 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리됩니다. [!DNL Experience Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 설명서](../../sandboxes/home.md)를 참조하세요.

[!DNL Schema Registry]에 대한 모든 조회(GET) 요청에는 API에서 반환되는 정보의 형식을 결정하는 추가 `Accept` 헤더가 필요합니다. 자세한 내용은 아래의 [Accept 헤더](#accept) 섹션을 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 테넌트 ID 확인 {#know-your-tenant_id}

API 안내서 전체에서 `TENANT_ID`에 대한 참조를 볼 수 있습니다. 이 ID는 사용자가 만드는 리소스의 이름 간격이 제대로 지정되고 조직 내에 포함되어 있는지 확인하는 데 사용됩니다. ID를 모를 경우 다음 GET 요청을 수행하여 액세스할 수 있습니다.

**API 형식**

```http
GET /stats
```

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답이 성공하면 조직에서 [!DNL Schema Registry]을(를) 사용하는 것과 관련된 정보가 반환됩니다. 여기에는 `tenantId` 특성이 포함되며, 이 값은 `TENANT_ID`입니다.

```JSON
{
  "imsOrg":"{ORG_ID}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## `CONTAINER_ID` 이해 {#container}

[!DNL Schema Registry] API를 호출하려면 `CONTAINER_ID`을(를) 사용해야 합니다. API 호출을 수행할 수 있는 컨테이너는 두 개입니다. `global` 컨테이너와 `tenant` 컨테이너입니다.

### 전역 컨테이너

`global` 컨테이너에는 모든 표준 Adobe 및 [!DNL Experience Platform] 파트너가 제공한 클래스, 스키마 필드 그룹, 데이터 형식 및 스키마가 들어 있습니다. `global` 컨테이너에 대해서만 목록 및 조회(GET) 요청을 수행할 수 있습니다.

`global` 컨테이너를 사용하는 호출의 예는 다음과 같습니다.

```http
GET /global/classes
```

### 임차인 컨테이너

고유한 `TENANT_ID`과(와) 혼동하지 않도록 `tenant` 컨테이너에는 조직에서 정의한 모든 클래스, 필드 그룹, 데이터 형식, 스키마 및 설명자가 있습니다. 이는 각 조직에 고유하며, 다른 조직에서 표시하거나 관리할 수 없음을 의미합니다. `tenant` 컨테이너에서 만든 리소스에 대해 모든 CRUD 작업(GET, POST, PUT, PATCH, DELETE)을 수행할 수 있습니다.

`tenant` 컨테이너를 사용하는 호출의 예는 다음과 같습니다.

```http
POST /tenant/fieldgroups
```

`tenant` 컨테이너에서 클래스, 필드 그룹, 스키마 또는 데이터 형식을 만들면 [!DNL Schema Registry]에 저장되고 `TENANT_ID`을(를) 포함하는 `$id` URI가 할당됩니다. 이 `$id`은(는) API 전체에서 특정 리소스를 참조하는 데 사용됩니다. `$id` 값의 예는 다음 섹션에 제공됩니다.

## 리소스 식별 {#resource-identification}

XDM 리소스는 다음 예제와 같이 URI 형식으로 `$id` 특성으로 식별됩니다.

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

URI를 보다 REST 친화적으로 만들기 위해 스키마에는 `meta:altId` 속성에서 URI의 점 표기법 인코딩도 있습니다.

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

[!DNL Schema Registry] API 호출은 URL로 인코딩된 `$id` URI 또는 `meta:altId`(점 표기법 형식)을 지원합니다. 가장 좋은 방법은 다음과 같이 API에 대한 REST 호출을 수행할 때 URL로 인코딩된 `$id` URI를 사용하는 것입니다.

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept 헤더 {#accept}

[!DNL Schema Registry] API에서 목록 및 조회(GET) 작업을 수행할 때 API에서 반환되는 데이터의 형식을 결정하려면 `Accept` 헤더가 필요합니다. 특정 리소스를 조회할 때 버전 번호도 `Accept` 헤더에 포함되어야 합니다.

다음 표에는 버전 번호가 포함된 호환 가능한 `Accept` 헤더 값과 API가 사용될 때 반환되는 값에 대한 설명이 나와 있습니다.

| 수락 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | ID 목록만 반환합니다. 리소스를 나열하는 데 가장 일반적으로 사용됩니다. |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이(가) 포함된 전체 JSON 스키마 목록을 반환합니다. 전체 리소스 목록을 반환하는 데 사용됩니다. |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`이(가) 있는 원시 XDM. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref`개 특성 및 `allOf`개 확인됨. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | `$ref` 및 `allOf`이(가) 있는 원시 XDM. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref`개 특성 및 `allOf`개 확인됨. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref`개 특성 및 `allOf`개 확인됨. 설명자가 포함됩니다. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 및 `allOf`이(가) 확인되었으며 제목 및 설명이 있습니다. 사용되지 않는 필드는 `deprecated`의 `meta:status` 특성으로 표시됩니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>Experience Platform은 현재 각 스키마(`1`)에 대해 하나의 주 버전만 지원합니다. 따라서 스키마의 최신 부 버전을 반환하려면 조회 요청을 수행할 때 `version`의 값이 항상 `1`이어야 합니다. 스키마 버전 관리에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### 스키마 버전 관리 {#versioning}

스키마 버전은 스키마 레지스트리 API의 `Accept` 헤더와 다운스트림 Experience Platform 서비스 API 페이로드의 `schemaRef.contentType` 속성에서 참조됩니다.

현재 Experience Platform에서는 각 스키마에 대해 단일 주 버전(`1`)만 지원합니다. [스키마 진화의 규칙](../schema/composition.md#evolution)에 따르면 스키마에 대한 각 업데이트는 비파괴적이어야 합니다. 즉, 스키마의 새 부 버전(`1.2`, `1.3` 등)은 항상 이전 부 버전과 역으로 호환됩니다. 따라서 `version=1`을(를) 지정하면 스키마 레지스트리는 항상 스키마의 **최신** 주 버전 `1`을(를) 반환합니다. 즉, 이전의 부 버전은 반환되지 않습니다.

>[!NOTE]
>
>스키마 진화에 대한 비파괴적인 요구 사항은 데이터 세트에서 스키마를 참조한 후에만 적용되며 다음 경우 중 하나가 적용됩니다.
>
>* 데이터가 데이터 세트에 수집되었습니다.
>* 데이터 세트가 실시간 고객 프로필에서 사용할 수 있도록 활성화되었습니다(데이터가 수집되지 않은 경우에도).
>
>위의 기준 중 하나를 충족하는 데이터 세트와 스키마가 연관되지 않은 경우 모든 변경 작업을 수행할 수 있습니다. 그러나 모든 경우에 `version` 구성 요소는 여전히 `1`에 남아 있습니다.

## XDM 필드 제한 및 우수 사례

스키마의 필드가 `properties` 개체 내에 나열됩니다. 각 필드는 그 자체로 하나의 객체로, 필드에 포함될 수 있는 데이터를 설명하고 제한하는 속성을 포함합니다. 코드 샘플 및 가장 일반적으로 사용되는 데이터 형식에 대한 선택적 제약 조건의 경우 [API에서 사용자 지정 필드 정의](../tutorials/custom-fields-api.md)에 대한 안내서를 참조하세요.

다음 샘플 필드는 아래에 제공된 이름 지정 제한 및 우수 사례에 대한 자세한 내용과 함께 올바른 형식의 XDM 필드를 보여줍니다. 이러한 사례는 유사한 속성을 포함하는 다른 리소스를 정의할 때도 적용할 수 있습니다.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* 필드 개체의 이름에는 영숫자, 대시 또는 밑줄 문자가 포함될 수 있지만 **밑줄로 시작할 수 없습니다**.
   * **수정:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **올바르지 않음:** `_fieldName`
* 필드 이름은 대소문자를 구분하지 않으며 스키마의 동일한 수준에서 다른 이름을 가져야 합니다.
* field 객체의 이름에는 camelCase가 선호됩니다. 예: `fieldName`
* 필드에는 제목 대/소문자로 작성된 `title`이(가) 포함되어야 합니다. 예: `Field Name`
* 필드에는 `type`이(가) 필요합니다.
   * 특정 형식을 정의하려면 선택적 `format`이(가) 필요할 수 있습니다.
   * 데이터의 특정 서식이 필요한 경우 `examples`을(를) 배열로 추가할 수 있습니다.
   * 필드 유형은 레지스트리의 데이터 유형을 사용하여 정의할 수도 있습니다. 자세한 내용은 데이터 형식 끝점 가이드의 [데이터 형식 만들기](./data-types.md#create)에 대한 섹션을 참조하십시오.
* `description`은(는) 필드 및 필드 데이터에 대한 관련 정보를 설명합니다. 스키마에 접근하는 누구나 현장의 의도를 이해할 수 있도록 언어가 명확한 전문장으로 작성해야 한다.

## 다음 단계

[!DNL Schema Registry] API를 사용하여 호출을 시작하려면 사용 가능한 끝점 가이드 중 하나를 선택하십시오.
