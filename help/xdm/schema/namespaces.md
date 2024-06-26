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
>XDM에서 네임스페이스(이 페이지의 주제)는 스키마의 필드를 구분하는 데 사용됩니다. 이는 ID 값을 구별하는 데 네임스페이스가 사용되는 ID 서비스의 ID 네임스페이스 개념과 다릅니다. 의 설명서를 읽어 보십시오. [identity 서비스의 네임스페이스](../../identity-service/features/namespaces.md) 추가 정보.

XDM(Experience Data Model) 스키마의 모든 필드에는 연결된 네임스페이스가 있습니다. 이러한 네임스페이스를 사용하면 서로 다른 스키마 구성 요소를 함께 가져올 때 스키마를 확장하고 필드 충돌을 방지할 수 있습니다. 이 문서에서는 XDM의 네임스페이스에 대한 개요와 네임스페이스가 [스키마 레지스트리 API](../api/overview.md).

이름 간격을 사용하면 한 네임스페이스의 필드를 다른 네임스페이스의 동일한 필드와 다른 의미로 정의할 수 있습니다. 실제로 필드의 네임스페이스는 필드를 만든 사람(예: 표준 XDM(Adobe), 공급업체 또는 조직)을 나타냅니다.

예를 들어 를 사용하는 XDM 스키마를 고려해 보겠습니다. [[!UICONTROL 개인 연락처 세부 정보] 필드 그룹](../field-groups/profile/demographic-details.md), 표준 포함 `mobilePhone` 에 있는 필드 `xdm` 네임스페이스입니다. 동일한 스키마에서 별도의 를 만들 수도 있습니다 `mobilePhone` 다른 네임스페이스 아래에 있는 필드 (사용자: [임차인 ID](../api/getting-started.md#know-your-tenant_id)). 이 두 장은 서로 다른 밑바탕의 의미나 제약조건을 가지면서 함께 공존할 수 있다.

## 이름 간격 구문

다음 섹션에서는 XDM 구문에서 네임스페이스가 지정되는 방법을 보여줍니다.

### 표준 XDM {#standard}

표준 XDM 구문은 스키마에서 네임스페이스가 표현되는 방식에 대한 통찰력을 제공합니다(다음을 포함) [Adobe Experience Platform에서 번역되는 방법](#compatibility)).

표준 XDM 사용 [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) 네임스페이스를 필드에 할당하는 구문 이 네임스페이스는 URI(예: `https://ns.adobe.com/xdm` 대상: `xdm` namespace) 형식으로나, 또는 `@context` 스키마 속성.

다음은 표준 XDM 구문의 제품에 대한 예제 스키마입니다. 를 제외하고 `@id` (JSON-LD 사양으로 정의된 고유 식별자), 각 필드 `properties` 네임스페이스로 시작하고 필드 이름으로 끝납니다. 아래에 정의된 축약 접두사를 사용하는 경우 `@context`, 네임스페이스와 필드 이름은 콜론(`:`). 접두사를 사용하지 않는 경우에는 네임스페이스와 필드 이름이 슬래시(`/`).

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
| `@context` | 아래에서 전체 네임스페이스 URI 대신 사용할 수 있는 줄임 접두사를 정의하는 개체입니다. `properties`. |
| `@id` | 로 정의된 레코드의 고유 식별자 [JSON-LD 사양](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | 축약 접두사를 사용하여 네임스페이스를 나타내는 필드의 예 이 경우, `xdm` 은(는) 네임스페이스입니다(`https://ns.adobe.com/xdm`), 및 `sku` 는 필드 이름입니다. |
| `https://ns.adobe.com/xdm/channels/application` | 전체 네임스페이스 URI를 사용하는 필드의 예입니다. 이 경우, `https://ns.adobe.com/xdm/channels` 는 네임스페이스이며, `application` 는 필드 이름입니다. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 공급업체 리소스에서 제공한 필드는 고유한 네임스페이스를 사용합니다. 이 예에서는 `https://ns.adobe.com/vendorA/product` 는 공급업체 네임스페이스이며, `stockNumber` 는 필드 이름입니다. |
| `tenantId:internalSku` | 조직에서 정의한 필드는 고유한 테넌트 ID를 네임스페이스로 사용합니다. 이 예에서는 `tenantId` 은 임차인 네임스페이스(`https://ns.adobe.com/tenantId`), 및 `internalSku` 는 필드 이름입니다. |

{style="table-layout:auto"}

### 호환성 모드 {#compatibility}

Adobe Experience Platform에서 XDM 스키마는에 표시됩니다 [호환성 모드](../api/appendix.md#compatibility) 구문 - 네임스페이스를 나타내는 데 JSON-LD 구문을 사용하지 않습니다. 대신 Platform은 네임스페이스를 상위 필드(밑줄로 시작)로 변환하고 그 아래에 필드를 중첩합니다.

예: 표준 XDM `repo:createdDate` 이(가) (으)로 변환되었습니다. `_repo.createdDate` 및 는 호환성 모드에서 다음 구조에 나타납니다.

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

를 사용하는 필드 `xdm` 네임스페이스는 아래의 루트 필드로 표시됩니다. `properties` 및 드롭하기 `xdm:` 다음에 나타날 접두사 [표준 XDM 구문](#standard). 예를 들어, `xdm:sku` 간단히 다음과 같이 나열됩니다. `sku` 대신,

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

이 안내서에서는 XDM 네임스페이스와 네임스페이스가 JSON에서 표현되는 방법에 대한 개요를 제공합니다. API를 사용하여 XDM 스키마를 구성하는 방법에 대한 자세한 내용은 [스키마 레지스트리 API 안내서](../api/overview.md).
