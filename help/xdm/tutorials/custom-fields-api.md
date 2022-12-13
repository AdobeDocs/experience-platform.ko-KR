---
title: 스키마 레지스트리 API에서 XDM 필드 정의
description: 스키마 레지스트리 API에서 사용자 지정 XDM(Experience Data Model) 리소스를 만들 때 다양한 필드를 정의하는 방법을 알아봅니다.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 0947eb38bdb18cb3783723cb11be79d3d32a3b76
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# 스키마 레지스트리 API에서 XDM 필드 정의

모든 XDM(경험 데이터 모델) 필드는 표준을 사용하여 정의됩니다 [JSON 스키마](https://json-schema.org/) 필드 유형에 적용되는 제한 조건 및 Adobe Experience Platform에 의해 적용되는 필드 이름에 대한 추가 제한. 스키마 레지스트리 API를 사용하면 형식 및 선택적 제약 조건을 사용하여 스키마에서 사용자 지정 필드를 정의할 수 있습니다. XDM 필드 유형은 필드 수준 특성에 의해 노출됩니다. `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 는 시스템에서 생성한 값이므로 API를 사용할 때(단, [사용자 지정 맵 유형 만들기](#custom-maps)). 가장 좋은 방법은 JSON 스키마 유형(예: `string` 및 `integer`)을 클릭하여 아래 표에 정의된 대로 적절한 최소/최대 제한을 지정합니다.

이 안내서에서는 선택적 속성이 있는 필드 유형을 비롯하여 다양한 필드 유형을 정의하는 데 적합한 형식을 간략하게 설명합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/type.html).

