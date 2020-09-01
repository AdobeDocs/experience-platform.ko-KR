---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;lookup;Lookup;get;GET
solution: Experience Platform
title: 리소스 찾기
description: 요청 경로에서 리소스의 $id(URL 인코딩 URI)를 포함하는 GET 요청을 수행하여 스키마 레지스트리 API에서 특정 리소스를 찾을 수 있습니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---


# 리소스 찾기

요청 경로에서 리소스의 `$id` (URL 인코딩 URI)를 포함하는 GET 요청을 수행하여 특정 리소스를 찾을 수 있습니다.

**API 형식**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONTAINER_ID}` | 리소스가 있는 컨테이너(&quot;전역&quot; 또는 &quot;테넌트&quot;). |
| `{RESOURCE_TYPE}` | 에서 검색할 리소스 [!DNL Schema Library]유형입니다. 유효한 유형은 `datatypes`, `mixins``schemas`, `classes`및 입니다. |
| `{RESOURCE_ID}` | URL로 인코딩된 `$id` URI 또는 리소스 `meta:altId` 의 URL입니다. |

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/mixins/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile-person-details \
  -H 'Accept: application/vnd.adobe.xed+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

리소스 조회 요청은 승인 헤더에 `version` 포함되어야 합니다. 룩업에 다음과 같은 승인 헤더를 사용할 수 있습니다.

| 수락 | 설명 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw 및 `$ref` 와 `allOf`함께 사용할 수 있으며 제목 및 설명이 포함되어 있습니다. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 그리고 `allOf` 해결되었습니다. 제목 및 설명이 있습니다. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | 제목 또는 설명 `$ref` `allOf`이 없는 Raw |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 제목 또는 설명이 없는 문제를 `allOf` 해결했습니다. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 설명자가 포함된 `allOf` 문제를 해결했습니다. |

>[!NOTE]
>
>버전(1, 2, 3 등)만 제공하면 레지스트리는 최신 `major` `minor` 버전(.1, .2, .3 등)을 자동으로 반환합니다.

**응답**

성공적인 응답은 리소스의 세부 정보를 반환합니다. 반환되는 필드는 요청에 전송된 수락 헤더에 따라 다릅니다. 다양한 수락 헤더를 실험하여 응답을 비교하고 사용 사례에 가장 적합한 헤더를 확인합니다.

```JSON
{
    "$id": "https://ns.adobe.com/xdm/context/profile-person-details",
    "title": "Profile Person Details",
    "type": "object",
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Profile person details including naming, gender etc.",
    "definitions": {
        "profile-person-details": {
            "properties": {
                "person": {
                    "title": "Person",
                    "$ref": "https://ns.adobe.com/xdm/context/person",
                    "description": "An individual actor, contact, or owner.",
                    "meta:xdmField": "xdm:person"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
        },
        {
            "$ref": "#/definitions/profile-person-details"
        }
    ],
    "meta:xdmId": "https://ns.adobe.com/xdm/context/profile-person-details",
    "meta:altId": "_xdm.context.profile-person-details",
    "meta:xdmType": "object",
    "meta:status": "experimental",
    "version": "1",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:resourceType": "mixins",
    "meta:registryMetadata": {
        "repo:createDate": 1551745787442,
        "repo:lastModifiedDate": 1551745787442
    }
}
```
