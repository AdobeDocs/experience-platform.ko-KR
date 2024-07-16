---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;유니온;유니온;유니온;유니온;유니온;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: 유니온 API 엔드포인트
description: 스키마 레지스트리 API의 /union 끝점을 사용하면 경험 애플리케이션에서 XDM 유니온 스키마를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 3da2e8f66f08a7bb9533795f7854ad583734911c
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 1%

---

# 유니온 엔드포인트

유니온(또는 유니온 보기)은 동일한 클래스([!DNL XDM ExperienceEvent] 또는 [!DNL XDM Individual Profile])를 공유하고 [[!DNL Real-Time Customer Profile]](../../profile/home.md)에 대해 활성화된 모든 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다.

이 문서에서는 다양한 작업에 대한 샘플 호출을 포함하여 스키마 레지스트리 API에서 유니온을 사용하여 작업하기 위한 필수 개념을 다룹니다. XDM의 유니온에 대한 자세한 내용은 [스키마 컴포지션의 기본 사항](../schema/composition.md#union)에서 유니온에 대한 섹션을 참조하십시오.

## 유니온 스키마 필드

[!DNL Schema Registry]은(는) 유니온 스키마 내에 세 개의 키 필드를 자동으로 포함합니다. `identityMap`, `timeSeriesEvents` 및 `segmentMembership`.

### ID 맵

유니온 스키마의 `identityMap`은(는) 유니온의 연결된 레코드 스키마 내의 알려진 ID를 나타냅니다. ID 맵은 ID를 네임스페이스로 처리된 다른 배열로 구분합니다. 나열된 각 ID는 그 자체로 고유한 `id` 값을 포함하는 개체입니다. 자세한 내용은 [ID 서비스 설명서](../../identity-service/home.md)를 참조하세요.

### 시계열 이벤트

`timeSeriesEvents` 배열은 유니온과 연결된 레코드 스키마와 관련된 시계열 이벤트 목록입니다. 프로필 데이터를 데이터 세트로 내보내면 이 배열이 각 레코드에 포함됩니다. 이 기능은 모델이 레코드 특성 외에 프로필의 전체 동작 기록이 필요한 머신 러닝과 같은 다양한 사용 사례에 유용합니다.

### 세그먼트 멤버십 맵

`segmentMembership` 맵은 세그먼트 정의를 평가한 결과를 저장합니다. [세그먼테이션 API](https://www.adobe.io/experience-platform-apis/references/segmentation/)를 사용하여 세그먼트 작업이 성공적으로 실행되면 맵이 업데이트됩니다. `segmentMembership`은(는) Platform에 수집되는 미리 평가된 대상도 모두 저장하여 Adobe Audience Manager과 같은 다른 솔루션과 통합할 수 있습니다. 자세한 내용은 [API를 사용하여 대상자 만들기](../../segmentation/tutorials/create-a-segment.md)에 대한 자습서를 참조하십시오.

## 유니온 목록 검색 {#list}

스키마에 `union` 태그를 설정하면 [!DNL Schema Registry]이(가) 스키마를 기반으로 하는 클래스의 유니온에 스키마를 자동으로 추가합니다. 해당 클래스에 대한 유니온이 없는 경우 새 유니온이 자동으로 생성됩니다. 유니온에 대한 `$id`은(는) 다른 [!DNL Schema Registry] 리소스의 표준 `$id`과(와) 유사하지만 두 개의 밑줄 및 &quot;유니온&quot;(`__union`)이라는 단어가 추가된 차이점만 있습니다.

`/tenant/unions` 끝점에 대한 GET 요청을 수행하면 사용 가능한 유니온 목록을 볼 수 있습니다.

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

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 유니온 목록을 만드는 데 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 만드는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본 `$ref` 및 `allOf`이(가) 포함된 각 리소스에 대한 전체 JSON 클래스를 반환합니다. (제한: 300) |

{style="table-layout:auto"}

**응답**

응답이 성공하면 응답 본문에 HTTP 상태 200(OK) 및 `results` 배열이 반환됩니다. 유니온이 정의된 경우 각 유니온에 대한 세부 사항이 배열 내의 객체로 제공됩니다. 유니온이 정의되지 않은 경우 HTTP 상태 200(OK)이 계속 반환되지만 `results` 배열이 비어 있습니다.

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

## 유니온 조회 {#lookup}

`$id`을(를) 포함하는 GET 요청을 수행하고 Accept 헤더에 따라 특정 유니온 세부 정보의 일부 또는 전부를 볼 수 있습니다.

>[!NOTE]
>
>유니온 조회는 `/unions` 및 `/schemas` 끝점을 사용하여 [!DNL Profile] 내보내기에서 데이터 집합으로 사용할 수 있도록 설정할 수 있습니다.

**API 형식**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{UNION_ID}` | 조회할 유니온의 URL 인코딩 `$id` URI입니다. 유니온 스키마의 URI에 &quot;union__이 추가됩니다. |

{style="table-layout:auto"}

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

유니온 조회 요청에는 Accept 헤더에 `version`이(가) 포함되어야 합니다.

유니온 스키마 조회에 다음 Accept 헤더를 사용할 수 있습니다.

| 수락 | 설명 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | `$ref` 및 `allOf`(으)로 원시 제목 및 설명을 포함합니다. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref`개 특성 및 `allOf`개 확인됨. 제목 및 설명을 포함합니다. |

{style="table-layout:auto"}

**응답**

응답이 성공하면 요청 경로에 `$id`이(가) 제공된 클래스를 구현하는 모든 스키마의 유니온 보기가 반환됩니다.

응답 형식은 요청에서 전송된 Accept 헤더에 따라 다릅니다. 다른 Accept 헤더로 테스트하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 결정합니다.

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

## 유니온 멤버십에 대한 스키마 활성화 {#enable}

스키마가 해당 클래스의 유니온에 포함되려면 스키마의 `meta:immutableTags` 특성에 `union` 태그를 추가해야 합니다. 단일 문자열 값이 `union`인 `meta:immutableTags` 배열을 해당 스키마에 추가하도록 PATCH 요청을 수행하면 됩니다. 자세한 예제는 [스키마 끝점 안내서](./schemas.md#union)를 참조하십시오.

## 유니온에 스키마 나열 {#list-schemas}

특정 유니온에 속하는 스키마를 확인하기 위해 `/tenant/schemas` 끝점에 대한 GET 요청을 수행할 수 있습니다. `property` 쿼리 매개 변수를 사용하여 `meta:immutableTags` 필드가 포함된 스키마만 반환하도록 응답을 구성할 수 있으며, `meta:class`은(는) 액세스하는 공용 구조체 클래스와 동일합니다.

**API 형식**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{CLASS_ID}` | 유니온 사용 스키마를 나열할 클래스의 `$id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 [!DNL XDM Individual Profile] 클래스에 대한 유니온의 일부인 모든 스키마 목록을 검색합니다.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. 스키마를 나열하는 데 다음 `Accept` 헤더를 사용할 수 있습니다.

| `Accept` 헤더 | 설명 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스 목록을 만드는 데 권장되는 헤더입니다. (제한: 300) |
| `application/vnd.adobe.xed+json` | 원본 `$ref` 및 `allOf`이(가) 포함된 각 리소스에 대해 전체 JSON 스키마를 반환합니다. (제한: 300) |

{style="table-layout:auto"}

**응답**

성공한 응답은 유니온 멤버십에 대해 활성화된 지정된 클래스에 속하는 스키마만 포함하는 필터링된 스키마 목록을 반환합니다. 여러 쿼리 매개 변수를 사용할 때는 AND 관계가 가정된다는 점을 기억하십시오.

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
