---
title: 스키마 레지스트리 API를 사용하여 스키마에 특정 필드 추가
description: 스키마 레지스트리 API를 사용하여 기존 필드 그룹의 개별 필드를 Experience Data Model(XDM) 스키마에 추가하는 방법을 알아봅니다.
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# 스키마 레지스트리 API를 사용하여 스키마에 특정 필드 추가

XDM(Experience Data Model) 스키마는 기본 클래스로 구성되며 Adobe에 의해 정의된 표준 필드 그룹과 조직에 의해 정의된 사용자 지정 필드 그룹을 사용하여 포함된 추가 필드가 있습니다.

스키마를 작성할 때, 필요하지 않은 동일한 그룹의 필드를 제외하면서 주어진 필드 그룹의 일부 필드를 사용할 수 있습니다. 이 자습서에서는 스키마 레지스트리 API를 사용하여 필드 그룹의 개별 필드를 스키마에 추가하는 방법을 보여줍니다.

>[!NOTE]
>
>Adobe Experience Platform UI에서 개별 스키마 필드를 추가 및 제거하는 방법에 대한 자세한 내용은 [필드 기반 워크플로](../ui/field-based-workflows.md) (현재 베타 버전).

## 사전 요구 사항

이 튜토리얼에는 [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 시작하기 전에 다음을 검토하십시오 [개발자 안내서](../api/getting-started.md) 를 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보 `{TENANT_ID}`, 컨테이너의 개념 및 요청을 하는 데 필요한 헤더입니다.

## 이해 `meta:refProperty` 필드

주어진 스키마의 경우 해당 구조를 구성하는 클래스 및 필드 그룹이 스키마 아래에서 참조됩니다 `allOf` 배열입니다. 각 구성 요소는 `$ref` 구성 요소의 URI를 참조하는 속성 `$id`.

다음 JSON은 단일 클래스(`experienceevent`) 및 필드 그룹(`experienceevent-all`):

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

의 모든 객체에 대해 `allOf` 필드 그룹을 참조하는 배열에서 형제 그룹을 추가할 수 있습니다. `meta:refProperty` 스키마에 포함할 그룹의 필드를 지정하는 필드입니다.

>[!NOTE]
>
>각 필드는 해당 필드 그룹 내의 필드 경로를 나타내는 JSON 포인터 문자열을 사용하여 지정됩니다. 문자열은 앞에 슬래시(`/`) 및 포함하지 않아야 합니다 `properties` 네임스페이스입니다. 예: `/_experience/campaign/message/id`.

문자열로 포함될 때, `meta:refProperty` 는 그룹의 단일 필드를 참조할 수 있습니다. 동일한 그룹의 다른 필드는 동일한 필드를 사용하여 포함할 수 있습니다 `$ref` 다른 값이 있는 다른 개체의 값 `meta:refProperty` 값.

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

또는 `meta:refProperty` 배열로 제공할 수 있으므로 단일 내에서 주어진 그룹에서 포함할 여러 필드를 지정할 수 있습니다 `allOf` 목록 항목:

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## PUT 작업을 사용하여 필드 추가

PUT 요청을 사용하여 전체 스키마를 재작성하고 아래에 포함할 필드를 구성할 수 있습니다 `allOf`.

**API 형식**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 다시 작성할 스키마의 수입니다. |

**요청**

다음 요청은 아래의 필드 그룹에 포함된 특정 필드를 업데이트합니다. `allOf` 배열입니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**응답**

성공한 응답은 업데이트된 스키마의 세부 정보를 반환합니다.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>스키마의 PUT 요청에 대한 자세한 내용은 [스키마 엔드포인트 안내서](../api/schemas.md#put).

## PATCH 작업을 사용하여 필드 추가

PATCH 요청을 사용하여 다른 필드를 덮어쓰지 않고 스키마에 개별 필드를 추가할 수 있습니다. 스키마 레지스트리는 다음을 포함한 모든 표준 JSON 패치 작업을 지원합니다. `add`, `remove`, 및 `replace`. JSON 패치에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch).

**API 형식**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SCHEMA_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 다시 작성할 스키마의 수입니다. |

**요청**

다음 요청은 스키마에 새 개체를 추가합니다 `allOf` 배열, 추가할 필드를 지정합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**응답**

성공한 응답은 업데이트된 스키마의 세부 정보를 반환합니다.

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>스키마의 PATCH 요청에 대한 자세한 내용은 [스키마 엔드포인트 안내서](../api/schemas.md#patch).

## 다음 단계

이 안내서에서는 API 호출을 사용하여 기존 필드 그룹의 개별 필드를 스키마에 추가하는 방법을 다룹니다. Platform UI에서 유사한 필드 기반 작업을 수행하는 방법에 대한 자세한 내용은 [필드 기반 워크플로](../ui/field-based-workflows.md).

스키마 레지스트리 API의 기능에 대한 자세한 내용은 [API 개요](../api/overview.md) 엔드포인트 및 프로세스의 전체 목록
