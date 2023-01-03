---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;결합;결합;결합;세그먼트 멤버십;시간 시리즈 이벤트;
solution: Experience Platform
title: 결합 API 끝점
description: 스키마 레지스트리 API의 /union 종단점을 사용하면 경험 애플리케이션에서 XDM 결합 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# 결합 끝점

결합(또는 결합 보기)은 동일한 클래스([!DNL XDM ExperienceEvent] 또는 [!DNL XDM Individual Profile]) 및에 대해 활성화되어 있습니다. [[!DNL Real-Time Customer Profile]](../../profile/home.md).

이 문서에서는 다양한 작업에 대한 샘플 호출을 포함하여 스키마 레지스트리 API에서 결합 작업을 위한 필수 개념을 다룹니다. XDM의 조합에 대한 일반적인 자세한 내용은 [스키마 구성 기본 사항](../schema/composition.md#union).

## 결합 스키마 필드

다음 [!DNL Schema Registry] 는 자동으로 결합 스키마 내에 세 개의 키 필드를 포함합니다. `identityMap`, `timeSeriesEvents`, 및 `segmentMembership`.

### ID 맵

결합 스키마 `identityMap` 는 결합의 관련 레코드 스키마 내에 있는 알려진 ID를 나타냅니다. ID 맵은 ID를 네임스페이스로 사용하는 다른 배열로 구분합니다. 나열된 각 ID는 고유한 ID를 포함하는 객체 자체입니다 `id` 값. 자세한 내용은 [ID 서비스 설명서](../../identity-service/home.md) 추가 정보.

### 시계열 이벤트

다음 `timeSeriesEvents` 배열은 결합과 연관된 레코드 스키마와 관련된 시계열 이벤트 목록입니다. 프로필 데이터를 데이터 세트로 내보내면 이 배열이 각 레코드에 대해 포함됩니다. 이 기능은 모델이 레코드 특성 외에 프로필의 전체 동작 기록을 필요로 하는 기계 학습과 같은 다양한 사용 사례에 유용합니다.

### 세그먼트 멤버십 맵

다음 `segmentMembership` 맵은 세그먼트 평가 결과를 저장합니다. 세그먼트 작업을 [세그멘테이션 API](https://www.adobe.io/experience-platform-apis/references/segmentation/)를 입력하면 맵이 업데이트됩니다. `segmentMembership` 또한 Platform에 수집되는 사전 평가된 대상 세그먼트를 저장하여 Adobe Audience Manager과 같은 다른 솔루션과 통합할 수 있습니다. 다음에서 자습서를 참조하십시오. [api를 사용하여 세그먼트 만들기](../../segmentation/tutorials/create-a-segment.md) 추가 정보.

## 조합 목록 검색 {#list}

를 설정할 때 `union` 태그에 태그, [!DNL Schema Registry] 스키마를 기반으로 하는 클래스에 대한 조합에 스키마를 자동으로 추가합니다. 해당 클래스에 대한 조합이 없으면 새 조합이 자동으로 생성됩니다. 다음 `$id` 조합의 경우 표준과 유사합니다 `$id` 다른 [!DNL Schema Registry] 두 밑줄이 추가된 유일한 차이인 리소스 및 &quot;union&quot; 단어(`__union`).

GET 요청을 통해 사용 가능한 조합 목록을 볼 수 있습니다 `/tenant/unions` 엔드포인트.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

응답 형식은 `Accept` 헤더가 전송되었습니다. 다음 `Accept` 목록 조합에 사용할 수 있는 헤더는 다음과 같습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본과 함께 각 리소스에 대한 전체 JSON 클래스 반환 `$ref` 및 `allOf` 포함됩니다. (제한: 300) |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 HTTP 상태 200(OK) 및 `results` 배열에 있는 경우입니다. 결합이 정의된 경우 각 결합에 대한 세부 정보가 배열 내의 개체로 제공됩니다. 정의된 조합이 없는 경우 HTTP 상태 200(OK)이 반환되지만 `results` 배열이 비어 있습니다.

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

를 포함하는 GET 요청을 수행하여 특정 결합을 볼 수 있습니다 `$id` 및, Accept 헤더에 따라 조합의 일부 또는 모든 세부 사항이 달라집니다.

>[!NOTE]
>
>통합 조회는 `/unions` 및 `/schemas` 엔드포인트에서 사용할 수 있도록 설정 [!DNL Profile] 를 데이터 세트에 내보냅니다.

**API 형식**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{UNION_ID}` | URL로 인코딩되어 있습니다 `$id` 조회하려는 조합의 URI입니다. 결합 스키마에 대한 URI가 &quot;__union&quot;에 추가됩니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

결합 조회 요청에는 `version` Accept 헤더에 포함됩니다.

결합 스키마 조회에는 다음 Accept 헤더를 사용할 수 있습니다.

| Accept | 설명 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | 원시 `$ref` 및 `allOf`. 제목 및 설명을 포함합니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 속성 및 `allOf` 해결됨. 제목 및 설명을 포함합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 `$id` 이 요청 경로에 제공되었습니다.

응답 형식은 요청에서 전송된 Accept 헤더에 따라 다릅니다. 다른 Accept 헤더로 실험을 통해 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인해 보십시오.

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

## 결합 멤버십에 대한 스키마 활성화 {#enable}

스키마를 클래스에 대한 조합에 포함하려면 `union` 태그를 스키마 `meta:immutableTags` 속성을 사용합니다. PATCH 요청을 수행하여 다음을 추가할 수 있습니다 `meta:immutableTags` 단일 문자열 값이 인 배열 `union` 해당 스키마로 변경. 자세한 내용은 [스키마 끝점 안내서](./schemas.md#union) 자세한 예

## 결합 스키마 나열 {#list-schemas}

특정 결합에 속하는 스키마를 확인하려면 `/tenant/schemas` 엔드포인트. 사용 `property` 쿼리 매개 변수를 사용하면 `meta:immutableTags` 필드 및 `meta:class` 사용자가 액세스하는 공용 구조체의 클래스와 같습니다.

**API 형식**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 다음 `$id` 공용 구조체를 사용할 수 있는 스키마를 나열할 클래스 |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 공용 구조체에 대해 공용 구조체에 속하는 모든 스키마 목록을 검색합니다 [!DNL XDM Individual Profile] 클래스 이름을 지정합니다.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 `Accept` 헤더가 전송되었습니다. 다음 `Accept` 스키마를 나열할 때 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본과 함께 각 리소스에 대한 전체 JSON 스키마 반환 `$ref` 및 `allOf` 포함됩니다. (제한: 300) |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 조합 멤버십에 대해 활성화된 지정된 클래스에 속하는 스키마만 포함하는 필터링된 스키마 목록을 반환합니다. 여러 쿼리 매개 변수를 사용할 때는 AND 관계를 가정합니다.

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
