---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;
solution: Experience Platform
title: 스키마 레지스트리 API 시작하기
description: 이 문서에서는 스키마 레지스트리 API를 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# 시작하기 [!DNL Schema Registry] API

다음 [!DNL Schema Registry] API를 사용하면 다양한 XDM(Experience Data Model) 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 을 호출하기 전에 알아야 하는 핵심 개념에 대해 소개합니다. [!DNL Schema Registry] API.

## 전제 조건

개발자 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해가 필요합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

XDM은 JSON 스키마 형식을 사용하여 수집된 고객 경험 데이터의 구조를 설명하고 유효성을 검사합니다. 따라서 다음을 검토하는 것이 좋습니다. [공식 JSON 스키마 설명서](https://json-schema.org/) 이 기반 기술을 더 잘 이해할 수 있도록.

## 샘플 API 호출 읽기

다음 [!DNL Schema Registry] API 설명서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 참조하십시오.

## 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform], 다음에 속하는 항목 포함 [!DNL Schema Registry]는 특정 가상 샌드박스로 분리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 설명서](../../sandboxes/home.md).

에 대한 모든 조회(GET) 요청 [!DNL Schema Registry] 추가 필요 `Accept` 값이 API에서 반환되는 정보의 형식을 결정하는 헤더입니다. 다음을 참조하십시오. [Accept 헤더](#accept) 자세한 내용은 아래 섹션을 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 테넌트 ID 확인 {#know-your-tenant_id}

API 안내서 전체에서 다음에 대한 참조를 볼 수 있습니다. `TENANT_ID`. 이 ID는 사용자가 만드는 리소스의 이름 간격이 제대로 지정되고 IMS 조직 내에 포함되어 있는지 확인하는 데 사용됩니다. ID를 모를 경우 다음 GET 요청을 수행하여 액세스할 수 있습니다.

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

성공적인 응답은 조직의 다음 사용 방법에 대한 정보를 반환합니다. [!DNL Schema Registry]. 여기에는 다음이 포함됩니다. `tenantId` 속성. 값이 다음과 같습니다. `TENANT_ID`.

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

## 이해 `CONTAINER_ID` {#container}

에 대한 호출 [!DNL Schema Registry] API에는 `CONTAINER_ID`. API 호출을 수행할 수 있는 컨테이너에는 두 개가 있습니다. `global` 컨테이너 및 `tenant` 컨테이너.

### 전역 컨테이너

다음 `global` 컨테이너에는 모든 표준 Adobe 및 [!DNL Experience Platform] 파트너가 제공한 클래스, 스키마 필드 그룹, 데이터 유형 및 스키마. 목록 및 조회(GET) 요청만 수행할 수 있습니다. `global` 컨테이너.

를 사용하는 호출의 예 `global` 컨테이너는 다음과 같이 표시됩니다.

```http
GET /global/classes
```

### 임차인 컨테이너

귀하의 고유한 것과 혼동하지 마십시오 `TENANT_ID`, `tenant` 컨테이너에는 IMS 조직에서 정의한 모든 클래스, 필드 그룹, 데이터 유형, 스키마 및 설명자가 포함됩니다. 이는 각 조직에 고유하며, 다른 IMS 조직에서 표시하거나 관리할 수 없음을 의미합니다. 에서 만든 리소스에 대해 모든 CRUD 작업(GET, POST, PUT, PATCH, DELETE)을 수행할 수 있습니다. `tenant` 컨테이너.

를 사용하는 호출의 예 `tenant` 컨테이너는 다음과 같이 표시됩니다.

```http
POST /tenant/fieldgroups
```

클래스, 필드 그룹, 스키마 또는 데이터 형식을 `tenant` 컨테이너를 만든 후 [!DNL Schema Registry] 및 할당됨 `$id` 다음을 포함하는 URI `TENANT_ID`. 이 `$id` 는 API 전체에서 특정 리소스를 참조하는 데 사용됩니다. 예 `$id` 값은 다음 섹션에 제공됩니다.

## 리소스 식별 {#resource-identification}

XDM 리소스는 `$id` 속성은 다음 예제와 같이 URI 형식으로 표시됩니다.

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

URI를 보다 REST 친화적으로 만들기 위해 스키마에는 라는 속성에 있는 URI의 점 표기법 인코딩도 있습니다. `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

에 대한 호출 [!DNL Schema Registry] API는 URL로 인코딩된 `$id` URI 또는 `meta:altId` (점 표기법 형식). 가장 좋은 방법은 URL로 인코딩된 `$id` API에 대해 REST 호출을 수행할 때 URI는 다음과 같습니다.

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept 헤더 {#accept}

에서 목록 및 조회(GET) 작업을 수행할 때 [!DNL Schema Registry] API, `Accept` API에서 반환되는 데이터의 형식을 결정하려면 헤더가 필요합니다. 특정 리소스를 조회할 때 버전 번호도 포함되어야 합니다. `Accept` 머리글입니다.

다음 표에는 호환되는 항목이 나열되어 있습니다 `Accept` API가 사용될 때 반환할 내용에 대한 설명과 함께 버전 번호가 있는 헤더 값이 포함됩니다.

| Accept | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | ID 목록만 반환합니다. 리소스를 나열하는 데 가장 일반적으로 사용됩니다. |
| `application/vnd.adobe.xed+json` | 원본과 함께 전체 JSON 스키마 목록을 반환합니다. `$ref` 및 `allOf` 포함. 전체 리소스 목록을 반환하는 데 사용됩니다. |
| `application/vnd.adobe.xed+json; version=1` | 원시 XDM 포함 `$ref` 및 `allOf`. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 속성 및 `allOf` 해결되었습니다. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | 원시 XDM 포함 `$ref` 및 `allOf`. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 속성 및 `allOf` 해결되었습니다. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 속성 및 `allOf` 해결되었습니다. 설명자가 포함됩니다. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 및 `allOf` 해결됨, 제목 및 설명 포함. 더 이상 사용되지 않는 필드는 `meta:status` 속성 `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Platform은 현재 각 스키마에 대해 하나의 주요 버전만 지원합니다(`1`). 따라서 값은 `version` 은(는) 항상 `1` 스키마의 최신 부 버전을 반환하기 위해 조회 요청을 수행하는 경우. 스키마 버전 관리에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### 스키마 버전 관리 {#versioning}

에서 참조하는 스키마 버전 `Accept` 스키마 레지스트리 API 및 의 헤더 `schemaRef.contentType` 다운스트림 플랫폼 서비스 API 페이로드의 속성.

현재 Platform은 단일 주요 버전(`1`)을 참조하십시오. 에 따라 [스키마 진화 규칙](../schema/composition.md#evolution): 스키마에 대한 각 업데이트는 비파괴적이어야 합니다. 즉, 스키마의 새로운 부 버전(`1.2`, `1.3`등) 는 항상 이전 부 버전과 역으로 호환됩니다. 따라서 을 지정할 때 `version=1`, 스키마 레지스트리는 항상 **최신** 주요 버전 `1` 스키마의 경우: 이전 부 버전이 반환되지 않습니다.

>[!NOTE]
>
>스키마 진화에 대한 비파괴적인 요구 사항은 데이터 세트에서 스키마를 참조한 후에만 적용되며 다음 경우 중 하나가 적용됩니다.
>
>* 데이터가 데이터 세트에 수집되었습니다.
>* 데이터 세트가 실시간 고객 프로필에서 사용할 수 있도록 활성화되었습니다(데이터가 수집되지 않은 경우에도).
>
>위의 기준 중 하나를 충족하는 데이터 세트와 스키마가 연관되지 않은 경우 모든 변경 작업을 수행할 수 있습니다. 그러나 모든 경우에 `version` 구성 요소가 여전히 다음 위치에 남아 있음 `1`.

## XDM 필드 제한 및 우수 사례

스키마 필드는 해당 항목 내에 나열됩니다 `properties` 개체. 각 필드는 그 자체로 하나의 객체로, 필드에 포함될 수 있는 데이터를 설명하고 제한하는 속성을 포함합니다. 다음 안내서를 참조하십시오. [api에서 사용자 정의 필드 정의](../tutorials/custom-fields-api.md) 코드 샘플 및 가장 일반적으로 사용되는 데이터 형식에 대한 선택적 제약 조건입니다.

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

* 필드 개체의 이름에는 영숫자, 대시 또는 밑줄 문자가 포함될 수 있지만 **다음을 수행할 수 없음** 밑줄로 시작합니다.
   * **정답:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **잘못됨:** `_fieldName`
* field 객체의 이름에는 camelCase가 선호됩니다. 예: `fieldName`
* 필드에는 다음이 포함되어야 합니다. `title`, 제목 대/소문자로 작성됨. 예: `Field Name`
* 필드에는 다음이 필요합니다. `type`.
   * 특정 유형을 정의하려면 선택 사항이 필요할 수 있습니다 `format`.
   * 데이터의 특정 서식이 필요한 경우 `examples` 배열로 추가할 수 있습니다.
   * 필드 유형은 레지스트리의 데이터 유형을 사용하여 정의할 수도 있습니다. 의 섹션을 참조하십시오. [데이터 유형 만들기](./data-types.md#create) 자세한 내용은 데이터 형식 끝점 안내서를 참조하십시오.
* 다음 `description` 필드 및 필드 데이터에 대한 관련 정보를 설명합니다. 스키마에 접근하는 누구나 현장의 의도를 이해할 수 있도록 언어가 명확한 전문장으로 작성해야 한다.

## 다음 단계

을 사용하여 호출을 시작하려면 [!DNL Schema Registry] API에서 사용 가능한 엔드포인트 안내서 중 하나를 선택합니다.
