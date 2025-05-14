---
title: 스키마 레지스트리 API에서 XDM 필드 정의
description: 스키마 레지스트리 API에서 사용자 지정 XDM(경험 데이터 모델) 리소스를 만들 때 다양한 필드를 정의하는 방법을 알아봅니다.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6c6104a6aa0a80c886f4f02486a7645eb95da781
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# 스키마 레지스트리 API에서 XDM 필드 정의

모든 XDM(Experience Data Model) 필드는 해당 필드 형식에 적용되는 표준 [JSON 스키마](https://json-schema.org/) 제약 조건을 사용하여 정의되며, Adobe Experience Platform에서 필드 이름에 대한 추가 제약 조건이 적용됩니다. 스키마 레지스트리 API를 사용하면 형식 및 선택적 제약 조건을 사용하여 스키마에서 사용자 지정 필드를 정의할 수 있습니다. XDM 필드 유형은 필드 수준 특성 `meta:xdmType`에 의해 노출됩니다.

>[!NOTE]
>
>`meta:xdmType`은(는) 시스템에서 생성한 값이므로 API를 사용할 때는([사용자 지정 맵 유형을 만드는 경우](#custom-maps) 제외) 이 속성을 필드의 JSON에 추가할 필요가 없습니다. 가장 좋은 방법은 아래 표에 정의된 대로 적절한 최소/최대 제약 조건과 함께 JSON 스키마 유형(예: `string` 및 `integer`)을 사용하는 것입니다.

이 안내서에서는 속성(선택 사항)이 있는 필드 유형을 포함하여 다양한 필드 유형을 정의하기 위한 적절한 형식을 간략하게 설명합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/type.html)를 통해 확인할 수 있습니다.

시작하려면 원하는 필드 유형을 찾아 제공된 샘플 코드를 사용하여 [필드 그룹 만들기](../api/field-groups.md#create) 또는 [데이터 유형 만들기](../api/data-types.md#create)를 위한 API 요청을 빌드하십시오.

## [!UICONTROL 문자열] {#string}

[!UICONTROL 문자열] 필드는 `type: string`(으)로 표시됩니다.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

다음 추가 속성을 통해 문자열에 입력할 수 있는 값 종류를 선택적으로 제한할 수 있습니다.

* `pattern`: 제한할 정규 표현식 패턴입니다.
* `minLength`: 문자열의 최소 길이입니다. 문자열은 기본적으로 최소값 `1`을(를) 받습니다.
* `maxLength`: 문자열의 최대 길이입니다.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] 필드는 `format` 속성이 `uri`(으)로 설정된 `type: string`로 표시됩니다. 다른 속성은 허용되지 않습니다.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 열거형] {#enum}

[!UICONTROL 열거형] 필드는 열거형 값 자체가 `enum` 배열에 제공되는 `type: string`을(를) 사용해야 합니다.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

선택적으로 `meta:enum` 속성의 각 값에 대해 고객 대면 레이블을 제공할 수 있으며, 각 레이블은 `enum`의 해당 값에 맞춰집니다.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
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
  }
}
```

>[!NOTE]
>
>`meta:enum` 값이 열거형을 선언하거나 데이터 유효성 검사를 자체적으로 **하지**&#x200B;않습니다. 대부분의 경우 데이터가 제한되도록 `meta:enum`에서 제공된 문자열도 `enum`에서 제공됩니다. 그러나 해당 `enum` 배열 없이 `meta:enum`이(가) 제공되는 사용 사례가 있습니다. 자세한 내용은 [제안 값 정의](../tutorials/suggested-values.md)에 대한 자습서를 참조하십시오.

값을 제공하지 않을 경우 필드가 사용할 기본 `enum` 값을 나타내기 위해 `default` 속성을 선택적으로 제공할 수 있습니다.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
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

>[!IMPORTANT]
>
>`default` 값이 제공되지 않고 열거형 필드가 `required`(으)로 설정된 경우, 이 필드에 대해 허용되는 값이 없는 레코드는 수집 시 유효성 검사가 실패합니다.

## [!UICONTROL 숫자] {#number}

숫자 필드는 `type: number`(으)로 표시되며 다른 필수 속성이 없습니다.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` 형식은 정수 또는 부동 소수점 숫자의 모든 숫자 형식에 사용되는 반면, [`integer` 형식](#integer)은 특히 정수에 사용됩니다. 각 유형의 사용 사례에 대한 자세한 내용은 [숫자 유형에 대한 JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/numeric.html)를 참조하십시오.

## [!UICONTROL 정수] {#integer}

[!UICONTROL 정수] 필드는 `type: integer`(으)로 표시되며 다른 필수 필드는 없습니다.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>`integer` 형식이 정수 또는 부동 소수점 숫자와 같은 모든 숫자 형식에 대해 [`number` 형식](#number)이(가) 사용됩니다. 각 유형의 사용 사례에 대한 자세한 내용은 [숫자 유형에 대한 JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/numeric.html)를 참조하십시오.

`minimum` 및 `maximum` 속성을 정의에 추가하여 정수 범위를 선택적으로 제한할 수 있습니다. 스키마 빌더 UI에서 지원되는 다른 숫자 유형은 [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short), [[!UICONTROL Byte]](#byte)과(와) 같이 특정 `minimum` 및 `maximum` 제약 조건을 가진 `integer` 유형입니다.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL 길게] {#long}

스키마 빌더 UI를 통해 만든 [!UICONTROL Long] 필드에 해당하는 값은 특정 `minimum` 및 `maximum` 값(`-9007199254740992` 및 `9007199254740992`)을 가진 [`integer` 형식 필드](#integer)입니다.

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL 짧음] {#short}

스키마 빌더 UI를 통해 만든 [!UICONTROL Short] 필드에 해당하는 값은 특정 `minimum` 및 `maximum` 값(`-32768` 및 `32767`)을 가진 [`integer` 형식 필드](#integer)입니다.

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32767
}
```

## [!UICONTROL 바이트] {#byte}

스키마 빌더 UI를 통해 만든 [!UICONTROL 바이트] 필드에 해당하는 값은 특정 `minimum` 및 `maximum` 값(`-128` 및 `127`)을 가진 [`integer` 형식 필드](#integer)입니다.

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 127
}
```

## [!UICONTROL 부울] {#boolean}

[!UICONTROL 부울] 필드는 `type: boolean`(으)로 표시됩니다.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

선택적으로 수집 중에 명시적 값이 제공되지 않을 때 필드가 사용할 `default` 값을 제공할 수 있습니다.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>`default` 값이 제공되지 않고 부울 필드가 `required`(으)로 설정된 경우, 이 필드에 대해 허용되는 값이 없는 레코드는 수집 시 유효성 검사가 실패합니다.

## [!UICONTROL 날짜] {#date}

[!UICONTROL 날짜] 필드는 `type: string` 및 `format: date`(으)로 표시됩니다. 데이터를 수동으로 입력하는 사용자에 대한 샘플 날짜 문자열을 표시하려는 경우 활용할 `examples` 배열을 선택적으로 제공할 수도 있습니다.

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL DateTime] {#date-time}

[!UICONTROL DateTime] 필드는 `type: string` 및 `format: date-time`(으)로 표시됩니다. 데이터를 수동으로 입력하는 사용자에 대한 샘플 날짜/시간 문자열을 표시하려는 경우 활용할 `examples` 배열을 선택적으로 제공할 수도 있습니다.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL 배열] {#array}

[!UICONTROL 배열] 필드는 배열이 허용할 항목의 스키마를 정의하는 `type: array` 및 `items` 개체로 표시됩니다.

문자열 배열과 같은 기본 유형을 사용하여 배열 항목을 정의할 수 있습니다.

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

`$ref` 속성을 통해 데이터 형식의 `$id`을(를) 참조하여 기존 데이터 형식을 기반으로 배열 항목을 정의할 수도 있습니다. 다음은 [!UICONTROL 결제 항목] 개체의 배열입니다.

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL 개체] {#object}

[!UICONTROL 개체] 필드는 스키마 필드의 하위 속성을 정의하는 `type: object` 및 `properties` 개체로 표시됩니다.

`properties`에 정의된 각 하위 필드는 기본 `type`을(를) 사용하거나 해당 데이터 형식의 `$id`을(를) 가리키는 `$ref` 속성을 통해 기존 데이터 형식을 참조하여 정의할 수 있습니다.

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

해당 데이터 형식 자체가 `type: object`(으)로 정의된 경우 데이터 형식을 참조하여 전체 개체를 정의할 수도 있습니다.

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 맵] {#map}

맵 필드는 기본적으로 키가 제한되지 않은 [`object` 형식의 필드](#object)입니다. 개체와 마찬가지로 맵의 `type` 값은 `object`이지만 `meta:xdmType`이(가) 명시적으로 `map`(으)로 설정되어 있습니다.

**맵은 속성을 정의하면 안 됩니다**. 맵 내에 포함된 값의 형식을 설명하기 위해 **must**&#x200B;에서 단일 `additionalProperties` 스키마를 정의해야 합니다(각 맵에는 단일 데이터 형식만 포함할 수 있음). `type` 값은 `string` 또는 `integer`이어야 합니다.

예를 들어 문자열 유형 값이 있는 맵 필드는 다음과 같이 정의됩니다.

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

사용자 정의 맵 필드 만들기에 대한 자세한 내용은 아래 섹션을 참조하십시오.

### 사용자 정의 맵 유형 만들기 {#custom-maps}

XDM에서 &quot;맵과 유사한&quot; 데이터를 효율적으로 지원하기 위해 `map`(으)로 설정된 `meta:xdmType`(으)로 개체에 주석을 달아 키 집합이 제약 조건 없는 것처럼 개체를 관리해야 함을 명확히 할 수 있습니다. 맵 필드에 수집되는 데이터는 문자열 키를 사용해야 하며, 문자열 또는 정수 값만 사용해야 합니다(`additionalProperties.type`에서 결정).

XDM에서는 이 스토리지 힌트의 사용에 대해 다음과 같은 제한 사항을 적용합니다.

* 맵 형식은 `object` 형식이어야 합니다.
* 맵 유형에는 속성이 정의되지 않아야 합니다(즉, &quot;빈&quot; 개체를 정의함).
* 맵 유형에는 맵 내에 배치할 수 있는 값을 설명하는 `additionalProperties.type` 필드(`string` 또는 `integer`)가 포함되어야 합니다.

맵 유형 필드는 다음과 같은 성능 단점이 있으므로 반드시 필요한 경우에만 사용해야 합니다.

* 1억 개의 레코드에 대해 [Adobe Experience Platform 쿼리 서비스](../../query-service/home.md)의 응답 시간이 3초에서 10초로 감소합니다.
* 맵의 키가 16개 미만이어야 합니다. 그렇지 않으면 더 이상 성능이 저하될 수 있습니다.

Experience Platform 사용자 인터페이스에서도 맵 유형 필드의 키를 추출하는 방법에 제한이 있습니다. 개체 유형 필드는 확장할 수 있지만 맵은 대신 단일 필드로 표시됩니다.

## 다음 단계

이 안내서에서는 API에서 다양한 필드 유형을 정의하는 방법을 다룹니다. XDM 필드 형식 지정 방법에 대한 자세한 내용은 [XDM 필드 형식 제약 조건](../schema/field-constraints.md)에 대한 안내서를 참조하십시오.
