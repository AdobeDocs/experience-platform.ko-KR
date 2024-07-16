---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;xdm;경험 데이터 모델;네임스페이스;네임스페이스;호환성 모드;xed;
solution: Experience Platform
title: Experience Data Model(XDM)의 이름 간격
description: XDM(Experience Data Model)의 이름 간격을 통해 스키마를 확장하고 다른 스키마 구성 요소를 가져올 때 필드 충돌을 방지하는 방법에 대해 알아봅니다.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: d26a0586a992948e1b278bae91a985fe3d9f1ee8
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Experience Data Model(XDM)의 이름 간격

>[!IMPORTANT]
>
>XDM에서 네임스페이스(이 페이지의 주제)는 스키마의 필드를 구분하는 데 사용됩니다. 이는 ID 값을 구별하는 데 네임스페이스가 사용되는 ID 서비스의 ID 네임스페이스 개념과 다릅니다. 자세한 내용은 ID 서비스의 [네임스페이스](../../identity-service/features/namespaces.md)에 대한 설명서를 참조하십시오.

XDM(Experience Data Model) 스키마의 모든 필드에는 연결된 네임스페이스가 있습니다. 이러한 네임스페이스를 사용하면 서로 다른 스키마 구성 요소를 함께 가져올 때 스키마를 확장하고 필드 충돌을 방지할 수 있습니다. 이 문서에서는 XDM의 네임스페이스와 [스키마 레지스트리 API](../api/overview.md)에서 네임스페이스를 나타내는 방법에 대한 개요를 제공합니다.

이름 간격을 사용하면 한 네임스페이스의 필드를 다른 네임스페이스의 동일한 필드와 다른 의미로 정의할 수 있습니다. 실제로 필드의 네임스페이스는 필드를 만든 사람(예: 표준 XDM(Adobe), 공급업체 또는 조직)을 나타냅니다.

예를 들어 `xdm` 네임스페이스에 있는 표준 `mobilePhone` 필드가 있는 [[!UICONTROL 개인 연락처 세부 정보] 필드 그룹](../field-groups/profile/demographic-details.md)을(를) 사용하는 XDM 스키마를 고려해 보십시오. 동일한 스키마에서는 다른 네임스페이스([테넌트 ID](../api/getting-started.md#know-your-tenant_id)) 아래에 별도의 `mobilePhone` 필드를 자유롭게 만들 수도 있습니다. 이 두 장은 서로 다른 밑바탕의 의미나 제약조건을 가지면서 함께 공존할 수 있다.

## 이름 간격 구문

다음 섹션에서는 XDM 구문에서 네임스페이스가 지정되는 방법을 보여줍니다.

### 표준 XDM {#standard}

표준 XDM 구문은 스키마에서 네임스페이스가 표현되는 방법([Adobe Experience Platform에서 네임스페이스를 변환하는 방법](#compatibility) 포함)에 대한 통찰력을 제공합니다.

표준 XDM은 [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) 구문을 사용하여 필드에 네임스페이스를 할당합니다. 이 네임스페이스는 URI(예: `xdm` 네임스페이스의 `https://ns.adobe.com/xdm`) 형태로 제공되거나 스키마의 `@context` 특성에 구성된 축약 접두사로 사용됩니다.

다음은 표준 XDM 구문의 제품에 대한 예제 스키마입니다. `@id`(JSON-LD 사양에 정의된 고유 식별자)을 제외하고 `properties`의 각 필드는 네임스페이스로 시작하고 필드 이름으로 끝납니다. `@context` 아래에 정의된 축약 접두사를 사용하는 경우 네임스페이스와 필드 이름은 콜론(`:`)으로 구분됩니다. 접두사를 사용하지 않는 경우 네임스페이스와 필드 이름은 슬래시(`/`)로 구분됩니다.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `@context` | `properties`에서 전체 네임스페이스 URI 대신 사용할 수 있는 줄임 접두사를 정의하는 개체입니다. |
| `@id` | [JSON-LD 사양](https://www.w3.org/TR/json-ld11/#node-identifiers)에 정의된 레코드의 고유 식별자입니다. |
| `xdm:sku` | 축약 접두사를 사용하여 네임스페이스를 나타내는 필드의 예 이 경우 `xdm`은(는) 네임스페이스(`https://ns.adobe.com/xdm`)이고 `sku`은(는) 필드 이름입니다. |
| `https://ns.adobe.com/xdm/channels/application` | 전체 네임스페이스 URI를 사용하는 필드의 예입니다. 이 경우 `https://ns.adobe.com/xdm/channels`은(는) 네임스페이스이고 `application`은(는) 필드 이름입니다. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 공급업체 리소스에서 제공한 필드는 고유한 네임스페이스를 사용합니다. 이 예제에서 `https://ns.adobe.com/vendorA/product`은 공급업체 네임스페이스이고 `stockNumber`은(는) 필드 이름입니다. |
| `tenantId:internalSku` | 조직에서 정의한 필드는 고유한 테넌트 ID를 네임스페이스로 사용합니다. 이 예제에서 `tenantId`은 테넌트 네임스페이스(`https://ns.adobe.com/tenantId`)이고 `internalSku`은(는) 필드 이름입니다. |

{style="table-layout:auto"}

### 호환성 모드 {#compatibility}

Adobe Experience Platform에서 XDM 스키마는 네임스페이스를 나타내는 데 JSON-LD 구문을 사용하지 않는 [호환성 모드](../api/appendix.md#compatibility) 구문으로 표시됩니다. 대신 Platform은 네임스페이스를 상위 필드(밑줄로 시작)로 변환하고 그 아래에 필드를 중첩합니다.

예를 들어 표준 XDM `repo:createdDate`은(는) `_repo.createdDate`(으)로 변환되며 호환성 모드에서 다음 구조에 나타납니다.

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

`xdm` 네임스페이스를 사용하는 필드는 `properties`에서 루트 필드로 나타나고 [표준 XDM 구문](#standard)에 나타나는 `xdm:` 접두사를 삭제합니다. 예를 들어 `xdm:sku`은(는) 대신 `sku`(으)로 나열됩니다.

다음 JSON은 위에 표시된 표준 XDM 구문 예가 호환성 모드로 변환되는 방식을 나타냅니다.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## 다음 단계

이 안내서에서는 XDM 네임스페이스와 네임스페이스가 JSON에서 표현되는 방법에 대한 개요를 제공합니다. API를 사용하여 XDM 스키마를 구성하는 방법에 대한 자세한 내용은 [스키마 레지스트리 API 안내서](../api/overview.md)를 참조하십시오.
