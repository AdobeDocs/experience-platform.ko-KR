---
title: API에서 제안된 값 관리
description: 스키마 레지스트리 API의 문자열 필드에 제안된 값을 추가하는 방법을 알아봅니다.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# API에서 제안된 값 관리

XDM(Experience Data Model)의 문자열 필드에 대해 **enum** 필드가 사전 정의된 집합으로 수집할 수 있는 값을 제한합니다. 열거형 필드에 데이터를 수집하려고 하는데 값이 해당 구성에 정의된 값과 일치하지 않으면 수집이 거부됩니다.

열거형과는 대조적으로, 를 추가합니다 **제안 값** 문자열 필드로는 수집할 수 있는 값을 제한하지 않습니다. 대신, 제안 값은 [세분화 UI](../../segmentation/ui/overview.md) 문자열 필드를 속성으로 포함할 때.

>[!NOTE]
>
>필드의 업데이트된 제안 값이 세분화 UI에 반영되려면 약 5분이 걸립니다.

이 안내서에서는 다음을 사용하여 제안된 값을 관리하는 방법을 다룹니다. [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Adobe Experience Platform 사용자 인터페이스에서 이 작업을 수행하는 방법에 대한 단계는 [열거형 및 제안 값에 대한 UI 안내서](../ui/fields/enum.md).

## 사전 요구 사항

이 안내서에서는 사용자가 XDM의 스키마 구성 요소 및 스키마 레지스트리 API를 사용하여 XDM 리소스를 만들고 편집하는 방법을 잘 알고 있다고 가정합니다. 소개가 필요한 경우 다음 설명서를 참조하십시오.

* [스키마 컴포지션 기본 사항](../schema/composition.md)
* [스키마 레지스트리 API 안내서](../api/overview.md)

또한 다음을 검토하는 것이 좋습니다. [열거형 및 제안 값에 대한 진행 규칙](../ui/fields/enum.md#evolution) 기존 필드를 업데이트하는 경우. 유니온에 참여하는 스키마에 대한 제안 값을 관리하는 경우 다음을 참조하십시오. [열거형과 제안 값 병합 규칙](../ui/fields/enum.md#merging).

## 컴포지션

API에서 의 제한된 값 **enum** 필드는 로 표시됩니다. `enum` 배열, 반면에 `meta:enum` 객체에서는 다음 값에 대해 친숙한 표시 이름을 제공합니다.

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

열거형 필드의 경우 스키마 레지스트리에서 허용하지 않습니다. `meta:enum` 아래에 제공된 값 이상으로 확장되어야 합니다. `enum`, 해당 제약 조건 외부의 문자열 값을 수집하려고 하면 유효성 검사를 통과하지 못합니다.

또는 다음을 포함하지 않는 문자열 필드를 정의할 수 있습니다. `enum` 배열 및 만 사용 `meta:enum` 표시할 개체 **제안 값**:

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

문자열에 다음이 없으므로 `enum` 제약 조건을 정의하는 배열, `meta:enum` 속성을 확장하여 새 값을 포함할 수 있습니다.

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## 표준 필드에 제안 값 추가 {#add-suggested-standard}

을(를) 확장하려면 `meta:enum` 표준 문자열 필드의 경우 [설명자에 대한 알기 쉬운 이름](../api/descriptors.md#friendly-name) 특정 스키마에서 해당 필드.

>[!NOTE]
>
>문자열 필드에 대한 제안 값은 스키마 수준에서만 추가할 수 있습니다. 즉, `meta:enum` 한 스키마에 있는 표준 필드의 내용이 동일한 표준 필드를 사용하는 다른 스키마에는 영향을 주지 않습니다.

다음 요청은 표준에 제안된 값을 추가합니다 `eventType` 필드(에서 제공) [XDM ExperienceEvent 클래스](../classes/experienceevent.md)아래에 식별된 스키마용 `sourceSchema`:

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

설명자를 적용한 후 스키마를 검색할 때 스키마 레지스트리는 다음과 같이 응답합니다(공간에 대해 잘린 응답).

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
>표준 필드에 다음 값이 이미 포함된 경우 `meta:enum`, 설명자의 새 값이 기존 필드를 덮어쓰지 않고 대신 추가됩니다.
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

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

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

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

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
``` -->

## 사용자 정의 필드에 대한 제안 값 관리 {#suggested-custom}

을 관리하려면 `meta:enum` 사용자 지정 필드의 경우 PATCH 요청을 통해 필드의 상위 클래스, 필드 그룹 또는 데이터 유형을 업데이트할 수 있습니다.

>[!WARNING]
>
>표준 필드와 달리 `meta:enum` 사용자 지정 필드의 값은 해당 필드를 사용하는 다른 모든 스키마에 영향을 줍니다. 변경 사항이 스키마 간에 전파되지 않도록 하려면 대신 새 사용자 지정 리소스를 만드는 것이 좋습니다.
>
>* [사용자 정의 클래스 만들기](../api/classes.md#create)
>* [사용자 정의 필드 그룹 만들기](../api/field-groups.md#create)
>* [사용자 지정 데이터 유형 만들기](../api/data-types.md#create)


다음 요청은 `meta:enum` 사용자 지정 데이터 유형에서 제공하는 &quot;충성도 수준&quot; 필드의 경우:

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

변경 사항을 적용한 후 스키마 검색 시 스키마 레지스트리는 다음과 같이 응답합니다(응답은 공백으로 잘림).

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

이 안내서에서는 스키마 레지스트리 API의 문자열 필드에 대해 제안된 값을 관리하는 방법을 다룹니다. 다음 안내서를 참조하십시오 [api에서 사용자 정의 필드 정의](./custom-fields-api.md) 다른 필드 유형을 만드는 방법에 대한 자세한 내용을 보려면 여기를 클릭하십시오.
