---
title: 소프트 열거형 필드 확장
description: 스키마 레지스트리 API에서 소프트 열거형 필드를 확장하는 방법을 알아봅니다.
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a26c8d43ff7874bcedd2adb3d6da995986198c96
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 소프트 열거형 필드 확장

XDM(Experience Data Model)에서 열거형 필드는 사전 정의된 값 하위 집합으로 제한되는 문자열 필드를 나타냅니다. 열거형 필드는 수집된 데이터가 허용되는 값 집합(&quot;하드 열거형&quot;이라고 함)을 준수하는지 확인하기 위해 유효성 검사를 제공할 수 있으며, 제한을 집행하지 않고 제안된 값 집합(&quot;소프트 열거형&quot;이라고 함)을 단순히 나타낼 수 있습니다.

스키마 레지스트리 API에서 하드 열거형에 대한 제한 값은 `enum` 배열, `meta:enum` 객체에서는 해당 값에 대해 친숙한 표시 이름을 제공합니다.

```json
"sampleHardEnumField": {
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

하드 열거형 필드의 경우 스키마 레지스트리에서 다음을 허용하지 않습니다 `meta:enum` 에 제공된 값 이상으로 확장됩니다. `enum`를 지정하는 경우, 해당 제한 외에 문자열 값을 수집하려고 하면 유효성 검사가 전달되지 않습니다.

반면에 소프트 열거형 필드는 다음을 포함하지 않습니다 `enum` 스토리지 및 는 `meta:enum` 제안된 값을 표시하기 위한 객체:

```json
"sampleSoftEnumField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

소프트 열거형에는 하드 열거형과 동일한 유효성 검사 제한이 없으므로 해당 열거형은 `meta:enum` 속성을 확장하여 새 값을 포함할 수 있습니다. 이 자습서에서는 스키마 레지스트리 API에서 표준 및 사용자 지정 소프트 열거형 필드를 확장하는 방법을 설명합니다.

## 전제 조건

이 안내서에서는 사용자가 XDM의 스키마 구성 요소 및 스키마 레지스트리 API를 사용하여 XDM 리소스를 만들고 편집하는 방법을 잘 알고 있다고 가정합니다. 소개가 필요한 경우 다음 설명서를 참조하십시오.

* [스키마 작성 기본 사항](../schema/composition.md)
* [스키마 레지스트리 API 안내서](../api/overview.md)

## 표준 소프트 열거형 필드 확장

확장 `meta:enum` 표준 문자열 필드의 경우 [친숙한 이름 설명자](../api/descriptors.md#friendly-name) 참조하십시오.

>[!NOTE]
>
>표준 소프트 열거형은 스키마 수준에서만 확장할 수 있습니다. 즉, `meta:enum` 한 스키마의 표준 필드 중 하나는 동일한 표준 필드를 사용하는 다른 스키마에는 영향을 주지 않습니다.

다음 요청은 소프트 열거형 값을 표준에 추가합니다 `eventType` 필드(에서 제공) [XDM ExperienceEvent 클래스](../classes/experienceevent.md))에 대해 사용할 수 있습니다. `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 사용자 지정 소프트 열거형 필드 확장

확장 `meta:enum` 사용자 지정 필드의 경우 PATCH 요청을 통해 필드의 상위 클래스, 필드 그룹 또는 데이터 유형을 업데이트할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

이 안내서에서는 스키마 레지스트리 API에서 소프트 열거형을 확장하는 방법을 다룹니다. 다음 안내서를 참조하십시오. [api에서 사용자 지정 필드 정의](./custom-fields-api.md) 를 참조하십시오.
