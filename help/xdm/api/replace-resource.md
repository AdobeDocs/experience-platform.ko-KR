---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 리소스 바꾸기
topic: developer guide
translation-type: tm+mt
source-git-commit: 67826f838951b3202a6a04321c28daa8ee883d20

---


# 리소스 바꾸기

스키마 레지스트리를 사용하면 PUT 작업을 통해 전체 리소스를 교체할 수 있습니다. 이 작업은 기본적으로 리소스를 다시 작성하므로 요청 본문에는 POST 요청을 사용하여 새 리소스를 만들 때 필요한 모든 필드가 포함되어야 합니다.

이 방법은 리소스의 많은 정보를 한 번에 업데이트하려면 특히 유용합니다.

>[!NOTE] 자원의 일부를 완전히 교체하는 대신 업데이트하려는 경우 패치 작업을 [사용하여 리소스](update-resource.md)업데이트에 대한 문서를 참조하십시오.

**API 형식**

PUT 요청은 테넌트 컨테이너에서 정의한 리소스에 대해서만 수행할 수 있습니다.

```http
PUT /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RESOURCE_TYPE}` | 스키마 라이브러리에서 업데이트할 리소스 유형입니다. 유효한 유형은 `datatypes`, `mixins`, `schemas`및 `classes`입니다. |
| `{RESOURCE_ID}` | URL로 인코딩된 `$id` URI 또는 `meta:altId` 리소스의 URL입니다. |

**요청**

이 샘플 요청은 이전 예제에서 생성된 속성 구성 데이터 형식을 대체합니다. 요청 본문은 데이터 형식을 만드는 데 사용된 POST 요청과 유사하게 보입니다. 단, 이제 데이터 형식에 새 값이 있는 업데이트된 필드 세트가 들어 있습니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Construction",
        "description":"Information related to the construction of the property.",
        "type":"object",
        "properties": {
          "dateOpened": {
            "type":"string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened."
          },
          "propertyType": {
            "type":"string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
              "standAlone",
              "highRise",
              "stripMall"
            ],
            "meta:enum": {
              "standAlone": "Stand-Alone Building",
              "highRise": "High Rise Building",
              "stripMall": "Strip Mall"
            }
          },
          "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property."
          },
          "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property."
          }
        } 
      }'
```

**응답**

성공적인 응답은 요청에 제공된 대로 업데이트된 필드 및 값을 보여주는 데이터 유형의 세부 정보를 반환합니다.

```JSON
{
    "title": "Property Construction",
    "description": "Information related to the construction of the property.",
    "type": "object",
    "properties": {
        "dateOpened": {
            "type": "string",
            "format": "date",
            "title": "Date Opened",
            "description": "The date the property was first opened.",
            "meta:xdmType": "date"
        },
        "propertyType": {
            "type": "string",
            "title": "Property Type",
            "description": "Type of building or structure in which the property exists.",
            "enum": [
                "standAlone",
                "highRise",
                "stripMall"
            ],
            "meta:enum": {
                "standAlone": "Stand-Alone Building",
                "highRise": "High Rise Building",
                "stripMall": "Strip Mall"
            },
            "meta:xdmType": "string"
        },
        "constructionCompany": {
            "type": "string",
            "title": "Construction Company",
            "description": "Name of the construction company that completed the construction of the property.",
            "meta:xdmType": "string"
        },
        "totalSquareFootage": {
            "type": "integer",
            "title": "Total Square Footage",
            "description": "Total square footage of the property.",
            "meta:xdmType": "int"
        }
    },
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:altId": "_{TENANT_ID}.datatypes.24c643f618647344606222c494bd0102",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102",
    "version": "1.2",
    "meta:resourceType": "datatypes",
    "meta:registryMetadata": {
        "repo:createDate": 1552087079285,
        "repo:lastModifiedDate": 1552090569013,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```
