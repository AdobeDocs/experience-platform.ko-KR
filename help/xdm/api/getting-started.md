---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: 스키마 레지스트리 API 시작하기
description: 이 문서에서는 스키마 레지스트리 API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Getting started with the [!DNL Schema Registry] API

API를 사용하여 다양한 XDM(Experience Data Model) 리소스를 만들고 관리할 수 있습니다. [!DNL Schema Registry] 이 문서에서는 [!DNL Schema Registry] API를 호출하기 전에 알아야 할 핵심 개념을 소개합니다.

## 전제 조건

개발자 안내서를 사용하려면 다음 Adobe Experience Platform 구성 요소에 대한 작업 지식이 필요합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../schema/composition.md):XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

XDM은 JSON 스키마 포맷을 사용하여 인제스트된 고객 경험 데이터의 구조를 설명하고 검증합니다. 따라서 이 기본 기술을 보다 잘 이해하려면 [공식 JSON 스키마 설명서를](https://json-schema.org/) 검토해야 합니다.

## 샘플 API 호출 읽기

API 설명서는 요청의 서식을 지정하는 방법을 시연하기 위한 예제 API 호출을 제공합니다. [!DNL Schema Registry] 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기 방법에 대한 섹션을 참조하십시오.

## 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Schema Registry]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 설명서를 참조하십시오](../../sandboxes/home.md).

사용자에 대한 모든 조회(GET) 요청은 추가 [!DNL Schema Registry] `Accept` 헤더가 필요하며, 이 헤더 값은 API에서 반환되는 정보의 형식을 결정합니다. 자세한 내용은 [아래의 헤더](#accept) 수락 섹션을 참조하십시오.

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

## 테넌트 ID 확인 {#know-your-tenant_id}

API 가이드 전체에서 A에 대한 참조가 표시됩니다 `TENANT_ID`. 이 ID는 사용자가 만든 리소스가 IMS 조직 내에 올바르게 지정되고 포함되어 있는지 확인하는 데 사용됩니다. ID를 모르는 경우 다음 GET 요청을 수행하여 ID에 액세스할 수 있습니다.

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

성공적인 응답은 조직의 사용 방법에 대한 정보를 반환합니다 [!DNL Schema Registry]. 여기에는 사용자 `tenantId` 의 값이 포함된 속성이 포함됩니다 `TENANT_ID`.

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

## Adobe의 `CONTAINER_ID` {#container}

API를 [!DNL Schema Registry] `CONTAINER_ID`호출하려면 API 호출을 수행할 수 있는 컨테이너는 두 가지가 있습니다.컨테이너 `global` 및 `tenant` 컨테이너.

### 전역 컨테이너

이 `global` 컨테이너에는 모든 표준 Adobe 및 [!DNL Experience Platform] 파트너가 제공하는 클래스, 믹싱, 데이터 유형 및 스키마가 들어 있습니다. 컨테이너에 대해서만 목록 및 조회(GET) 요청만 수행할 수 `global` 있습니다.

컨테이너를 사용하는 호출의 예는 `global` 다음과 같습니다.

```http
GET /global/classes
```

### 테넌트 컨테이너

고유한과 혼동하지 않도록 컨테이너 `TENANT_ID`는 IMS 조직에서 정의한 모든 클래스, 믹싱, 데이터 유형, 스키마 및 설명자를 `tenant` 보유합니다. 이는 다른 IMS 조직에서 볼 수 없거나 관리할 수 없음을 의미합니다. 컨테이너에 만드는 리소스에 대해 모든 CRUD 작업(GET, POST, PUT, PATCH, DELETE)을 수행할 수 `tenant` 있습니다.

컨테이너를 사용하는 호출의 예는 `tenant` 다음과 같습니다.

```http
POST /tenant/mixins
```

컨테이너에서 클래스, 혼합, 스키마 또는 데이터 유형을 만들 때 `tenant` 컨테이너에 [!DNL Schema Registry] 저장되고 `$id` URI가 할당되어 사용자의 URL이 `TENANT_ID`포함됩니다. 이 `$id` 는 API 전체에서 특정 리소스를 참조하는 데 사용됩니다. 값의 예는 다음 섹션에 제공됩니다. `$id`

## 리소스 식별 {#resource-identification}

XDM 리소스는 다음과 같이 URI 형식의 `$id` 속성으로 식별됩니다.

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

URI를 보다 REST에 사용하기 위해 스키마에는 다음 속성에 URI가 점 표기법 인코딩되어 있습니다. `meta:altId`

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

API [!DNL Schema Registry] 호출은 URL 인코딩 `$id` URI 또는 `meta:altId` (점 표기법 형식)를 지원합니다. 다음과 같이 API에 REST 호출을 할 때 URL 인코딩 `$id` URI를 사용하는 것이 좋습니다.

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 헤더 수락 {#accept}

API에서 목록 및 조회(GET) 작업을 수행할 때 API에서 반환되는 데이터의 형식을 결정하려면 [!DNL Schema Registry] `Accept` 헤더가 필요합니다. 특정 리소스를 조회하는 경우 버전 번호도 `Accept` 헤더에 포함되어야 합니다.

다음 표는 버전 번호가 있는 헤더 값을 비롯하여 호환 가능한 `Accept` 헤더 값을 나열하고, API가 사용될 때 반환할 내용에 대한 설명을 제공합니다.

| 수락 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | ID 목록만 반환합니다. 리소스를 나열하는 데 가장 일반적으로 사용됩니다. |
| `application/vnd.adobe.xed+json` | 원본 및 포함된 전체 JSON 스키마 목록 `$ref` 을 `allOf` 반환합니다. 전체 리소스 목록을 반환하는 데 사용됩니다. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | 및 가 있는 원시 XDM `$ref` 을 `allOf`참조하십시오. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 속성 및 `allOf` 해결되었습니다. 제목과 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 및 가 있는 원시 XDM `$ref` 을 `allOf`참조하십시오. 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 속성 및 `allOf` 해결되었습니다. 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 속성 및 `allOf` 해결되었습니다. 설명자가 포함되어 있습니다. |

>[!NOTE]
>
>주 버전만 제공하는 경우(예: 1, 2, 3) 레지스트리는 최신 마이너 버전(예:.1, .2, .3)을 자동으로 설정할 수 있습니다.

## XDM 필드 제한 및 우수 사례

스키마의 필드는 해당 객체 내에 `properties` 나열됩니다. 각 필드는 필드가 포함할 수 있는 데이터를 설명하고 제한하는 특성을 포함하는 개체입니다.

API에서 필드 유형 정의에 대한 자세한 내용은 가장 일반적으로 사용되는 데이터 유형에 대한 코드 샘플 및 선택적 제약 조건 등 이 안내서의 [부록에](appendix.md) 나와 있습니다.

다음 샘플 필드는 올바른 형식의 XDM 필드를 보여주며, 아래에 제공된 이름 지정 제한 및 우수 사례에 대한 자세한 내용을 참조하십시오. 유사한 속성을 포함하는 다른 리소스를 정의할 때도 이러한 방법을 적용할 수 있습니다.

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

* 필드 개체의 이름에는 영숫자, 대시 또는 밑줄 문자가 포함될 수 있지만 밑줄로 시작할 **수** 없습니다.
   * **정답:**`fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **틀림:** `_fieldName`
* field 개체의 이름에 cameraCase가 더 적합합니다. 예: `fieldName`
* 이 필드에는 제목 `title`케이스로 작성된 항목이 포함되어야 합니다. 예: `Field Name`
* 이 필드는 필수 항목입니다 `type`.
   * 특정 유형을 정의하려면 선택 사항이 필요할 수 있습니다 `format`.
   * 데이터의 특정 형식이 필요한 경우 배열로 추가할 `examples` 수 있습니다.
   * 레지스트리에서 데이터 유형을 사용하여 필드 유형을 정의할 수도 있습니다. 자세한 내용은 데이터 유형 끝점 안내서 [에서 데이터 유형](./data-types.md#create) 만들기에 대한 섹션을 참조하십시오.
* 는 필드 데이터에 대한 필드 및 관련 정보에 대해 `description` 설명합니다. 스키마에 액세스하는 모든 사람이 필드의 의도를 이해할 수 있도록 명확한 언어로 전체 문장으로 작성해야 합니다.

API에서 다양한 필드 유형을 정의하는 방법에 대한 자세한 내용은 [필드 제한](../schema/field-constraints.md) 사항에 대한 문서를 참조하십시오.

## 다음 단계

API를 사용하여 [!DNL Schema Registry] 호출을 시작하려면 사용 가능한 끝점 가이드 중 하나를 선택합니다.
