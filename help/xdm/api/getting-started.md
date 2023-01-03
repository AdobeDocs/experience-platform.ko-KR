---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;
solution: Experience Platform
title: 스키마 레지스트리 API 시작하기
description: 이 문서에서는 스키마 레지스트리 API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 0%

---

# 시작하기 [!DNL Schema Registry] API

다음 [!DNL Schema Registry] API를 사용하면 다양한 XDM(Experience Data Model) 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 을 호출하기 전에 알아야 하는 핵심 개념을 소개합니다 [!DNL Schema Registry] API.

## 전제 조건

개발자 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../schema/composition.md): XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

XDM은 JSON 스키마 형식을 사용하여 수집된 고객 경험 데이터의 구조를 설명하고 확인합니다. 따라서 다음을 검토하는 것이 좋습니다 [공식 JSON 스키마 설명서](https://json-schema.org/) 이 기초 기술을 더 잘 이해하려고

## 샘플 API 호출 읽기

다음 [!DNL Schema Registry] API 설명서는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

## 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]에 속했던 것 포함 [!DNL Schema Registry]은 특정 가상 샌드박스로 구분됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 설명서](../../sandboxes/home.md).

에 대한 모든 조회(GET) 요청 [!DNL Schema Registry] 추가 필요 `Accept` 헤더. 값은 API에서 반환되는 정보의 형식을 결정합니다. 자세한 내용은 [Accept header](#accept) 자세한 내용은 아래 섹션을 참조하십시오.

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## TENANT_ID 인식 {#know-your-tenant_id}

API 안내서에서 `TENANT_ID`. 이 ID는 사용자가 만드는 리소스가 제대로 식별되고 IMS 조직 내에 포함되어 있는지 확인하는 데 사용됩니다. ID를 모를 경우 다음 GET 요청을 수행하여 ID에 액세스할 수 있습니다.

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

성공적인 응답은 조직이 [!DNL Schema Registry]. 여기에는 다음이 포함됩니다 `tenantId` 속성, 값이 사용자 `TENANT_ID`.

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

호출 [!DNL Schema Registry] API에는 `CONTAINER_ID`. API 호출을 수행할 수 있는 컨테이너는 두 가지가 있습니다. a `global` 컨테이너 및 `tenant` 컨테이너.

### 전역 컨테이너

다음 `global` 컨테이너에는 모든 표준 Adobe 및 [!DNL Experience Platform] 파트너가 제공한 클래스, 스키마 필드 그룹, 데이터 유형 및 스키마. 에 대해서만 목록 및 조회(GET) 요청만 수행할 수 있습니다 `global` 컨테이너.

를 사용하는 호출의 예 `global` 컨테이너는 다음과 같습니다.

```http
GET /global/classes
```

### 테넌트 컨테이너

당신의 독특한 것과 혼동하지 마세요 `TENANT_ID`, `tenant` 컨테이너에는 IMS 조직에서 정의한 모든 클래스, 필드 그룹, 데이터 형식, 스키마 및 설명자가 들어 있습니다. 이러한 기능은 각 조직에 고유하며 다른 IMS 조직에서 보거나 관리할 수 없습니다. 에서 만드는 리소스에 대해 모든 CRUD 작업(GET, POST, PUT, PATCH, DELETE)을 수행할 수 있습니다 `tenant` 컨테이너.

를 사용하는 호출의 예 `tenant` 컨테이너는 다음과 같습니다.

```http
POST /tenant/fieldgroups
```

에서 클래스, 필드 그룹, 스키마 또는 데이터 유형을 만들 때 `tenant` 컨테이너, 저장됨 [!DNL Schema Registry] 및 할당 `$id` 를 포함하는 URI `TENANT_ID`. 이 `$id` 는 API 전체에서 특정 리소스를 참조하는 데 사용됩니다. 예 `$id` 값은 다음 섹션에 제공됩니다.

## 리소스 식별 {#resource-identification}

XDM 리소스는 `$id` 다음 예와 같이 URI 형식의 속성입니다.

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

URI를 보다 REST 친화적으로 만들기 위해 스키마에는 라는 속성에서 URI의 점 표기법 인코딩도 있습니다. `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

호출 [!DNL Schema Registry] API는 URL로 인코딩된 항목을 지원합니다 `$id` URI 또는 `meta:altId` (점 표기법 형식) 가장 좋은 방법은 URL로 인코딩된 항목을 사용하는 것입니다 `$id` 다음과 같이 API에 REST 호출을 지정할 때 URI가 다음과 같습니다.

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Accept header {#accept}

에서 목록 및 조회(GET) 작업을 수행하는 경우 [!DNL Schema Registry] API, `Accept` 헤더는 API에서 반환되는 데이터의 형식을 결정하는 데 필요합니다. 특정 리소스를 찾을 때는 버전 번호도 `Accept` 헤더.

다음 표에는 호환되는 목록이 나와 있습니다 `Accept` 헤더 값(버전 번호가 있는 값 포함)과 API가 사용될 때 반환될 내용에 대한 설명.

| Accept | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | ID 목록만 반환합니다. 리소스 목록은 가장 일반적으로 사용됩니다. |
| `application/vnd.adobe.xed+json` | 원본이 있는 전체 JSON 스키마 목록 반환 `$ref` 및 `allOf` 포함됩니다. 전체 리소스 목록을 반환하는 데 사용됩니다. |
| `application/vnd.adobe.xed+json; version=1` | 원시 XDM 및 `$ref` 및 `allOf`. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 속성 및 `allOf` 해결됨. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | 원시 XDM 및 `$ref` 및 `allOf`. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 속성 및 `allOf` 해결됨. 제목 또는 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 속성 및 `allOf` 해결됨. 설명자가 포함되어 있습니다. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 및 `allOf` 해결됨, 에는 제목 및 설명이 있습니다. 사용되지 않는 필드는 `meta:status` 속성 `deprecated`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>플랫폼에서는 현재 각 스키마에 대해 하나의 주요 버전만 지원합니다(`1`). 따라서 값 `version` 항상 `1` 스키마의 최신 부 버전을 반환하기 위해 조회 요청을 수행할 때. 스키마 버전 관리에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### 스키마 버전 관리 {#versioning}

스키마 버전은 `Accept` 스키마 레지스트리 API 및 의 헤더 `schemaRef.contentType` 다운스트림 Platform 서비스 API 페이로드의 속성.

현재 Platform은 단일 주요 버전(`1`) 내의 아무 곳에나 삽입할 수 있습니다. 에 따라 [스키마 진화 규칙](../schema/composition.md#evolution)를 지정하는 경우 각 스키마 업데이트는 원본에 영향을 주지 않아야 합니다. 즉, 새로운 부 버전의 스키마(`1.2`, `1.3`등) 이전 부 버전과 항상 이전 버전과 호환됩니다. 따라서 `version=1`를 설정하는 경우 스키마 레지스트리는 항상 **최신** 주요 버전 `1` 의 경우, 이전 부 버전이 반환되지 않음을 의미합니다.

>[!NOTE]
>
>스키마 진화에 대한 비파괴 요구 사항은 데이터 세트에 의해 스키마가 참조되고 다음 중 하나가 참인 후에만 적용됩니다.
>
>* 데이터를 데이터 집합에 수집했습니다.
>* 데이터 세트가 실시간 고객 프로필에서 사용할 수 있도록 활성화되었습니다(데이터가 수집되지 않은 경우에도).
>
>스키마가 위의 기준 중 하나를 충족하는 데이터 세트와 연결되어 있지 않으면 변경할 수 있습니다. 그러나 모든 경우에 `version` 구성 요소는 여전히 남아 있습니다 `1`.

## XDM 필드 제한 및 우수 사례

스키마의 필드는 스키마 내에 나열됩니다 `properties` 개체. 각 필드는 필드가 포함할 수 있는 데이터를 설명하고 제한하는 속성을 포함하는 객체입니다. 다음 안내서를 참조하십시오. [api에서 사용자 지정 필드 정의](../tutorials/custom-fields-api.md) 가장 일반적으로 사용되는 데이터 유형에 대한 코드 샘플 및 선택적 제한 조건.

다음 샘플 필드는 올바른 형식의 XDM 필드를 보여주며 아래에 제공된 이름 지정 제한 및 우수 사례에 대한 자세한 내용을 참조하십시오. 유사한 속성을 포함하는 다른 리소스를 정의할 때에도 이러한 방법을 적용할 수 있습니다.

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

* 필드 개체 이름에는 영숫자, 대시 또는 밑줄이 포함될 수 있지만 **그렇지 않음** 밑줄로 시작합니다.
   * **올바른:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **잘못된:** `_fieldName`
* field 개체의 이름은 camelCase가 선호됩니다. 예: `fieldName`
* 필드에는 `title`: 제목 사례에 기록됩니다. 예: `Field Name`
* 이 필드에는 `type`.
   * 특정 유형을 정의하려면 선택 사항이 필요할 수 있습니다 `format`.
   * 데이터의 특정 포맷이 필요한 경우 `examples` 배열로 추가할 수 있습니다.
   * 레지스트리에서 데이터 유형을 사용하여 필드 유형을 정의할 수도 있습니다. 의 섹션을 참조하십시오. [데이터 유형 만들기](./data-types.md#create) 자세한 내용은 데이터 유형 엔드포인트 안내서를 참조하십시오.
* 다음 `description` 필드 데이터와 관련된 필드 및 관련 정보를 설명합니다. 스키마에 액세스하는 모든 사람이 필드의 의도를 이해할 수 있도록 명확한 언어로 전체 문장을 작성해야 합니다.

## 다음 단계

를 사용하여 호출을 시작하려면 [!DNL Schema Registry] API를 사용하려면 사용 가능한 엔드포인트 가이드 중 하나를 선택합니다.
