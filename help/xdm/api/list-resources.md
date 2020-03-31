---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 리소스 목록
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# 리소스 목록

단일 GET 요청을 수행하여 컨테이너 내의 모든 리소스(스키마, 클래스, 믹싱 또는 데이터 유형) 목록을 볼 수 있습니다. 결과 필터링을 돕기 위해 스키마 레지스트리는 리소스를 나열할 때 쿼리 매개 변수 사용을 지원합니다.

가장 일반적인 쿼리 매개 변수는 다음과 같습니다.

* `limit` - 반환된 리소스 수를 제한합니다. 예:5개의 리소스 목록을 `limit=5` 반환합니다.
* `orderby` - 특정 속성별로 결과를 정렬합니다. 예:제목별로 결과를 오름차순(A-Z)으로 `orderby=title` 정렬합니다. 제목 `-` 앞에 추가(`orderby=-title`)를 추가하면 항목들이 내림차순(Z-A)으로 정렬됩니다.
* `property` - 모든 최상위 속성에 대한 결과를 필터링합니다. 예를 들어 `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` XDM 개별 프로필 클래스와 호환되는 혼합만 반환합니다.

여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(`&`)로 구분해야 합니다.

**API 형식**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 리소스가 있는 컨테이너(&quot;전역&quot; 또는 &quot;테넌트&quot;). |
| `{RESOURCE_TYPE}` | 스키마 라이브러리에서 검색할 리소스 유형입니다. 유효한 유형은 `datatypes`, `mixins`, `schemas`및 `classes`입니다. |

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
| application/vnd.adobe.xed-id+json | 각 리소스의 간단한 요약(일반적으로 나열할 때 선호하는 헤더)을 반환합니다. |
| application/vnd.adobe.xed+json | 원본 및 `$ref` `allOf` 포함된 각 리소스에 대한 전체 JSON 스키마를 반환합니다. |

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
