---
keywords: Experience Platform;홈;인기 항목;스키마;필드 그룹;필드 그룹;필드 그룹;필드 그룹;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;스키마 디자인;데이터 유형;데이터 유형;데이터 유형;스키마;스키마;스키마 디자인;맵;맵;
solution: Experience Platform
title: XDM 필드 유형 제한
topic-legacy: overview
description: 매핑할 수 있는 다른 직렬화 형식 및 API에서 고유한 필드 유형을 정의하는 방법을 포함하여 XDM(Experience Data Model)의 필드 유형 제약 조건에 대한 참조입니다.
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 61025ada3a900a5bd7682e3bb7d4f6cd23347231
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 2%

---

# XDM 필드 유형 제한

XDM(Experience Data Model) 스키마에서 필드의 유형은 필드에 포함할 수 있는 데이터 종류를 제한합니다. 이 문서에서는 매핑할 수 있는 다른 직렬화 형식 및 다른 제한을 적용하기 위해 API에서 고유한 필드 유형을 정의하는 방법을 포함하여 각 코어 필드 유형에 대한 개요를 제공합니다.

## 시작하기

이 안내서를 사용하기 전에 XDM 스키마, 클래스 및 스키마 필드 그룹에 대한 소개는 스키마 구성](./composition.md)의 [기본 사항을 검토하십시오.

API에서 고유한 필드 유형을 정의할 계획이라면 [스키마 레지스트리 개발자 안내서](../api/getting-started.md)로 시작하여 사용자 지정 필드를 포함하도록 필드 그룹 및 데이터 유형을 만드는 방법을 학습하는 것이 좋습니다. Experience Platform UI를 사용하여 스키마를 만드는 경우, 사용자 지정 필드 그룹 및 데이터 유형 내에서 정의하는 필드에 대한 제한을 구현하는 방법을 알려면 UI](../ui/fields/overview.md)에서 필드 정의 안내서를 참조하십시오.[

## 기본 구조 및 예

XDM은 JSON 스키마 위에 구축되므로 XDM 필드는 해당 유형을 정의할 때 유사한 구문을 상속합니다. JSON 스키마에 다양한 필드 유형이 표시되는 방식을 이해하면 각 유형의 기본 제한을 나타내는 데 도움이 됩니다.

>[!NOTE]
>
>Platform API의 JSON 스키마 및 기타 기본 기술에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-schema)를 참조하십시오.

다음 표에서는 유형을 준수하는 예제 값과 함께 각 XDM 유형이 JSON 스키마에서 표시되는 방식을 설명합니다.

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
{"type":"string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Double]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":9007199254740991,
  "minimum":-9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":2147483648,
  "minimum":-2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":32768,
  "minimum":-32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":128년,
  "minimum":-128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL 날짜]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"string",
  "format":"date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"string",
  "format":"date-time"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**날짜 형식이 지정된 모든 문자열은 ISO 8601 표준([RFC 3339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6))을 준수해야 합니다.*

## XDM 유형을 다른 형식에 매핑

아래 섹션에서는 각 XDM 유형이 다른 일반적인 직렬화 형식에 매핑되는 방법을 설명합니다.

* [Parquet, Spark SQL 및 Java](#parquet)
* [Scala, .NET 및 CosmosDB](#scala)
* [MongoDB, Aerospak 및 Protoff 2](#mongo)

>[!IMPORTANT]
>
>아래 표에 나열된 표준 XDM 유형 중 [!UICONTROL Map] 유형도 포함됩니다. 맵은 데이터가 특정 값에 매핑되는 키로 표시되거나, 키가 정적 스키마에 합리적으로 포함할 수 없고 데이터 값으로 처리되어야 하는 경우 표준 스키마에서 사용됩니다.
>
>맵 유형 필드는 업계 및 공급업체 스키마 사용을 위해 예약되어 있으므로 정의한 사용자 정의 리소스에서 사용할 수 없습니다. 아래 표에 맵 유형의 포함은 기존 데이터가 현재 아래 나열된 형식으로 저장된 경우 XDM에 매핑하는 방법을 결정하는 데만 도움이 됩니다.

### Parquet, Spark SQL 및 Java {#parquet}

| XDM 유형 | 쪽모이 세공 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 문자열] | 유형:`BYTE_ARRAY`<br>주석:`UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 이중] | 유형: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | 유형: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 정수] | 유형:`INT32`<br>주석:`INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | 유형:`INT32`<br>주석:`INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 바이트] | 유형:`INT32`<br>주석:`INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 날짜] | 유형:`INT32`<br>주석:`DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 유형:`INT64`<br>주석:`TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 부울] | 유형: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 맵] | `MAP`-주석 처리된 그룹<br><br>(`<key-type>` 반드시  `STRING`) | `MapType`<br><br>(`keyType` 이어야  `StringType` 함) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala, .NET 및 CosmosDB {#scala}

| XDM 유형 | 스칼라 | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL 문자열] | `String` | `System.String` | `String` |
| [!UICONTROL 이중] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 정수] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 바이트] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 날짜] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 부울] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 맵] | `Map` | (N/A) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB, Aerospak 및 Protoff 2 {#mongo}

| XDM 유형 | MongoDB | 에어로스파이크 | 프로토부프 2 |
| --- | --- | --- | --- |
| [!UICONTROL 문자열] | `string` | `String` | `string` |
| [!UICONTROL 이중] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL 정수] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL 바이트] | `int` | `Integer` | `int32` |
| [!UICONTROL 날짜] | `date` | `Integer`<br>(Unix 밀리초) | `int64`<br>(Unix 밀리초) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix 밀리초) | `int64`<br>(Unix 밀리초) |
| [!UICONTROL 부울] | `bool` | `Integer`<br>(0/1 이진) | `bool` |
| [!UICONTROL 맵] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## API {#define-fields}에서 XDM 필드 유형 정의

