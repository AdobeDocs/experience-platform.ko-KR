---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;xdm;경험 데이터 모델;네임스페이스;네임스페이스;호환성 모드;Confliction;home;popular topics;schema;xdm;experience data model;namespace;namespace;compatibility mode;xed;
solution: Experience Platform
title: 경험 데이터 모델(XDM)의 이름 지정
topic-legacy: overviews
description: XDM(Experience Data Model)의 이름 대싱을 통해 스키마를 확장하고 다른 스키마 구성 요소가 함께 가져오면 필드 충돌을 방지하는 방법을 알아봅니다.
source-git-commit: b4c4f8f7e428d27f389bff5591a03925b6afa6d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# 경험 데이터 모델(XDM)의 이름 지정

XDM(경험 데이터 모델) 스키마의 모든 필드에는 연관된 네임스페이스가 있습니다. 이러한 네임스페이스를 통해 여러 스키마 구성 요소를 함께 가져올 때 스키마를 확장하고 필드 충돌을 방지할 수 있습니다. 이 문서에서는
XDM과 [스키마 레지스트리 API](../api/overview.md)에 표시되는 방식입니다.

Namespacing을 사용하면 한 네임스페이스에 있는 필드를 다른 네임스페이스에 있는 동일한 필드와 다른 의미를 갖는 것으로 정의할 수 있습니다. 실제로 필드의 네임스페이스는 필드를 만든 사람(예: 표준 XDM(Adobe), 공급업체 또는 조직)을 나타냅니다.

예를 들어 `xdm` 네임스페이스에 있는 표준 `mobilePhone` 필드가 있는 [[!UICONTROL 개인 연락처 세부 사항] 필드 그룹](../field-groups/profile/demographic-details.md)을 사용하는 XDM 스키마를 고려하십시오. 동일한 스키마에서는 다른 네임스페이스(사용자의 [테넌트 ID](../api/getting-started.md#know-your-tenant_id)) 아래에 별도의 `mobilePhone` 필드를 만들 수도 있습니다. 이러한 두 필드는 서로 다른 기본 의미나 제한을 가지고 있을 때 함께 사용할 수 있습니다.

## Namespacing 구문

다음 섹션에서는 XDM 구문에서 네임스페이스가 어떻게 할당되는지 보여 줍니다.

### 표준 XDM {#standard}

표준 XDM 구문은 네임스페이스가 스키마에서 표시되는 방식에 대한 통찰력을 제공합니다([Adobe Experience Platform](#compatibility)에서 변환하는 방법 포함).

표준 XDM은 [JSON-LD](https://json-ld.org/) 구문을 사용하여 필드에 네임스페이스를 할당합니다. 이 네임스페이스는 `xdm` 네임스페이스의 `https://ns.adobe.com/xdm` 같은 URI 형식이나 스키마의 `@context` 속성에 구성된 대표 접두어로 제공됩니다.

다음은 표준 XDM 구문의 제품 스키마 예입니다. `@id`(JSON-LD 사양에 의해 정의된 고유 식별자)를 제외하고 `properties` 아래의 각 필드는 네임스페이스로 시작하여 필드 이름으로 끝납니다. `@context` 아래에 정의된 축약형 접두어를 사용하는 경우 네임스페이스 및 필드 이름은 콜론(`:`)으로 구분됩니다. 접두어를 사용하지 않는 경우 네임스페이스 및 필드 이름은 슬래시(`/`)로 구분됩니다.

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
| `@context` | 전체 네임스페이스 URI 대신 사용할 수 있는 축약형 접두어를 정의하는 개체입니다(`properties`). |
| `@id` | [JSON-LD 사양](https://json-ld.org/spec/latest/json-ld/#node-identifiers)에 의해 정의된 레코드에 대한 고유 식별자입니다. |
| `xdm:sku` | 네임스페이스를 나타내는 대표 접두사를 사용하는 필드의 예입니다. 이 경우 `xdm`은 네임스페이스(`https://ns.adobe.com/xdm`)이고 `sku`는 필드 이름입니다. |
| `https://ns.adobe.com/xdm/channels/application` | 전체 네임스페이스 URI를 사용하는 필드의 예입니다. 이 경우 `https://ns.adobe.com/xdm/channels`은 네임스페이스이고 `application`은 필드 이름입니다. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 공급업체 리소스에서 제공하는 필드는 고유한 네임스페이스를 사용합니다. 이 예에서 `https://ns.adobe.com/vendorA/product`은 공급업체 네임스페이스이고 `stockNumber`은 필드 이름입니다. |
| `tenantId:internalSku` | 조직에서 정의한 필드는 고유한 테넌트 ID를 네임스페이스로 사용합니다. 이 예에서 `tenantId`은(는) 테넌트 네임스페이스(`https://ns.adobe.com/tenantId`)이고 `internalSku`는 필드 이름입니다. |

{style=&quot;table-layout:auto&quot;}

### 호환성 모드 {#compatibility}

Adobe Experience Platform에서 XDM 스키마는 네임스페이스를 나타내는 JSON-LD 구문을 사용하지 않는 [호환성 모드](../api/appendix.md#compatibility) 구문으로 표시됩니다. 대신 Platform은 네임스페이스를 상위 필드로 변환하고 그 아래에 필드를 중첩합니다(밑줄로 시작).

예를 들어 표준 XDM `repo:createdDate`은(는) `_repo.createdDate`으로 변환되고 호환성 모드의 다음 구조 아래에 나타납니다.

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

`xdm` 네임스페이스를 사용하는 필드는 `properties` 아래에 루트 필드로 표시되고 [표준 XDM 구문](#standard)에 나타나는 `xdm:` 접두어를 삭제합니다. 예를 들어 `xdm:sku`은(는) 단순히 `sku`로 나열됩니다.

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

이 안내서에서는 XDM 네임스페이스와 JSON에 표시되는 방식에 대한 개요를 제공합니다. API를 사용하여 XDM 스키마를 구성하는 방법에 대한 자세한 내용은 [스키마 레지스트리 API 안내서](../api/overview.md)를 참조하십시오.
