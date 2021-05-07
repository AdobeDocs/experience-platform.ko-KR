---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;결합;결합;결합;Union;segmentMembership;timeSeriesEvents;home;XDM;XDM;experience data model;Model;Data model;Model;Model;Data Model;Model;Model;Data Data Model;Data Model;Data Model;Data Data Model;Model;Model;Data Data-Model;Data Model;Model;Data-Model;Data Model;Data-Model;Data Data-Model;Model;Model;Data Data-Model;Model;Data Data Model;Model;Model;Model;Model;Union;Union;Union;Union;Union;Union;Union;Union;Union;Union;Union;union;
solution: Experience Platform
title: 조합 API 끝점
description: 스키마 레지스트리 API의 /union 끝점을 사용하면 경험 응용 프로그램에서 XDM 결합 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 1%

---

# 조합 끝점

조합(또는 조합 뷰)은 동일한 클래스([!DNL XDM ExperienceEvent] 또는 [!DNL XDM Individual Profile])를 공유하고 [[!DNL Real-time Customer Profile]](../../profile/home.md)에 대해 활성화된 모든 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다.

이 문서에서는 다양한 작업에 대한 샘플 호출을 비롯하여 스키마 레지스트리 API에서 조합과 작업하는 데 반드시 필요한 개념을 설명합니다. XDM의 조합에 대한 일반적인 자세한 내용은 스키마 구성](../schema/composition.md#union)의 [기본 사항에 있는 조합의 섹션을 참조하십시오.

## 결합 스키마 필드

[!DNL Schema Registry]은(는) 조합 스키마 내에 3개의 키 필드를 자동으로 포함합니다.`identityMap`, `timeSeriesEvents` 및 `segmentMembership`.

### ID 맵

조합 스키마의 `identityMap`은 결합의 연결된 레코드 스키마 내에서 알려진 ID를 나타냅니다. ID 맵은 ID를 네임스페이스로 다른 배열로 구분합니다. 나열된 각 ID는 고유한 `id` 값을 포함하는 객체입니다. 자세한 내용은 [ID 서비스 설명서](../../identity-service/home.md)를 참조하십시오.

### 시계열 이벤트

`timeSeriesEvents` 배열은 결합과 연관된 레코드 스키마와 관련된 시간 시리즈 이벤트 목록입니다. 프로필 데이터를 데이터 세트로 내보낼 때 이 배열은 각 레코드에 포함됩니다. 이는 모델에 레코드 특성 외에 프로파일의 전체 동작 내역이 필요한 기계 학습과 같은 다양한 사용 사례에 유용합니다.

### 세그먼트 멤버십 맵

`segmentMembership` 맵은 세그먼트 평가 결과를 저장합니다. [세그멘테이션 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)를 사용하여 세그먼트 작업을 성공적으로 실행하면 맵이 업데이트됩니다. `segmentMembership` 또한 Platform으로 인제스트된 사전 평가 대상 세그먼트를 저장하여 Adobe Audience Manager과 같은 다른 솔루션과 통합할 수 있습니다. 자세한 내용은 [API](../../segmentation/tutorials/create-a-segment.md)를 사용하여 세그먼트 만들기에 대한 자습서를 참조하십시오.

## 조합 목록 가져오기 {#list}

스키마에서 `union` 태그를 설정하면 [!DNL Schema Registry]은 스키마를 기반으로 하는 클래스에 대해 자동으로 스키마를 추가합니다. 해당 클래스에 대한 조합이 없는 경우 새 조합이 자동으로 생성됩니다. 조합의 `$id`은 다른 [!DNL Schema Registry] 리소스의 표준 `$id`과 비슷하며, 단 하나의 차이에는 두 개의 밑줄이 추가되고 &quot;union&quot;(`__union`)이라는 단어가 추가됩니다.

`/tenant/unions` 끝점에 GET 요청을 함으로써 사용 가능한 조합 목록을 볼 수 있습니다.

**API 형식**

```http
GET /tenant/unions
```

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 달라집니다. 다음 `Accept` 헤더는 조합을 나열하는 데 사용할 수 있습니다.

| `Accept` header | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이 포함된 각 리소스에 대한 전체 JSON 클래스를 반환합니다. (제한:300) |

**응답**

성공적인 응답은 응답 본문에 HTTP 상태 200(OK) 및 `results` 배열을 반환합니다. 조합이 정의된 경우 각 조합의 세부 사항은 배열 내의 객체로 제공됩니다. 정의된 조합이 없는 경우 HTTP 상태 200(OK)은 여전히 반환되지만 `results` 배열은 비어 있게 됩니다.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## 조합 {#lookup} 검색

`$id`을 포함하는 GET 요청을 수행하고 Accept 헤더에 따라 조합의 일부 또는 전체 세부 사항을 포함하여 특정 조합을 볼 수 있습니다.

>[!NOTE]
>
>조합 조회는 `/unions` 및 `/schemas` 끝점을 사용하여 [!DNL Profile] 내보내기에서 데이터 세트로 사용할 수 있도록 합니다.

**API 형식**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{UNION_ID}` | 조회하려는 조합의 URL 인코딩 `$id` URI입니다. 공용 구조체 스키마에 대한 URI에는 &quot;__union&quot;이 추가됩니다. |

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

조합 조회 요청에는 수락 헤더에 `version`이 포함되어야 합니다.

결합 스키마 조회에 사용할 수 있는 헤더는 다음과 같습니다.

| Accept | 설명 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`이(가) 있는 원시. 제목 및 설명이 포함되어 있습니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 속성 및  `allOf` 해결됨. 제목 및 설명이 포함되어 있습니다. |

**응답**

성공적인 응답은 요청 경로에 `$id`이(가) 제공된 클래스를 구현하는 모든 스키마의 결합 보기를 반환합니다.

응답 형식은 요청에서 전송된 수락 헤더에 따라 달라집니다. 서로 다른 수락 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/fieldgroups/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/fieldgroups/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## 공용 멤버 자격 {#enable} 스키마 사용

스키마의 클래스에 대한 유니스트에 스키마를 포함하려면 `union` 태그를 스키마의 `meta:immutableTags` 속성에 추가해야 합니다. PATCH 요청에 `union` 문자열 값이 하나만 있는 `meta:immutableTags` 배열을 문제의 스키마에 추가하도록 함으로써 이 작업을 수행할 수 있습니다. 자세한 예제는 [스키마 끝점 안내서](./schemas.md#union)를 참조하십시오.

## 공용 구조체 {#list-schemas}의 스키마 목록

특정 공용 구조체의 일부인 스키마를 확인하려면 `/tenant/schemas` 끝점에 대한 GET 요청을 수행할 수 있습니다. `property` 쿼리 매개 변수를 사용하면 `meta:immutableTags` 필드와 `meta:class`가 액세스하려는 조합의 클래스와 동일한 반환 스키마만 포함하는 응답을 구성할 수 있습니다.

**API 형식**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 나열하려는 공용 스키마가 있는 클래스의 `$id`. |

**요청**

다음 요청은 [!DNL XDM Individual Profile] 클래스에 대한 유니션에 포함된 모든 스키마 목록을 검색합니다.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 달라집니다. 다음 `Accept` 헤더는 스키마 나열을 위해 사용할 수 있습니다.

| `Accept` header | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원래 `$ref` 및 `allOf`이 포함된 각 리소스에 대한 전체 JSON 스키마를 반환합니다. (제한:300) |

**응답**

성공적인 응답은 조합 멤버십에 대해 활성화된 지정된 클래스에 속한 스키마만 포함하는 필터링된 스키마 목록을 반환합니다. 여러 쿼리 매개 변수를 사용할 때는 AND 관계가 가정됩니다.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