모든 XDM 필드는 해당 필드 유형에 적용되는 표준 [JSON 스키마](https://json-schema.org/) 제약 조건을 사용하여 정의되며, [!DNL Experience Platform]에 의해 적용되는 필드 이름에 대한 추가 제한 사항이 있습니다. 스키마 레지스트리 API를 사용하면 형식 및 선택적 제약 조건을 사용하여 추가 필드 유형을 정의할 수 있습니다. XDM 필드 유형은 필드 수준 속성인 `meta:xdmType`에 의해 노출됩니다.

>[!NOTE]
>
>`meta:xdmType` 는 시스템에서 생성한 값이므로 API를 사용할 때 필드의 JSON에 이 속성을 추가할 필요가 없습니다. 모범 사례는 아래 표에 정의된 대로 적절한 최소/최대 제약 조건과 함께 JSON 스키마 유형(예: `string` 및 `integer`)을 사용하는 것입니다.

다음 표에서는 선택적 속성이 있는 필드 유형을 포함하여 다른 필드 유형을 정의하는 데 적합한 형식에 대해 설명합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/type.html)를 참조하십시오.

시작하려면 원하는 필드 유형을 찾고 [필드 그룹 만들기](../api/field-groups.md#create) 또는 [데이터 유형 만들기](../api/data-types.md#create)에 대한 API 요청을 작성하는 데 제공된 샘플 코드를 사용하십시오.

<table style="table-layout:auto">
  <tr>
    <th>XDM 유형</th>
    <th>선택적 속성</th>
    <th>예</th>
  </tr>
  <tr>
    <td>[!UICONTROL String]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
    "type":"string",
    "pattern":"^[A-Z]{2}$",
    "maxLength":2개
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "format":"uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>제약 있는 열거형 값은 <code>enum</code> 배열 아래에 제공되지만, 각 값에 대한 선택적 고객 대면 레이블은 <code>meta:enum</code> 아래에 제공할 수 있습니다.
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "enum":[
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum":{
      "value1":"값 1",
      "value2":"값 2",
      "value3":"값 3"
  },
  "default":"value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  "minimum":-9007199254740992,
  "maximum":9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  "minimum":-2147483648,
  "maximum":2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  "minimum":-32768,
  "maximum":32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  "minimum":-128,
  "maximum":128년
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Boolean]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"boolean",
  "default":false
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL 날짜]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "format":"date",
  "예":["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"string",
  "format":"date-time",
  "예":["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>기본 스칼라 형식(예: 문자열)의 배열입니다.
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"array",
  "items":{
    "type":"string"
  }
}</pre>
      다른 스키마에 의해 정의된 개체 배열:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"array",
  "items":{
    "$ref":"https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td><code>properties</code> 아래에 정의된 각 하위 필드의 <code>type</code> 속성은 스칼라 유형을 사용하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "properties":{
    "field1":{
      "type":"string"
    },
    "field2":{
      "type":"number"
    }
  }
}</pre>
      개체 유형 필드는 데이터 형식의 <code>$id</code> 을 참조하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "$ref":"https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>맵 <strong>은(는) </strong>에서 속성을 정의하지 않아야 합니다. 이 <strong>은(는) 맵에 포함된 값 유형을 설명하는 단일 <code>additionalProperties</code> 스키마를 정의해야 합니다(각 맵은 단일 데이터 유형만 포함할 수 있음). </strong> 값은 모든 유효한 XDM <code>type</code> 속성이거나 <code>$ref</code> 속성을 사용하는 다른 스키마에 대한 참조일 수 있습니다.<br/><br/>문자열 유형 값이 있는 맵 필드:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "type":"string"
  }
}</pre>
    값에 대한 문자열 배열이 있는 맵 필드:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "type":"array",
    "items":{
      "type":"string"
    }
  }
}</pre>
    다른 데이터 유형을 참조하는 맵 필드:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "$ref":"https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>
