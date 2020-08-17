---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type;datatype;Datatype
solution: Experience Platform
title: 데이터 유형 만들기
topic: developer guide
description: '조직에서 여러 방법으로 사용하려는 일반적인 데이터 구조가 있는 경우 데이터 유형을 정의할 수 있습니다. 데이터 유형은 필드의 ''유형''으로 추가하여 스키마에서 어느 곳에나 포함할 수 있으므로 혼합보다 유연하면서 다중 필드 구조를 일관되게 사용할 수 있습니다. '
translation-type: tm+mt
source-git-commit: cc81d590f308c7e2677cec000c27e8aca42437f5
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 데이터 유형 만들기

조직에서 여러 방법으로 사용하려는 일반적인 데이터 구조가 있는 경우 데이터 유형을 정의할 수 있습니다. 데이터 유형은 필드의 일부로 추가하여 스키마에서 어디에나 포함할 수 있으므로 혼합보다 유연하면서 다중 필드 구조를 일관되게 사용할 수 `type` 있습니다.

즉, 데이터 유형을 사용하면 객체 계층을 한 번 정의할 수 있으며 다른 스칼라 유형과 동일한 방식으로 필드에서 참조할 수 있습니다.

**API 형식**

```http
POST /tenant/datatypes
```

**요청**

데이터 형식을 정의해도 `meta:extends` 또는 필드가 필요하지 않으며, 충돌을 방지하기 위해 필드를 중첩할 필요가 `meta:intendedToExtend` 없습니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the property construction",
        "type":"object",
        "properties": {
          "yearBuilt": {
            "type":"integer",
            "title": "Year Built",
            "description": "The year the property was constructed."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "freeStanding",
              "mall",
              "shoppingCenter"
            ],
            "meta:enum": {
              "freeStanding": "Free Standing Building",
              "mall": "Mall Space",
              "shoppingCentre": "Shopping Center"
            }
          }
        } 
      }'
```

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과 새로 만든 데이터 유형(예: `$id`, `meta:altId`및 `version`포함)의 세부 사항을 포함하는 페이로드를 반환합니다. 이 세 개의 값은 읽기 전용이며 [!DNL Schema Registry]

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the property construction",
    "type": "object",
    "properties": {
        "yearBuilt": {
            "type": "integer",
            "title": "Year Built",
            "description": "The year the property was constructed.",
            "meta:xdmType": "int"
        },
        "constructionType": {
            "type": "string",
            "title": "Construction Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "freeStanding",
                "mall",
                "shoppingCenter"
            ],
            "meta:enum": {
                "freeStanding": "Free Standing Building",
                "mall": "Mall Space",
                "shoppingCentre": "Shopping Center"
            },
            "meta:xdmType": "string"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.0",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552087079285,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

테넌트 컨테이너에 모든 데이터 유형을 나열하기 위한 GET 요청을 수행하면 속성 구성 데이터 유형이 포함됩니다. 또한 URL 인코딩 URI를 사용하여 조회(GET) 요청을 수행하여 새 데이터 유형을 직접 볼 수도 `$id` 있습니다. 조회 요청에 대한 수락 헤더 `version` 에 해당 항목을 포함해야 합니다.
