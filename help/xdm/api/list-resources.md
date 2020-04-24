---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 리소스 목록
topic: developer guide
translation-type: tm+mt
source-git-commit: 58549241f05f1bd604f33762f681c60946fa52f5

---


# 리소스 목록

단일 GET 요청을 수행하여 컨테이너 내에 특정 유형(클래스, 믹싱, 스키마, 데이터 유형 또는 설명자)의 모든 스키마 레지스트리 리소스 목록을 볼 수 있습니다.

>[!NOTE] 리소스를 나열할 때 스키마 레지스트리는 결과 집합을 300개 항목으로 제한합니다. 이 제한을 초과하는 리소스를 반환하려면 [페이징 매개 변수를](#paging)사용해야 합니다. 쿼리 매개 변수를 사용하여 결과를 [필터링하고 반환된 리소스](#filtering) 수를 줄이는 것도 좋습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 리소스가 있는 컨테이너(&quot;전역&quot; 또는 &quot;테넌트&quot;). |
| `{RESOURCE_TYPE}` | 스키마 라이브러리에서 검색할 리소스 유형입니다. 유효한 유형은 `classes`, `mixins`, `schemas``datatypes`및 `descriptors`입니다. |
| `{QUERY_PARAMS`} | 결과를 필터링하는 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수에](#query) 대한 섹션을 참조하십시오. |

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답 형식은 요청에서 전송된 수락 헤더에 따라 달라집니다. 리소스를 나열하는 경우 다음 승인 헤더를 사용할 수 있습니다.

| 헤더 수락 | 설명 |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | 각 리소스에 대한 간단한 요약을 반환합니다. 리소스를 나열하는 데 권장되는 헤더입니다. (제한:300) |
| application/vnd.adobe.xed+json | 원본 및 `$ref` `allOf` 포함된 각 리소스에 대한 전체 JSON 스키마를 반환합니다. (제한:300) |
| application/vnd.adobe.xdm-v2+json | 끝점을 사용할 때 `/descriptors` 페이징 기능을 활용하려면 이 승인 헤더를 사용해야 합니다. |

**응답**

위의 요청에는 수락 `application/vnd.adobe.xed-id+json` 헤더가 사용되므로 응답에는 각 리소스의 `title`, `$id``meta:altId`및 `version` 속성만 포함됩니다. 수락 `full` 헤더로 대체하면 각 리소스의 모든 속성이 반환됩니다. 응답에 필요한 정보에 따라 적절한 수락 헤더를 선택합니다.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## 쿼리 매개 변수 사용 {#query}

스키마 레지스트리는 리소스를 나열할 때 쿼리 매개 변수를 페이지에 사용하고 결과를 필터링할 수 있도록 지원합니다.

>[!NOTE] 여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(`&`)로 구분해야 합니다.

### 페이징 {#paging}

페이징 시 가장 일반적인 쿼리 매개 변수는 다음과 같습니다.

| 매개 변수 | 설명 |
| --- | --- |
| `start` | 나열된 결과를 기록할 위치를 지정합니다. 예:다음으로 반환된 세 번째 항목의 결과를 `start=2` 나열합니다. |
| `limit` | 반환된 리소스 수를 제한합니다. 예:5개의 리소스 목록을 `limit=5` 반환합니다. |
| `orderby` | 특정 속성별로 결과를 정렬합니다. 예:제목별로 결과를 오름차순(A-Z)으로 `orderby=title` 정렬합니다. 제목 `-` 앞에 추가(`orderby=-title`)를 추가하면 항목들이 내림차순(Z-A)으로 정렬됩니다. |

### 필터링 {#filtering}

검색된 리소스 내의 지정된 JSON 속성에 대해 특정 연산자를 적용하는 데 사용되는 `property` 매개 변수를 사용하여 결과를 필터링할 수 있습니다. 지원되는 연산자는 다음과 같습니다.

| 연산자 | 설명 | 예 |
| --- | --- | --- |
| `==` | 속성이 제공된 값과 같은지 여부를 기준으로 필터링합니다. | `property=title==test` |
| `!=` | 속성이 제공된 값과 동일하지 않은지 여부를 기준으로 필터링합니다. | `property=title!=test` |
| `<` | 속성이 제공된 값보다 작은지 여부에 따라 필터링합니다. | `property=version<5` |
| `>` | 속성이 제공된 값보다 큰지 여부를 기준으로 필터링합니다. | `property=version>5` |
| `<=` | 속성이 제공된 값보다 작거나 같은지 여부를 기준으로 필터링합니다. | `property=version<=5` |
| `>=` | 속성이 제공된 값보다 크거나 같은지 여부를 기준으로 필터링합니다. | `property=version>=5` |
| `~` | 속성이 제공된 정규 표현식과 일치하는지 여부를 기준으로 필터링합니다. | `property=title~test$` |
| (없음) | 속성 이름만 지정하면 속성이 있는 항목만 반환됩니다. | `property=title` |

>[!TIP] 이 `property` 매개 변수를 사용하여 호환되는 클래스로 믹스를 필터링할 수 있습니다. 예를 들어 `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` XDM 개별 프로필 클래스와 호환되는 혼합만 반환합니다.
