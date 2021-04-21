---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;;home;popular topics;api;XDM;XDM system;experience data model;data Model;schema registry;Schema Registry;Registry
solution: Experience Platform
title: 스키마 레지스트리 API 시작하기
description: 이 문서에서는 스키마 레지스트리 API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---

# [!DNL Schema Registry] API 시작하기

[!DNL Schema Registry] API를 사용하여 다양한 XDM(Experience Data Model) 리소스를 만들고 관리할 수 있습니다. 이 문서에서는 [!DNL Schema Registry] API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.

## 전제 조건

개발자 안내서를 사용하려면 다음 Adobe Experience Platform 구성 요소에 대한 작업 지식이 필요합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../schema/composition.md):XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

XDM은 JSON 스키마 형식을 사용하여 인제스트된 고객 경험 데이터의 구조를 설명하고 검증합니다. 따라서 이 기본 기술을 더 잘 이해하려면 [공식 JSON 스키마 설명서](https://json-schema.org/)를 검토해야 합니다.

## 샘플 API 호출 읽기

[!DNL Schema Registry] API 설명서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법을 참조하십시오.

## 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Schema Registry]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 설명서](../../sandboxes/home.md)를 참조하십시오.

[!DNL Schema Registry]에 대한 모든 조회(GET) 요청에는 API에서 반환되는 정보의 형식을 결정하는 추가 `Accept` 헤더가 필요합니다. 자세한 내용은 아래의 [헤더](#accept) 수락 섹션을 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## TENANT_ID {#know-your-tenant_id} 알아보기

API 안내선 전체에서 `TENANT_ID`에 대한 참조가 표시됩니다. 이 ID는 사용자가 만든 리소스가 적절하게 대체되고 IMS 조직 내에 포함되도록 하는 데 사용됩니다. ID를 모를 경우 다음 GET 요청을 수행하여 ID에 액세스할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 조직의 [!DNL Schema Registry] 사용과 관련된 정보를 반환합니다. 여기에는 `tenantId` 속성이 포함되며 이 속성의 값은 `TENANT_ID`입니다.

```JSON
{
  "imsOrg":"{IMS_ORG}",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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

## `CONTAINER_ID` {#container} 이해

[!DNL Schema Registry] API를 호출하려면 `CONTAINER_ID`을 사용해야 합니다. API 호출을 수행할 수 있는 컨테이너는 두 개입니다.`global` 컨테이너 및 `tenant` 컨테이너

### 전역 컨테이너

`global` 컨테이너에는 모든 표준 Adobe이 들어 있으며 제공된 클래스, 믹싱, 데이터 유형 및 스키마가 [!DNL Experience Platform] 파트너에 포함되어 있습니다. `global` 컨테이너에 대해서만 목록 및 조회(GET) 요청만 수행할 수 있습니다.

`global` 컨테이너를 사용하는 호출의 예는 다음과 같습니다.

```http
GET /global/classes
```

### 테넌트 컨테이너

고유한 `TENANT_ID`과 혼동하지 않도록 `tenant` 컨테이너는 IMS 조직에서 정의한 모든 클래스, 믹싱, 데이터 유형, 스키마 및 설명자를 보유합니다. 이러한 구성 요소는 각 조직에 고유하며, 이는 다른 IMS Orgs에서 보거나 관리할 수 없음을 의미합니다. `tenant` 컨테이너에 만든 리소스에 대해 모든 CRUD 작업(GET, POST, PUT, PATCH, DELETE)을 수행할 수 있습니다.

`tenant` 컨테이너를 사용하는 호출의 예는 다음과 같습니다.

```http
POST /tenant/mixins
```

`tenant` 컨테이너에서 클래스, 혼합, 스키마 또는 데이터 유형을 만들 때 [!DNL Schema Registry]에 저장되고 `TENANT_ID`이 포함된 `$id` URI가 할당됩니다. 이 `$id`는 API 전체에서 특정 리소스를 참조하기 위해 사용됩니다. `$id` 값의 예는 다음 섹션에 제공됩니다.

## 리소스 ID {#resource-identification}

XDM 리소스는 다음과 같은 URI 형식으로 `$id` 속성으로 식별됩니다.

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

URI를 보다 REST에 사용하기 위해 스키마에는 `meta:altId`이라는 속성에 URI의 도트 표기법 인코딩도 있습니다.

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

[!DNL Schema Registry] API 호출은 URL 인코딩 `$id` URI 또는 `meta:altId`(도트 표기법 형식)을 지원합니다. 다음과 같이 API에 REST 호출을 할 때 URL 인코딩 `$id` URI를 사용하는 것이 좋습니다.

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 헤더 {#accept} 수락

[!DNL Schema Registry] API에서 목록 및 조회(GET) 작업을 수행할 때 API에서 반환되는 데이터의 형식을 결정하려면 `Accept` 헤더가 필요합니다. 특정 리소스를 검색할 때 버전 번호도 `Accept` 헤더에 포함되어야 합니다.

다음 표에는 버전 번호가 있는 값을 포함하여 호환되는 `Accept` 헤더 값이 나와 있으며 API가 사용될 때 반환할 내용에 대한 설명이 나와 있습니다.

| Accept | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | ID 목록만 반환합니다. 리소스를 나열하는 데 가장 일반적으로 사용됩니다. |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이 포함된 전체 JSON 스키마 목록을 반환합니다. 전체 리소스 목록을 반환하는 데 사용됩니다. |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`의 원시 XDM입니다. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 속성 및  `allOf` 해결됨. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version=1` | `$ref` 및 `allOf`의 원시 XDM입니다. 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 속성 및  `allOf` 해결됨. 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 속성 및  `allOf` 해결됨. 설명자가 포함되어 있습니다. |

>[!NOTE]
>
>플랫폼은 현재 각 스키마(`1`)에 대해 하나의 주요 버전만 지원합니다. 따라서 스키마의 최신 부 버전을 반환하려면 조회 요청을 수행할 때 `version`의 값은 항상 `1`이어야 합니다. 스키마 버전 관리에 대한 자세한 내용은 아래 하위 섹션을 참조하십시오.

### 스키마 버전 관리 {#versioning}

스키마 버전은 스키마 레지스트리 API의 `Accept` 헤더와 다운스트림 플랫폼 서비스 API 페이로드의 `schemaRef.contentType` 속성에서 참조됩니다.

현재 플랫폼은 각 스키마에 대해 단일 주요 버전(`1`)만 지원합니다. 스키마 진행](../schema/composition.md#evolution)의 [규칙에 따르면 스키마에 대한 각 업데이트는 비파괴적이어야 합니다. 즉, 새로운 부 버전의 스키마(`1.2`, `1.3` 등) 이전 보조 버전과 항상 이전 버전과 호환됩니다. 따라서 `version=1`을 지정하는 경우 스키마 레지스트리는 항상 스키마의 **최신** 주 버전 `1`을 반환합니다. 즉, 이전 부 버전은 반환되지 않습니다.

>[!NOTE]
>
>스키마 진화에 대한 비파괴 요구 사항은 데이터 세트에 의해 스키마가 참조되고 다음 중 하나가 참인 후에만 적용됩니다.
>
>* 데이터를 데이터 세트에 수집했습니다.
>* 데이터 세트를 실시간 고객 프로필에서 사용할 수 있습니다(데이터를 인제스트하지 않은 경우에도).

>
>
스키마가 위의 조건 중 하나를 충족하는 데이터 세트와 연결되어 있지 않으면 스키마를 변경할 수 있습니다. 그러나 모든 경우 `version` 구성 요소는 여전히 `1`에 있습니다.

## XDM 필드 제한 및 우수 사례

스키마의 필드는 해당 `properties` 개체 내에 나열됩니다. 각 필드는 필드가 포함할 수 있는 데이터를 설명하고 제한하는 특성을 포함하는 객체입니다.

API에서 필드 유형을 정의하는 방법에 대한 자세한 내용은 이 안내서의 [필드 제한 조건 안내서](../schema/field-constraints.md)에서 코드 샘플 및 가장 일반적으로 사용되는 데이터 유형에 대한 선택적 제약 조건을 참조하십시오.

다음 샘플 필드는 올바른 형식의 XDM 필드를 보여 주며, 아래에 제공된 제한 조건 및 우수 사례에 대한 자세한 내용을 보여 줍니다. 비슷한 속성을 포함하는 다른 리소스를 정의할 때도 이러한 방법을 적용할 수 있습니다.

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

* 필드 개체의 이름은 영숫자, 대시 또는 밑줄 문자를 포함할 수 있지만 **은 밑줄로 시작할 수 없습니다.**
   * **정답:** `fieldName`,  `field_name2`,  `Field-Name`,  `field-name_3`
   * **오답:** `_fieldName`
* field 개체의 이름에 cameraCase가 사용됩니다. 예: `fieldName`
* 필드에는 제목 사례에 쓰여진 `title`이 포함되어야 합니다. 예: `Field Name`
* 필드에 `type`이 필요합니다.
   * 특정 유형을 정의하려면 선택 사항인 `format`이 필요할 수 있습니다.
   * 데이터의 특정 형식이 필요한 경우 `examples`을(를) 배열로 추가할 수 있습니다.
   * 레지스트리에서 모든 데이터 유형을 사용하여 필드 유형을 정의할 수도 있습니다. 자세한 내용은 데이터 유형 끝점 안내서의 [데이터 유형 만들기](./data-types.md#create)에 대한 섹션을 참조하십시오.
* `description`은 필드 데이터와 관련된 필드 정보를 설명합니다. 스키마에 액세스하는 모든 사람이 필드의 의도를 이해할 수 있도록 명확한 언어로 전체 문장으로 작성해야 합니다.

API에서 다른 필드 유형을 정의하는 방법에 대한 자세한 내용은 [필드 제한 조건](../schema/field-constraints.md)에 있는 문서를 참조하십시오.

## 다음 단계

[!DNL Schema Registry] API를 사용하여 호출을 시작하려면 사용 가능한 끝점 안내선 중 하나를 선택합니다.
