---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;필드 그룹;필드 그룹;필드 그룹;필드 그룹;데이터 유형;데이터 유형;데이터 유형;데이터 유형;스키마 디자인;데이터 유형;데이터 유형;데이터 유형;데이터 유형;스키마;스키마;스키마;스키마 디자인;맵;맵;
solution: Experience Platform
title: XDM 필드 유형 제한
description: 매핑할 수 있는 다른 일련화 형식과 API에서 고유한 필드 유형을 정의하는 방법을 포함하여 XDM(Experience Data Model)의 필드 유형 제약 조건에 대한 참조입니다.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

# XDM 필드 유형 제약 조건

XDM(경험 데이터 모델) 스키마에서 필드 유형은 필드에 포함될 수 있는 데이터 종류를 제한합니다. 이 문서에서는 매핑할 수 있는 다른 일련화 형식과 다양한 제약 조건을 적용하기 위해 API에서 고유한 필드 유형을 정의하는 방법을 포함하여 각 코어 필드 유형에 대한 개요를 제공합니다.

## 시작하기

이 안내서를 사용하기 전에 XDM 스키마, 클래스 및 스키마 필드 그룹에 대한 소개는 [스키마 컴포지션의 기본 사항](./composition.md)을 검토하십시오.

API에서 고유한 필드 유형을 정의할 계획이라면 [스키마 레지스트리 개발자 안내서](../api/getting-started.md)로 시작하여 사용자 지정 필드를 포함할 필드 그룹 및 데이터 유형을 만드는 방법을 배우는 것이 좋습니다. Experience Platform UI를 사용하여 스키마를 만드는 경우 [UI의 필드 정의](../ui/fields/overview.md)에 대한 안내서를 참조하여 사용자 지정 필드 그룹 및 데이터 형식 내에서 정의한 필드에 대한 제약 조건을 구현하는 방법에 대해 알아보십시오.

## 기본 구조 및 예 {#basic-types}

XDM은 JSON 스키마 위에 구축되므로 XDM 필드는 해당 유형을 정의할 때 유사한 구문을 상속합니다. JSON 스키마에서 다양한 필드 유형이 표현되는 방식을 이해하면 각 유형의 기본 제약 조건을 표시하는 데 도움이 될 수 있습니다. 사용자 정의 필드 이름은 대소문자를 구분하지 않으며 스키마의 동일한 수준에서 다른 이름을 가져야 합니다.

>[!NOTE]
>
>JSON 스키마 및 Experience Platform API의 기타 기본 기술에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-schema)를 참조하십시오.

다음 표에서는 해당 유형을 준수하는 예제 값과 함께 각 XDM 유형이 JSON 스키마에서 표시되는 방식을 간략하게 설명합니다.

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM 유형</th>
      <th>JSON 스키마</th>
      <th>예</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Number]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 9007199254740991,
  "minimum": -9007199254740991
&rbrace;</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL 정수]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 2147483648,
  "minimum": -2147483648
&rbrace;</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 32768,
  "minimum": -32768
&rbrace;</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "integer",
  "maximum": 128,
  "minimum": -128
&rbrace;</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL 날짜]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
&lbrace;
  "type": "string",
  "format": "date-time"
&rbrace;</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL 부울]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type": "boolean"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**날짜 형식의 모든 문자열은 ISO 8601 표준([RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6))을 준수해야 합니다.*

## XDM 유형을 다른 형식으로 매핑

아래 섹션에서는 각 XDM 유형이 다른 일반적인 직렬화 형식에 매핑되는 방법을 설명합니다.

* [Parquet, Spark SQL 및 Java](#parquet)
* [Scala, .NET 및 CosmosDB](#scala)
* [MongoDB, Aerospike 및 Protobuf 2](#mongo)

>[!NOTE]
>
>아래 표에 나열된 표준 XDM 유형 중 [!UICONTROL Map] 유형도 포함됩니다. 맵은 데이터가 특정 값에 매핑되는 키로 표시되는 경우 또는 키가 정적 스키마에 합리적으로 포함될 수 없고 데이터 값으로 처리되어야 하는 경우 표준 스키마에서 사용됩니다.
>
>대부분의 표준 XDM 구성 요소는 맵 유형을 사용하며, 원하는 경우 [사용자 지정 맵 필드를 정의](../tutorials/custom-fields-api.md#custom-maps)할 수도 있습니다. 아래 표에 맵 유형이 포함된 이유는 기존 데이터가 현재 아래에 나열된 형식으로 저장되어 있는 경우 XDM에 매핑하는 방법을 결정하는 데 도움이 되기 위한 것입니다.

### Parquet, Spark SQL 및 Java {#parquet}

| XDM 유형 | 쪽모이 세공 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 문자열] | 형식: `BYTE_ARRAY`<br>주석: `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 숫자] | 유형: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 길게] | 유형: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 정수] | 형식: `INT32`<br>주석: `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 짧음] | 형식: `INT32`<br>주석: `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 바이트] | 형식: `INT32`<br>주석: `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 날짜] | 형식: `INT32`<br>주석: `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 형식: `INT64`<br>주석: `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 부울] | 유형: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 맵] | `MAP` 주석이 있는 그룹<br><br>(`<key-type>`은(는) `STRING`이어야 합니다.) | `MapType`<br><br>(`keyType`은(는) `StringType`이어야 함) | `java.util.Map` |

{style="table-layout:auto"}

### Scala, .NET 및 CosmosDB {#scala}

| XDM 유형 | 스칼라 | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL 문자열] | `String` | `System.String` | `String` |
| [!UICONTROL 숫자] | `Double` | `System.Double` | `Number` |
| [!UICONTROL 길게] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 정수] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL 짧음] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 바이트] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 날짜] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 부울] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 맵] | `Map` | (N/A) | `object` |

{style="table-layout:auto"}

### MongoDB, Aerospike 및 Protobuf 2 {#mongo}

| XDM 유형 | 몽고DB | 에어로스파이크 | 프로토콜 버퍼 2 |
| --- | --- | --- | --- |
| [!UICONTROL 문자열] | `string` | `String` | `string` |
| [!UICONTROL 숫자] | `double` | `Double` | `double` |
| [!UICONTROL 길게] | `long` | `Integer` | `int64` |
| [!UICONTROL 정수] | `int` | `Integer` | `int32` |
| [!UICONTROL 짧음] | `int` | `Integer` | `int32` |
| [!UICONTROL 바이트] | `int` | `Integer` | `int32` |
| [!UICONTROL 날짜] | `date` | `Integer`<br>(Unix 밀리초) | `int64`<br>(Unix 밀리초) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix 밀리초) | `int64`<br>(Unix 밀리초) |
| [!UICONTROL 부울] | `bool` | `Integer`<br>(0/1 이진) | `bool` |
| [!UICONTROL 맵] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## API에서 XDM 필드 유형 정의 {#define-fields}

스키마 레지스트리 API를 사용하면 형식 및 선택적 제약 조건을 사용하여 사용자 지정 필드를 정의할 수 있습니다. 자세한 내용은 [스키마 레지스트리 API에서 사용자 지정 필드 정의](../tutorials/custom-fields-api.md)에 대한 안내서를 참조하십시오.
