---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;비헤이비어;비헤이비어;비헤이비어;
solution: Experience Platform
title: 동작 API 끝점
description: 스키마 레지스트리 API의 /behaviors 끝점을 사용하면 전역 컨테이너에서 사용 가능한 모든 동작을 검색할 수 있습니다.
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# 비헤이비어 끝점

XDM(Experience Data Model)에서 동작은 스키마가 설명하는 데이터의 특성을 정의합니다. 각 XDM 클래스는 특정 동작을 참조해야 하며, 이 경우 해당 클래스를 사용하는 모든 스키마는 이 동작을 상속합니다. 플랫폼의 거의 모든 사용 사례에는 두 가지 동작이 있습니다.

* **[!UICONTROL 기록]**: 제목의 속성에 대한 정보를 제공합니다. 주제는 조직 또는 개인일 수 있습니다.
* **[!UICONTROL 시계열]**: 레코드 주체가 직접 또는 간접적으로 작업을 수행한 시간에 시스템의 스냅샷을 제공합니다.

>[!NOTE]
>
>위의 동작 중 하나를 사용하지 않는 스키마를 사용해야 하는 Platform의 일부 사용 사례가 있습니다. 이러한 경우 세 번째 &quot;임시&quot; 동작을 사용할 수 있습니다. 다음 튜토리얼 참조: [임시 스키마 생성](../tutorials/ad-hoc.md) 추가 정보.
>
>스키마 구성에 영향을 미치는 측면에서 데이터 동작에 대한 자세한 내용은 [스키마 컴포지션 기본 사항](../schema/composition.md).

다음 `/behaviors` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 의 사용 가능한 동작을 볼 수 있습니다. `global` 컨테이너.

## 시작하기

이 안내서에 사용된 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 비헤이비어 목록 검색 {#list}

에 GET 요청을 하여 사용 가능한 모든 동작 목록을 검색할 수 있습니다. `/behaviors` 엔드포인트.

**API 형식**

```http
GET /global/behaviors
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**응답**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## 동작 조회 {#lookup}

에 대한 GET 요청 경로에 해당 ID를 제공하여 특정 동작을 조회할 수 있습니다. `/behaviors` 엔드포인트.

**API 형식**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{BEHAVIOR_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 조회하려는 비헤이비어 중 하나. |

{style="table-layout:auto"}

**요청**

다음 요청은 를 제공하여 레코드 동작의 세부 정보를 검색합니다. `meta:altId` 요청 경로에서.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**응답**

성공적인 응답은 버전, 설명 및 동작이 해당 동작을 사용하는 클래스에 제공하는 속성을 포함한 동작의 세부 정보를 반환합니다.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## 다음 단계

이 안내서에서는 의 사용을 다룹니다. `/behaviors` 의 엔드포인트 [!DNL Schema Registry] API. API를 사용하여 클래스에 동작을 할당하는 방법을 알아보려면 다음을 참조하십시오. [클래스 끝점 안내서](./classes.md).