시작하려면 원하는 필드 유형을 찾아 제공된 샘플 코드를 사용하여 API 요청을 작성합니다 [필드 그룹 만들기](../api/field-groups.md#create) 또는 [데이터 유형 만들기](../api/data-types.md#create).

## [!UICONTROL 문자열] {#string}

[!UICONTROL 문자열] 필드는 `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

다음 추가 속성을 통해 문자열에 입력할 수 있는 값 종류를 선택적으로 제한할 수 있습니다.

* `pattern`: 로 제한할 정규 표현식 패턴입니다.
* `minLength`: 문자열의 최소 길이입니다.
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

[!UICONTROL URI] 필드는 `type: string` 사용 `format` 속성 설정 `uri`. 다른 속성은 허용되지 않습니다.

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 열거형] {#enum}

[!UICONTROL 열거형] 필드를 사용해야 합니다. `type: string`로 설정되면, `enum` 배열:

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

각 값에 대한 선택적 고객 응대 레이블을 `meta:enum` 각 레이블이 해당 `enum` 값.

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
>다음 `meta:enum` 값은 **not** 열거형을 선언하거나 데이터 유효성 검사를 직접 구동합니다. 대부분의 경우 `meta:enum` 다음 항목에서도 제공됩니다. `enum` 가 있어야 합니다. 그러나 다음과 같은 몇 가지 사용 사례가 있습니다 `meta:enum` 이(가) 해당 없이 제공됩니다 `enum` 배열입니다. 다음에서 자습서를 참조하십시오. [추천 값 정의](../tutorials/suggested-values.md) 추가 정보.

원할 경우 `default` 기본값을 나타내는 속성 `enum` 값이 제공되지 않을 경우 필드에서 사용할 값입니다.

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
>없는 경우 `default` 값이 제공되고 enum 필드가 `required`: 이 필드에 대해 허용된 값이 없는 레코드는 수집 시 유효성 검사에 실패합니다.

## [!UICONTROL 숫자] {#number}

숫자 필드는 `type: number` 및 에는 다른 필수 속성이 없습니다.

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` 유형은 정수 또는 부동 소수점 숫자와 같은 모든 숫자 유형에 사용되지만 [`integer` 유형](#integer) 특히 정수 계열 숫자에 사용됩니다. 자세한 내용은 [숫자 유형에 대한 JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/numeric.html) 를 참조하십시오.

## [!UICONTROL 정수] {#integer}

[!UICONTROL 정수] 필드는 `type: integer` 및 에는 다른 필수 필드가 없습니다.

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>While `integer` 유형은 특히 정수 숫자를 나타냅니다. [`number` 유형](#number) 정수 또는 부동 소수점 숫자인 모든 숫자 유형에 사용됩니다. 자세한 내용은 [숫자 유형에 대한 JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/numeric.html) 를 참조하십시오.

을 추가하여 정수 범위를 선택적으로 제한할 수 있습니다 `minimum` 및 `maximum` 속성에 값을 지정합니다. 스키마 빌더 UI에서 지원하는 몇 가지 다른 숫자 유형은 `integer` 특정 유형 `minimum` 및 `maximum` 다음과 같은 제한 [[!UICONTROL Long]](#long), [[!UICONTROL Short]](#short), 및 [[!UICONTROL 바이트]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL Long] {#long}

에 해당하는 [!UICONTROL Long] 스키마 빌더 UI를 통해 생성된 필드는 다음과 같습니다 [`integer` 유형 필드](#integer) 특정 `minimum` 및 `maximum` 값 (`-9007199254740992` 및 `9007199254740992`)를 반환합니다.

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL Short] {#short}

에 해당하는 [!UICONTROL Short] 스키마 빌더 UI를 통해 생성된 필드는 다음과 같습니다 [`integer` 유형 필드](#integer) 특정 `minimum` 및 `maximum` 값 (`-32768` 및 `32768`)를 반환합니다.

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL 바이트] {#byte}

에 해당하는 [!UICONTROL 바이트] 스키마 빌더 UI를 통해 생성된 필드는 다음과 같습니다 [`integer` 유형 필드](#integer) 특정 `minimum` 및 `maximum` 값 (`-128` 및 `128`)를 반환합니다.

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL 부울] {#boolean}

[!UICONTROL 부울] 필드는 `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

원할 경우 `default` 수집 중에 명시적 값이 제공되지 않을 때 필드가 사용할 값입니다.

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
>없는 경우 `default` 값이 제공되고 부울 필드가 `required`: 이 필드에 대해 허용된 값이 없는 레코드는 수집 시 유효성 검사가 실패합니다.

## [!UICONTROL 날짜] {#date}

[!UICONTROL 날짜] 필드는 `type: string` 및 `format: date`. 또는 선택적으로 `examples` 데이터를 수동으로 입력하는 사용자에 대한 샘플 날짜 문자열을 표시하려는 경우 를 활용하십시오.

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

[!UICONTROL DateTime] 필드는 `type: string` 및 `format: date-time`. 또는 선택적으로 `examples` 데이터를 수동으로 입력하는 사용자를 위해 샘플 datetime 문자열을 표시하려는 경우 활용하십시오.

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL 어레이] {#array}

[!UICONTROL 어레이] 필드는 `type: array` 그리고 `items` 배열이 허용할 항목의 스키마를 정의하는 개체입니다.

문자열 배열처럼 기본 유형을 사용하여 배열 항목을 정의할 수 있습니다.

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

를 참조하여 기존 데이터 유형을 기반으로 배열 항목을 정의할 수도 있습니다 `$id` 의 `$ref` 속성을 사용합니다. 다음은 [!UICONTROL 결제 항목] 개체:

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

## [!UICONTROL 오브젝트] {#object}

[!UICONTROL 개체] 필드는 `type: object` 그리고 `properties` 스키마 필드의 하위 속성을 정의하는 객체입니다.

아래에 정의된 각 하위 필드 `properties` 원시 속성을 사용하여 정의할 수 있습니다 `type` 또는 `$ref` 을 가리키는 속성 `$id` 문제의 데이터 유형:

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

해당 데이터 유형이 `type: object`:

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 맵] {#map}

지도 필드는 기본적으로 [`object`-type 필드](#object) ( 제약 없는 키 집합 사용). 물체와 마찬가지로 지도에도 `type` 값 `object`하지만, `meta:xdmType` 은 명시적으로 로 설정됩니다. `map`.

맵 **필수가 아니어야 합니다.** 속성을 정의합니다. It **반드시** 단일 정의 `additionalProperties` 맵 내에 포함된 값 유형을 설명하는 스키마입니다(각 맵에는 단일 데이터 유형만 포함할 수 있음). 다음 `type` 값은 다음 중 하나여야 합니다. `string` 또는 `integer`.

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

사용자 지정 맵 필드 만들기에 대한 자세한 내용은 아래 섹션을 참조하십시오.

### 사용자 지정 맵 유형 만들기 {#custom-maps}

XDM에서 &quot;맵 유사&quot; 데이터를 효율적으로 지원하기 위해 개체에 주석을 달 수 있습니다 `meta:xdmType` 설정 `map` 키 세트가 제약 없는 것처럼 개체를 관리해야 함을 명확히 하려면 맵 필드에 수집되는 데이터는 문자열 키, 문자열 또는 정수 값만 사용해야 합니다(결정된 대로) `additionalProperties.type`).

XDM에서는 이 저장소 힌트의 사용에 대해 다음과 같은 제한을 둡니다.

* 맵 유형은 형식이어야 합니다. `object`.
* 맵 유형에는 속성이 정의되어 있지 않아야 합니다(즉, &quot;빈&quot; 개체를 정의함).
* 맵 유형은 다음을 포함해야 합니다. `additionalProperties.type` 맵 내에 배치할 수 있는 값을 설명하는 필드입니다. `string` 또는 `integer`.

다음 성능 단점이 있으므로 반드시 필요한 경우에만 맵 유형 필드를 사용해야 합니다.

* 응답 시간 [Adobe Experience Platform 쿼리 서비스](../../query-service/home.md) 1억 개의 레코드에 대해 3초에서 10초로 등급이 저하됩니다.
* 맵에는 16개 미만의 키가 있어야 하며, 그렇지 않으면 더 큰 성능 저하가 발생할 수 있습니다.

Platform 사용자 인터페이스에는 맵 유형 필드의 키를 추출하는 방법에 대한 제한 사항도 있습니다. 객체 유형 필드를 확장할 수 있지만 맵은 대신 단일 필드로 표시됩니다.

## 다음 단계

이 안내서에서는 API에서 다른 필드 유형을 정의하는 방법을 다룹니다. XDM 필드 유형의 형식 지정 방법에 대한 자세한 내용은 안내서 를 참조하십시오 [XDM 필드 유형 제한](../schema/field-constraints.md).
