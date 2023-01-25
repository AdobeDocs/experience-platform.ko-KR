---
title: API에서 추천 값 관리
description: 스키마 레지스트리 API의 문자열 필드에 제안된 값을 추가하는 방법을 알아봅니다.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: b1ef2de1e6f9c6168a5ee2a62b55812123783a3a
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---

# API에서 추천 값을 관리합니다

XDM(Experience Data Model)의 모든 문자열 필드에 대해 **enum** 필드의 값이 사전 정의된 세트에 수집할 수 없도록 제한합니다. 데이터를 열거형 필드에 수집하려고 하며 값이 해당 구성에 정의된 데이터와 일치하지 않으면 수집이 거부됩니다.

열거형과는 반대로, **제안된 값** 문자열 필드로 이동해도 처리할 수 있는 값이 제한되지 않습니다. 대신, 제안된 값은 [세그멘테이션 UI](../../segmentation/ui/overview.md) 문자열 필드를 속성으로 포함할 때.

>[!NOTE]
>
>필드의 업데이트된 제안된 값이 세그멘테이션 UI에 반영되는 경우 약 5분 지연이 있습니다.

이 안내서에서는 [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Adobe Experience Platform 사용자 인터페이스에서 이 작업을 수행하는 방법에 대한 단계는 다음을 참조하십시오. [열거형 및 제안된 값에 대한 UI 안내서](../ui/fields/enum.md).

## 전제 조건

이 안내서에서는 사용자가 XDM의 스키마 구성 요소 및 스키마 레지스트리 API를 사용하여 XDM 리소스를 만들고 편집하는 방법을 잘 알고 있다고 가정합니다. 소개가 필요한 경우 다음 설명서를 참조하십시오.

* [스키마 작성 기본 사항](../schema/composition.md)
* [스키마 레지스트리 API 안내서](../api/overview.md)

또한 다음을 검토하는 것이 좋습니다 [열거형 및 제안된 값의 진행 규칙](../ui/fields/enum.md#evolution) 기존 필드를 업데이트하는 경우. 결합에 참여하는 스키마에 대한 권장 값을 관리하는 경우, [열거형 및 제안된 값 병합 규칙](../ui/fields/enum.md#merging).

## 조성물

API에서 **enum** 필드는 `enum` 배열, `meta:enum` 객체에서는 해당 값에 대해 친숙한 표시 이름을 제공합니다.

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

열거형 필드의 경우 스키마 레지스트리에서 다음을 허용하지 않습니다 `meta:enum` 에 제공된 값 이상으로 확장됩니다. `enum`를 지정하는 경우, 해당 제한 외에 문자열 값을 수집하려고 하면 유효성 검사가 전달되지 않습니다.

또는 다음을 포함하지 않는 문자열 필드를 정의할 수 있습니다 `enum` 스토리지 및 는 `meta:enum` 표시할 개체 **제안된 값**:

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

문자열에 `enum` 제약 조건을 정의하는 배열 `meta:enum` 새 값을 포함하도록 속성을 확장할 수 있습니다.

## 표준 필드에 대해 제안된 값 관리

기존 표준 필드의 경우 다음을 수행할 수 있습니다 [추천 값 추가](#add-suggested-standard) 또는 [추천 값 비활성화](#disable-suggested-standard).

### 표준 필드에 제안된 값 추가 {#add-suggested-standard}

확장 `meta:enum` 표준 문자열 필드의 경우 [친숙한 이름 설명자](../api/descriptors.md#friendly-name) 참조하십시오.

>[!NOTE]
>
>문자열 필드에 대해 권장되는 값은 스키마 수준에서만 추가할 수 있습니다. 즉, `meta:enum` 한 스키마의 표준 필드 중 하나는 동일한 표준 필드를 사용하는 다른 스키마에는 영향을 주지 않습니다.

다음 요청은 추천 값을 표준에 추가합니다 `eventType` 필드(에서 제공) [XDM ExperienceEvent 클래스](../classes/experienceevent.md))에 대해 사용할 수 있습니다. `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

설명자를 적용한 후 스키마를 검색할 때 스키마 레지스트리에서 다음과 같이 응답합니다(공백으로 인해 응답이 잘림).

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>표준 필드에 이미 다음 값이 포함되어 있는 경우 `meta:enum`를 지정하면 설명자의 새 값이 기존 필드를 덮어쓰지 않고 대신 추가됩니다.
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

### 표준 필드에 대해 제안된 값 비활성화 {#disable-suggested-standard}

표준 문자열 필드에 `meta:enum`, 세그먼테이션에서 보지 않으려는 모든 값을 비활성화할 수 있습니다. 이 작업은 을(를) 만들어 [친숙한 이름 설명자](../api/descriptors.md#friendly-name) 를 포함하는 스키마용 `xdm:excludeMetaEnum` 속성을 사용합니다.

>[!IMPORTANT]
>
>해당 열거형 제약 조건이 없는 표준 필드에 대해 제안된 값만 비활성화할 수 있습니다. 즉, 필드에 `enum` 배열 `meta:excludeMetaEnum` 효과가 없습니다.
>
>의 섹션을 참조하십시오. [열거형 및 제안된 값의 진행 규칙](../ui/fields/enum.md#evolution) 기존 필드 편집 제한에 대한 자세한 내용은

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 추천 값 &quot;을 비활성화합니다.[!DNL Web Form Filled Out]&quot; 및 &quot;[!DNL Media ping]&quot; `eventType` 를 기반으로 하는 스키마에서 [XDM ExperienceEvent 클래스](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의되는 설명자의 유형입니다. 친숙한 이름 설명자의 경우 이 값을 `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | 다음 `$id` 설명자가 정의되는 스키마의 URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | 제안된 값을 관리할 특정 속성의 경로입니다. 경로는 슬래시(`/`)로 끝나는 것이 아닙니다. 포함하지 않음 `properties` 경로(예: `/personalEmail/address` 대신 `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | 세그먼테이션의 필드에 대해 제외해야 하는 제안된 값을 설명하는 개체입니다. 각 항목의 키와 값은 원본에 포함된 키와 일치해야 합니다 `meta:enum` 을 입력합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공한 응답은 HTTP 상태 201(생성됨) 및 새로 만든 설명자의 세부 정보를 반환합니다. 에 포함된 추천 값 `xdm:excludeMetaEnum` 이제 세그먼테이션 UI에서 숨겨집니다.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 사용자 지정 필드에 대한 권장 값 관리 {#suggested-custom}

를 관리하려면 `meta:enum` 사용자 지정 필드의 경우 PATCH 요청을 통해 필드의 상위 클래스, 필드 그룹 또는 데이터 유형을 업데이트할 수 있습니다.

>[!WARNING]
>
>표준 필드와 달리, `meta:enum` 사용자 지정 필드의 값은 해당 필드를 사용하는 다른 모든 스키마에 영향을 줍니다. 변경 사항이 스키마 간에 전파되지 않도록 하려면 대신 새 사용자 지정 리소스를 만드는 것이 좋습니다.
>
>* [사용자 지정 클래스 만들기](../api/classes.md#create)
>* [사용자 지정 필드 그룹 만들기](../api/field-groups.md#create)
>* [사용자 지정 데이터 유형 만들기](../api/data-types.md#create)


다음 요청은 를 업데이트합니다 `meta:enum` 사용자 지정 데이터 유형에서 제공하는 &quot;충성도 수준&quot; 필드의 값:

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

변경 사항을 적용한 후 스키마를 검색할 때 스키마 레지스트리가 다음과 같이 응답합니다(공백으로 인해 응답이 잘림).

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## 다음 단계

이 안내서에서는 스키마 레지스트리 API에서 문자열 필드에 대해 제안된 값을 관리하는 방법을 다룹니다. 다음 안내서를 참조하십시오. [api에서 사용자 지정 필드 정의](./custom-fields-api.md) 를 참조하십시오.
