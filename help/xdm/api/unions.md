---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: 노조
description: 스키마 레지스트리 API의 /union 끝점을 사용하면 경험 응용 프로그램에서 XDM 결합 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 1%

---


# 조합 끝점

조합(또는 조합 뷰)은 동일한 클래스(또는)를 공유하고 사용할 수 있는 모든 스키마의 필드를 집계하는 시스템 생성,[!DNL XDM ExperienceEvent] 읽기 전용 스키마입니다 [!DNL XDM Individual Profile][[!DNL Real-time Customer Profile]](../../profile/home.md).

이 문서에서는 스키마 레지스트리 API에서 조합과 함께 작업하는 데 필요한 개념과 다양한 작업에 대한 샘플 호출을 다룹니다. XDM의 조합에 대한 일반적인 자세한 내용은 스키마 구성 [의 기본 사항에 있는 조합의 섹션을 참조하십시오](../schema/composition.md#union).

## 결합 스키마 필드

조합 스키마 내에 세 개의 키 필드가 자동으로 [!DNL Schema Registry] 포함됩니다. `identityMap`, `timeSeriesEvents`and `segmentMembership`.

### ID 맵

조합 스키마 `identityMap` 는 조합의 관련 레코드 스키마 내에서 알려진 ID를 나타냅니다. ID 맵은 네임스페이스로 키잉된 다른 배열로 ID를 구분합니다. 나열된 각 ID는 고유한 `id` 값을 포함하는 개체입니다. See the [Identity Service documentation](../../identity-service/home.md) for more information.

### 시계열 이벤트

이 `timeSeriesEvents` 배열은 조합과 연관된 레코드 스키마와 관련된 시계열 이벤트 목록입니다. 프로필 데이터를 데이터 세트로 내보낼 때 이 배열은 각 레코드에 포함됩니다. 이 기능은 모델에 레코드 특성 외에 프로파일의 전체 동작 내역이 필요한 기계 학습과 같은 다양한 사용 사례에 유용합니다.

### 세그먼트 멤버십 맵

맵에는 `segmentMembership` 세그먼트 평가의 결과가 저장됩니다. 세그먼트 작업이 세그멘테이션 [API를 사용하여 성공적으로](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)실행되면 지도가 업데이트됩니다. `segmentMembership` 또한 Platform으로 인제스트된 사전 평가 대상 세그먼트를 저장하여 Adobe Audience Manager과 같은 다른 솔루션과 통합할 수 있습니다. 자세한 내용은 API를 사용하여 세그먼트 [를](../../segmentation/tutorials/create-a-segment.md) 만드는 방법에 대한 자습서를 참조하십시오.

## 조합 목록 검색 {#list}

스키마에서 `union` 태그를 설정하면 스키마가 [!DNL Schema Registry] 기반이 되는 클래스에 대한 스키마에 스키마를 자동으로 추가합니다. 해당 클래스에 대한 조합이 없는 경우 새 조합이 자동으로 생성됩니다. 조합 `$id` 의 경우 다른 리소스 `$id` 의 표준과 유사하며 단 하나의 차이점이 두 개의 밑줄이 추가되고 &quot;union&quot;( [!DNL Schema Registry]`__union`)이라는 단어가 추가됩니다.

종단점에 GET 요청을 수행하여 사용 가능한 조합 목록을 볼 수 `/tenant/unions` 있습니다.

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

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다음 `Accept` 헤더는 조합을 나열하는 데 사용할 수 있습니다.

| `Accept` header | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원본 및 포함된 각 리소스에 대한 전체 JSON 클래스 `$ref` 를 `allOf` 반환합니다. (제한:300) |

**응답**

성공적인 응답은 HTTP 상태 200(OK) 및 응답 본문에 `results` 배열을 반환합니다. 조합이 정의된 경우 각 조합의 세부 정보가 배열 내의 개체로 제공됩니다. 정의된 조합이 없는 경우 HTTP 상태 200(OK)은 여전히 반환되지만 `results` 배열은 비어 있게 됩니다.

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

## 조합 찾기 {#lookup}

Accept 헤더에 따라 및 `$id` 를 포함하는 GET 요청을 수행하여 조합의 일부 또는 전체 세부 사항을 볼 수 있습니다.

>[!NOTE]
>
>조합 조회는 `/unions` 및 `/schemas` 종단점을 사용하여 데이터 세트로 [!DNL Profile] 내보내기 시 사용할 수 있습니다.

**API 형식**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{UNION_ID}` | 조회하려는 조합의 URL 인코딩 `$id` URI입니다. 결합 스키마에 대한 URI는 &quot;__union&quot;이 추가됩니다. |

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

조합 조회 요청은 수락 헤더에 `version` 포함되어야 합니다.

다음 승인 헤더를 조합 스키마 조회에 사용할 수 있습니다.

| 수락 | 설명 |
| -------|------------ |
| application/vnd.adobe.xed+json;version={MAJOR_VERSION} | Raw with `$ref` and `allOf`. 제목 및 설명을 포함합니다. |
| application/vnd.adobe.xed-full+json;version={MAJOR_VERSION} | `$ref` 속성 및 `allOf` 해결되었습니다. 제목 및 설명을 포함합니다. |

**응답**

성공적인 응답은 요청 경로에 제공된 클래스를 구현하는 모든 스키마의 조합 뷰 `$id` 를 반환합니다.

응답 형식은 요청에서 전송된 수락 헤더에 따라 다릅니다. 다양한 수락 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

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
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
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
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
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

## 조합 멤버십에 대한 스키마 사용 {#enable}

해당 클래스에 대한 조합에 스키마를 포함하려면 `union` 태그를 스키마의 `meta:immutableTags` 속성에 추가해야 합니다. 해당 스키마에 대해 단일 문자열 값이 있는 `meta:immutableTags` 배열을 추가하도록 PATCH 요청을 함으로써 이를 수행할 수 `union` 있습니다. 자세한 [예제는 스키마 끝점 안내서를](./schemas.md#union) 참조하십시오.

## 공용 구조체의 스키마 목록 {#list-schemas}

특정 조합의 일부인 스키마를 확인하려면 종단점에 대한 GET 요청을 수행할 수 `/tenant/schemas` 있습니다. 쿼리 매개 변수 `property` 를 사용하면 `meta:immutableTags` 필드가 포함된 스키마 및 액세스하 `meta:class` 는 조합이 있는 클래스와 동일한 스키마에 대한 응답만 구성할 수 있습니다.

**API 형식**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 나열하려는 조합 `$id` 이 활성화된 스키마를 소유한 클래스의 이름입니다. |

**요청**

다음 요청은 [!DNL XDM Individual Profile] 클래스에 대한 유니폼의 일부인 모든 스키마 목록을 검색합니다.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. 다음 헤더는 스키마를 나열할 수 `Accept` 있습니다.

| `Accept` header | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| `application/vnd.adobe.xed+json` | 원본 및 포함된 각 리소스에 대한 전체 JSON 스키마 `$ref` 를 `allOf` 반환합니다. (제한:300) |

**응답**

성공적인 응답은 조합 멤버십에 대해 활성화된 지정된 클래스에 속하는 스키마만 포함하는 필터링된 스키마 목록을 반환합니다. 여러 쿼리 매개 변수를 사용하는 경우 AND 관계가 가정됩니다.

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
