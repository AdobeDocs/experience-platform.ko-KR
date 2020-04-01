---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 조합
topic: developer guide
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# 조합

조합(또는 공용 뷰)은 동일한 클래스(XDM ExperienceEvent 또는 XDM 개별 프로필)를 공유하고 실시간 고객 프로필에 대해 활성화된 모든 스키마의 필드를 집계하는 시스템 생성, 읽기 전용 [스키마입니다](../../profile/home.md).

이 문서에서는 다양한 작업에 대한 샘플 호출을 비롯하여 스키마 레지스트리 API에서 조합 작업에 필요한 기본 개념을 다룹니다. XDM의 조합에 대한 일반적인 자세한 내용은 스키마 구성의 [기본 사항에](../schema/composition.md#union)있는 조합에 대한 섹션을 참조하십시오.

## 유니온 믹스

스키마 레지스트리에는 조합 스키마 내에 다음 세 가지 혼합이 자동으로 포함됩니다. `identityMap`및 `timeSeriesEvents`를 `segmentMembership`참조하십시오.

### ID 맵

조합 스키마는 `identityMap` 조합의 관련 레코드 스키마 내에서 알려진 ID를 나타냅니다. ID 맵은 네임스페이스로 키잉된 다른 배열로 ID를 구분합니다. 나열된 각 ID는 고유한 `id` 값을 포함하는 객체입니다.

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### 시계열 이벤트

이 `timeSeriesEvents` 배열은 결합과 연관된 레코드 스키마와 관련된 시계열 이벤트 목록입니다. 프로필 데이터를 데이터 세트로 내보낼 때 이 배열은 각 레코드에 대해 포함됩니다. 이 기능은 레코드 특성 외에 프로필의 전체 동작 내역이 필요한 기계 학습과 같은 다양한 사용 사례에 유용합니다.

### 세그먼트 멤버십 맵

맵은 `segmentMembership` 세그먼트 평가 결과를 저장합니다. 세그먼트 작업이 세그멘테이션 API를 사용하여 성공적으로 [실행되면](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)맵이 업데이트됩니다. `segmentMembership` 또한 Adobe Audience Manager와 같은 다른 솔루션과의 통합을 위해 인제스트된 사전 평가 대상 세그먼트를 플랫폼에 저장합니다.

자세한 내용은 API를 사용하여 세그먼트를 [만드는](../../segmentation/tutorials/create-a-segment.md) 방법에 대한 자습서를 참조하십시오.

## 조합 멤버십에 대한 스키마 활성화

병합된 조합 보기에 스키마를 포함하려면 &quot;union&quot; 태그를 스키마의 `meta:immutableTags` 속성에 추가해야 합니다. 이 작업은 PATCH 요청을 통해 스키마를 업데이트하고 값이 &quot;union&quot;인 `meta:immutableTags` 배열을 추가합니다.

>[!NOTE] 변경할 수 없는 태그는 설정하되 제거되지 않는 태그입니다.

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 프로필에서 사용할 수 있도록 `$id` 활성화할 URL 인코딩 URI 또는 `meta:altId` 스키마의 URL 인코딩 URI입니다. |

**요청**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**응답**

성공적인 응답은 업데이트된 스키마의 세부 사항을 반환하며, 여기에는 문자열 값 &quot;union&quot;이 포함된 `meta:immutableTags` 배열이 포함됩니다.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 목록 조합

스키마에서 &quot;union&quot; 태그를 설정하면 스키마 레지스트리가 스키마를 기반으로 하는 클래스에 대한 결합을 자동으로 생성하고 유지 관리합니다. 조합의 `$id` 은 클래스의 표준과 비슷하며, 단 두 개의 밑줄이 추가되고 &quot;union&quot;( `$id``"__union"`)이라는 단어가 추가되는 유일한 차이입니다.

사용 가능한 조합 목록을 보려면 종단점에 대한 GET 요청을 수행할 수 `/unions` 있습니다.

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

**응답**

성공적인 응답은 HTTP 상태 200(OK 파섹) 및 응답 본문에 `results` 배열을 반환합니다. 조합이 정의된 경우 `title`, `$id`, `meta:altId``version` ,및 각 조합에 대해 배열 내의 개체로 제공됩니다. 조합이 정의되지 않은 경우 HTTP 상태 200(OK)이 여전히 반환되지만 `results` 배열은 비어 있게 됩니다.

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

## 특정 조합 검색

Accept 헤더에 따라 `$id` 및 조합의 일부 또는 전체 세부 사항을 포함하는 GET 요청을 수행하여 특정 결합을 볼 수 있습니다.

>[!NOTE] 조합 조회는 `/unions` 및 `/schemas` 끝점을 사용하여 프로필 내보내기에서 데이터 세트로 사용할 수 있도록 합니다.

**API 형식**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{UNION_ID}` | 조회할 `$id` 조합의 URL 인코딩 URI. 공용 스키마의 URI는 &quot;__union&quot;과 함께 추가됩니다. |

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

조합 조회 요청은 승인 헤더에 포함되어야 `version` 합니다.

공용 스키마 조회에 대해 다음 승인 헤더를 사용할 수 있습니다.

| 수락 | 설명 |
| -------|------------ |
| application/vnd.adobe.xed+json;version={MAJOR_VERSION} | Raw with `$ref` and `allOf`. 제목 및 설명이 포함되어 있습니다. |
| application/vnd.adobe.xed-full+json;version={MAJOR_VERSION} | `$ref` 속성을 확인하고 `allOf` 해결했습니다. 제목 및 설명이 포함되어 있습니다. |

**응답**

성공적인 응답은 요청 경로에서 제공된 클래스를 구현하는 모든 스키마의 결합 보기를 `$id` 반환합니다.

응답 형식은 요청에서 전송된 수락 헤더에 따라 달라집니다. 다른 승인 헤더로 여러 가지 테스트를 통해 응답을 비교하고 사용 사례에 가장 적합한 헤더를 결정할 수 있습니다.

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

## 공용 구조체의 스키마 목록

특정 조합의 일부인 스키마를 확인하려면 쿼리 매개 변수를 사용하여 테넌트 컨테이너 내의 스키마를 필터링할 수 있습니다.

쿼리 매개 `property` 변수를 사용하여 `meta:immutableTags` 필드를 포함하는 반환 스키마만, 액세스하려는 조합이 있는 클래스와 `meta:class` 동일한 반환 스키마에 대한 응답을 구성할 수 있습니다.

**API 형식**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 액세스하려는 `$id` 조합의 클래스 |

**요청**

다음 요청은 XDM 개별 프로필 클래스 조합의 일부인 모든 스키마를 조회합니다.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 두 요구 사항을 모두 충족하는 스키마만 포함하는 필터링된 스키마 목록을 반환합니다. 여러 쿼리 매개 변수를 사용하는 경우 AND 관계가 가정됩니다. 응답 형식은 요청에서 전송된 수락 헤더에 따라 달라집니다.

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
