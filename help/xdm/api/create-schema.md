---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스키마 만들기
topic: developer guide
translation-type: tm+mt
source-git-commit: 162316c3b908ffa87d8df4dff72e26ba237993db

---


# 스키마 만들기

스키마는 Experience Platform에 인제스트하려는 데이터의 청사진이라고 생각할 수 있습니다. 각 스키마는 클래스와 0개 이상의 혼합으로 구성됩니다. 즉, 스키마를 정의하기 위해 혼합을 추가할 필요는 없지만 대부분의 경우 혼합을 하나 이상 사용합니다.

스키마 구성 프로세스는 클래스를 할당하여 시작됩니다. 이 클래스는 데이터(레코드 또는 시간 시리즈)의 주요 행동 측면과 인제스트할 데이터를 설명하는 데 필요한 최소 필드를 정의합니다.

**API 형식**

```http
POST /tenant/schemas
```

**요청**

요청에는 클래스의 속성을 참조하는 `allOf` 특성이 포함되어야 `$id` 합니다. 이 속성은 스키마가 구현할 &quot;기본 클래스&quot;를 정의합니다. 이 예제에서 기본 클래스는 이전에 만든 &quot;속성 정보&quot; 클래스입니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `allOf > $ref` | 새 스키마가 구현할 클래스의 `$id` 값입니다. |

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과 새로 만든 스키마( `$id`, `meta:altId`및 `version`포함)의 세부 정보가 포함된 페이로드를 반환합니다. 이러한 값은 읽기 전용이며 스키마 레지스트리에 지정됩니다.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

테넌트 컨테이너의 모든 스키마를 나열하기 위한 GET 요청을 수행하면 이제 속성 정보 스키마가 포함되거나, URL 인코딩 URI를 사용하여 조회(GET) 요청을 수행하여 새 스키마를 직접 볼 수 `$id` 있습니다. 모든 조회 요청에 대해 수락 `version` 헤더에 를 포함해야 합니다.
