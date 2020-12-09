---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;behavior;behaviour;behaviors;behaviours;
solution: Experience Platform
title: 동작 끝점 안내서
description: 스키마 레지스트리 API의 /behaviors 종단점을 사용하면 전역 컨테이너에서 사용 가능한 모든 동작을 검색할 수 있습니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 72c9147cefd00c9fe734ac64f8062c899b0588bc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---


# 동작 끝점

XDM(Experience Data Model)에서 비헤이비어는 스키마가 설명하는 데이터의 특성을 정의합니다. 각 XDM 클래스는 특정 동작을 참조해야 하며, 이 클래스를 사용하는 모든 스키마는 상속됩니다. Platform(플랫폼)에서 거의 모든 사용 사례에는 두 가지 사용 가능한 비헤이비어가 있습니다.

* **[!UICONTROL 기록]**:제목 속성에 대한 정보를 제공합니다. 대상은 조직 또는 개인일 수 있습니다.
* **[!UICONTROL 시계열]**:작업을 직접 또는 간접적으로 레코드 제목에 의해 수행한 시점에 시스템의 스냅샷을 제공합니다.

>[!NOTE]
>
>Platform에는 위의 비헤이비어 중 하나를 사용하지 않는 스키마를 사용해야 하는 일부 사용 사례가 있습니다. 이러한 경우 세 번째 &quot;임시&quot; 동작을 사용할 수 있습니다. 자세한 내용은 임시 스키마 [를 만드는](../tutorials/ad-hoc.md) 자습서를 참조하십시오.
>
>데이터 동작이 스키마 구성에 미치는 영향에 대한 일반적인 정보는 스키마 컴포지션의 [기본 사항에 대한 안내서를 참조하십시오](../schema/composition.md).

API의 `/behaviors` 종단점을 사용하면 [!DNL Schema Registry] 컨테이너에서 사용 가능한 동작을 볼 수 `global` 있습니다.

## 시작하기

이 안내서에서 사용되는 끝점은 [[!DNL Schema Registry] API의 일부입니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). 계속하기 전에 [시작하기 가이드](./getting-started.md) (관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서)와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 비헤이비어 목록 검색 {#list}

종단점에 GET 요청을 수행하여 사용 가능한 모든 비헤이비어 목록을 검색할 수 `/behaviors` 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 동작 검색 {#lookup}

종단점에 대한 GET 요청 경로에 해당 ID를 제공하여 특정 동작을 찾을 수 `/behaviors` 있습니다.

**API 형식**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BEHAVIOR_ID}` | 조회하려는 동작의 `meta:altId` 또는 URL 인코딩 `$id` 입니다. |

**요청**

다음 요청은 요청 경로에 레코드 동작의 세부 사항 `meta:altId` 을 제공하여 이를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**응답**

성공적인 응답은 해당 버전, 설명 및 비헤이비어가 해당 응답을 사용하는 클래스에 제공하는 특성을 포함하여 동작의 세부 사항을 반환합니다.

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

이 안내서에서는 API에서 종단점 `/behaviors` 사용을 [!DNL Schema Registry] 설명했습니다. API를 사용하여 클래스에 동작을 할당하는 방법을 알아보려면 [클래스 끝점 안내서를 참조하십시오](./classes.md).