---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스키마 레지스트리 API 개발자 가이드
topic: developer guide
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# 스키마 레지스트리 API 개발자 가이드

스키마 레지스트리는 Adobe Experience Platform에서 스키마 라이브러리에 액세스하는 데 사용되며, 사용 가능한 모든 라이브러리 리소스에 액세스할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다.

스키마 레지스트리 API를 사용하여 Adobe Experience Platform 내에서 사용 가능한 모든 스키마 및 관련 리소스를 보고 관리하기 위해 기본 CRUD 작업을 수행할 수 있습니다. 여기에는 Adobe, Experience Platform 파트너 및 애플리케이션을 사용하는 벤더가 정의합니다. 또한 API 호출을 사용하여 조직의 새 스키마 및 리소스를 만들 수 있을 뿐만 아니라 이미 정의된 리소스를 보고 편집할 수도 있습니다.

이 개발자 안내서에서는 스키마 레지스트리 API 사용을 시작하는 데 도움이 되는 단계를 제공합니다. 그러면 가이드는 스키마 레지스트리를 사용하여 키 작업을 수행하기 위한 샘플 API 호출을 제공합니다.

## 전제 조건

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의](../schema/composition.md)기본 사항:XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
* [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.
* [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 스키마 레지스트리 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

## 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

## 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

스키마 레지스트리에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

스키마 레지스트리에 대한 모든 조회(GET) 요청에는 추가 승인 헤더가 필요합니다. 이 헤더의 값은 API에서 반환되는 정보의 형식을 결정합니다. 자세한 내용은 [아래의 헤더](#accept) 수락 섹션을 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형:application/json

## 테넌트 ID 알아보기 {#know-your-tenant-id}

이 안내서 전체에서 에 대한 참조가 표시됩니다 `TENANT_ID`. 이 ID는 사용자가 만든 리소스가 IMS 조직 내에 적절하게 지정되어 있는지 확인하는 데 사용됩니다. ID를 모르는 경우 다음 GET 요청을 수행하여 ID에 액세스할 수 있습니다.

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

성공적인 응답은 조직의 스키마 레지스트리 사용과 관련된 정보를 반환합니다. 여기에는 `tenantId` 속성이 포함되며, 이 속성은 사용자의 `TENANT_ID`값입니다.

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

* `tenantId`:IMS 조직에 대한 `TENANT_ID` 값.

## Understanding the `CONTAINER_ID`{#container}

스키마 레지스트리 API를 호출하려면 `CONTAINER_ID` API 호출을 수행할 수 있는 컨테이너는 두 가지가 있습니다.전역 컨테이너 **및** 테넌트 컨테이너 ****.

### 전역 컨테이너

글로벌 컨테이너에는 모든 표준 Adobe 및 Experience Platform 파트너가 제공하는 클래스, 믹싱, 데이터 유형 및 스키마가 포함되어 있습니다. 목록 및 조회(GET) 요청만 글로벌 컨테이너에 대해 수행할 수 있습니다.

### 테넌트 컨테이너

고유한 요소와 혼동하지 않도록 임차인 컨테이너는 IMS 조직에 의해 정의된 모든 클래스, 믹싱, 데이터 유형, 스키마 및 설명자를 보유합니다. `TENANT_ID` 이는 다른 IMS 조직에서 볼 수 없거나 관리할 수 없음을 의미합니다. 테넌트 컨테이너에서 만든 리소스에 대해 모든 CRUD 작업(GET, POST, PUT, PATCH, DELETE)을 수행할 수 있습니다.

테넌트 컨테이너에서 클래스, 혼합, 스키마 또는 데이터 유형을 만들 때 해당 클래스는 스키마 레지스트리에 저장되고 `$id` 해당 항목이 포함된 URI가 할당됩니다 `TENANT_ID`. 이 `$id` 기능은 API 전체에서 특정 리소스를 참조하기 위해 사용됩니다. 값의 예는 다음 섹션에 제공됩니다. `$id`

## 스키마 식별 {#schema-identification}

스키마는 다음과 같은 URI 형식으로 `$id` 속성으로 식별됩니다.
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

URI를 보다 REST에 사용하기 위해 스키마에는 URI의 점 표기법 인코딩이 `meta:altId`있습니다.
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

스키마 레지스트리 API에 대한 호출은 URL 인코딩 URI `$id` 또는 `meta:altId` (도트 표기법 형식)를 지원합니다. 다음과 같이 REST 호출을 API에 `$id` 호출할 때 URL 인코딩 URI를 사용하는 것이 좋습니다.
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 헤더 수락 {#accept}

스키마 레지스트리 API에서 목록 및 조회(GET) 작업을 수행할 때 API에서 반환되는 데이터의 형식을 결정하려면 승인 헤더가 필요합니다. 특정 리소스를 검색할 때 버전 번호도 수락 헤더에 포함되어야 합니다.

다음 표에는 버전 번호가 있는 헤더 값을 비롯하여 호환되는 수락 헤더 값이 나와 있으며, 이러한 헤더 값이 사용될 때 API가 반환할 내용에 대한 설명이 나와 있습니다.

| 수락 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | ID 목록만 반환합니다. 리소스를 나열하는 데 가장 일반적으로 사용됩니다. |
| `application/vnd.adobe.xed+json` | 원본 및 `$ref` `allOf` 포함된 전체 JSON 스키마 목록을 반환합니다. 전체 리소스 목록을 반환하는 데 사용됩니다. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | RAW XDM과 `$ref` 함께 `allOf`제공됩니다. 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 속성을 확인하고 `allOf` 해결했습니다. 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | RAW XDM과 `$ref` 함께 `allOf`제공됩니다. 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 속성을 확인하고 `allOf` 해결했습니다. 제목이나 설명이 없습니다. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 속성을 확인하고 `allOf` 해결했습니다. 설명자가 포함되어 있습니다. |

>[!NOTE] 버전 `major` (예: 1, 2, 3)만 제공하면 레지스트리가 최신 `minor` 버전(예:.1, .2, .3)을 자동으로 생성할 수 있습니다.

## XDM 필드 제한 및 모범 사례

스키마 필드는 해당 `properties` 객체 내에 나열됩니다. 각 필드는 필드가 포함할 수 있는 데이터를 설명하고 제한하는 속성이 들어 있는 개체입니다.

API에서 필드 유형을 정의하는 방법에 대한 자세한 내용은 가장 일반적으로 사용되는 데이터 유형에 대한 코드 샘플 및 선택적 제약 조건 등 이 안내서의 [부록에](appendix.md) 있습니다.

다음 샘플 필드에는 올바른 형식의 XDM 필드가 표시되어 있으며, 아래에 제공된 이름 지정 제한 및 우수 사례에 대한 자세한 내용이 나와 있습니다. 유사한 속성을 포함하는 다른 리소스를 정의할 때도 이러한 방법을 적용할 수 있습니다.

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

* 필드 개체의 이름에는 영숫자, 대시 또는 밑줄 문자가 포함될 수 있지만 밑줄로 시작할 **수는** 없습니다.
   * **정답:**`fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **오답:** `_fieldName`
* field 개체의 이름에는 cameraCase가 선호됩니다. 예: `fieldName`
* 필드에는 제목 `title`케이스로 작성된 항목이 포함되어야 합니다. 예: `Field Name`
* 이 필드에는 ID가 있어야 `type`합니다.
   * 특정 유형을 정의하려면 선택 사항이 필요할 수 `format`있습니다.
   * 데이터의 특정 형식이 필요한 경우 배열로 추가할 `examples` 수 있습니다.
   * 레지스트리에서 데이터 유형을 사용하여 필드 유형을 정의할 수도 있습니다. 자세한 내용은 이 안내서의 데이터 유형 [](create-data-type.md) 만들기에 대한 섹션을 참조하십시오.
* 는 필드 데이터와 관련된 필드 및 관련 정보에 대해 `description` 설명합니다. 스키마에 액세스하는 모든 사람이 필드의 의도를 이해할 수 있도록 명확한 언어로 문장으로 작성해야 합니다.

API에서 필드 유형을 정의하는 방법에 대한 자세한 내용은 [부록을](appendix.md) 참조하십시오.

## 다음 단계

이 문서에서는 필요한 인증 자격 증명을 포함하여 스키마 레지스트리 API를 호출하는 데 필요한 사전 요구 사항에 대해 설명했습니다. 이제 이 개발자 안내서에서 제공하는 샘플 호출을 진행하여 지침을 따라 수행할 수 있습니다. API에서 스키마를 만드는 방법에 대한 단계별 연습은 다음 [자습서를](../tutorials/create-schema-api.md)참조하십시오.
