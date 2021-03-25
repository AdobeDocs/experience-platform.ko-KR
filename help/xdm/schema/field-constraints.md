---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;믹신;믹싱;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;스키마 디자인;데이터 유형;데이터 유형;데이터 유형;데이터 유형;스키마;스키마;스키마 디자인;맵;맵;맵;스키마;home;publicin;mixin;mixin;data types;data;
solution: Experience Platform
title: XDM 필드 유형 제한
topic: 개요
description: 매핑할 수 있는 다른 직렬화 형식 및 API에서 고유한 필드 유형을 정의하는 방법을 포함하여, XDM(경험 데이터 모델)의 필드 유형 제약 조건에 대한 참조입니다.
translation-type: tm+mt
source-git-commit: cc1fa21df0bb2d49106775c75a0cb3c4f4d73941
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 1%

---


# XDM 필드 유형 제약 조건

XDM(Experience Data Model) 스키마에서 필드의 유형은 필드에 포함할 수 있는 데이터 종류를 제한합니다. 이 문서에서는 매핑할 수 있는 다른 일련화 형식 및 다른 제약 조건을 적용하기 위해 API에서 고유한 필드 유형을 정의하는 방법을 포함하여 각 핵심 필드 유형에 대한 개요를 제공합니다.

## 시작하기

이 안내서를 사용하기 전에 스키마 컴포지션](./composition.md)의 [기본 사항을 검토하여 XDM 스키마, 클래스 및 혼합에 대한 소개를 확인하십시오.

API에서 고유한 필드 유형을 정의할 계획인 경우 사용자 정의 필드를 포함할 믹싱 및 데이터 유형을 만드는 방법을 알려면 [스키마 레지스트리 개발자 가이드](../api/getting-started.md)로 시작하는 것이 좋습니다. Experience Platform UI를 사용하여 스키마를 만드는 경우, 사용자 정의 믹싱 및 데이터 유형 내에서 정의하는 필드에 제한을 구현하는 방법을 알아보려면 [UI](../ui/fields/overview.md)의 필드 정의 가이드를 참조하십시오.

## 기본 구조 및 예

XDM은 JSON 스키마 상단에 구축되므로 XDM 필드는 유형을 정의할 때 유사한 구문을 상속합니다. JSON 스키마에서 다양한 필드 유형이 표현되는 방식을 이해하면 각 유형의 기본 제약 조건을 나타낼 수 있습니다.

>[!NOTE]
>
>플랫폼 API의 JSON 스키마 및 기타 기본 기술에 대한 자세한 내용은 [API 기본 사항 가이드](../../landing/api-fundamentals.md#json-schema)를 참조하십시오.

다음 표에서는 각 XDM 유형이 JSON 스키마에서 해당 유형을 준수하는 예제 값과 함께 어떻게 표현되는지를 보여 줍니다.

<table>
  <thead>
    <tr>
      <th>XDM 유형</th>
      <th>JSON 스키마</th>
      <th>예</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL 문자열]</td>
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
  "최소":-9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL 정수]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type":"integer",
  "maximum":2147483648,
  "최소":-2147483648
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
  "최소":-32768
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
  "maximum":128,
  "최소":-128
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

**모든 날짜 형식 문자열은 ISO 8601 표준([RFC 339, 섹션 5.6](https://tools.ietf.org/html/rfc3339#section-5.6))을 준수해야 합니다.*

## XDM 유형을 다른 형식으로 매핑

아래 섹션에서는 각 XDM 유형이 다른 일반적인 일련화 형식에 매핑되는 방법을 설명합니다.

* [Partial, Spark SQL 및 Java](#parquet)
* [Scala, .NET 및 CosmosDB](#scala)
* [MongoDB, Aerospike 및 Protobuf 2](#mongo)

>[!IMPORTANT]
>
>아래 표에 나와 있는 표준 XDM 유형 중 [!UICONTROL Map] 유형도 포함되어 있습니다. 맵은 데이터가 특정 값에 매핑되는 키로 표현되거나, 정적 스키마에 키를 합리적으로 포함할 수 없고 데이터 값으로 처리되어야 하는 경우 표준 스키마에서 사용됩니다.
>
>맵 유형 필드는 업계 및 공급업체 스키마 사용을 위해 예약되어 있으므로 사용자가 정의하는 사용자 지정 리소스에는 사용할 수 없습니다. 아래 표에 포함된 맵 유형은 현재 XDM이 아래 나열된 형식으로 저장된 경우 기존 데이터를 XDM에 매핑하는 방법을 결정하는 데만 도움이 됩니다.

### Partial, Spark SQL 및 Java {#parquet}

| XDM 유형 | 쪽모이 세공 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | 유형:`BYTE_ARRAY`<br>주석:`UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | 유형: `DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | 유형: `INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | 유형:`INT32`<br>주석:`INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | 유형:`INT32`<br>주석:`INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | 유형:`INT32`<br>주석:`INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | 유형:`INT32`<br>주석:`DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 유형:`INT64`<br>주석:`TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | 유형: `BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-annotated group<br><br>(`<key-type>` 필수 `STRING`) | `MapType`<br><br>(`keyType` 필수 `StringType`) | `java.util.Map` |

### Scala, .NET 및 CosmosDB {#scala}

| XDM 유형 | 스칼라 | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (N/A) | `object` |

### MongoDB, Aerospike 및 Protobuf 2 {#mongo}

| XDM 유형 | MongoDB | 공기스파이크 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>(Unix 밀리초) | `int64`<br>(Unix 밀리초) |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>(Unix 밀리초) | `int64`<br>(Unix 밀리초) |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>(0/1 이진) | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

## API {#define-fields}에서 XDM 필드 유형 정의

모든 XDM 필드는 필드 유형에 적용되는 표준 [JSON 스키마](https://json-schema.org/) 제약 조건을 사용하여 정의되며 [!DNL Experience Platform]에 의해 적용되는 필드 이름에 대한 추가 제약 조건을 사용합니다. 스키마 레지스트리 API를 사용하면 형식 및 선택적 제약 조건을 사용하여 추가 필드 유형을 정의할 수 있습니다. XDM 필드 유형은 필드 수준 특성 `meta:xdmType`에 의해 노출됩니다.

>[!NOTE]
>
>`meta:xdmType` 은 시스템에서 생성된 값이므로 API를 사용할 때 해당 필드의 JSON에 이 속성을 추가할 필요가 없습니다. 아래 표에 정의된 대로 적절한 최소/최대 제약 조건과 함께 JSON 스키마 유형(예: `string` 및 `integer`)을 사용하는 것이 좋습니다.

다음 표에서는 선택적 속성이 있는 필드 유형을 포함하여 다양한 필드 유형을 정의하는 데 적합한 서식에 대해 대략적으로 설명합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/type.html)를 통해 확인할 수 있습니다.

시작하려면 원하는 필드 유형을 찾아 [mixin](../api/mixins.md#create) 또는 [데이터 유형 만들기 API 요청을 작성하기 위해 제공된 샘플 코드를 사용하십시오](../api/data-types.md#create).

<table>
  <tr>
    <th>XDM 유형</th>
    <th>선택적 속성</th>
    <th>예</th>
  </tr>
  <tr>
    <td>[!UICONTROL 문자열]</td>
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
    "패턴":"^[A-Z]{2}$",
    "maxLength":2
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
    <td>제한적 열거형 값은 <code>enum</code> 배열 아래에 제공되지만 각 값에 대한 선택적 고객 대면 레이블은 <code>meta:enum</code> 아래에 제공할 수 있습니다.
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
  "기본값":"value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL 번호]</td>
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
  "최소":-9007199254740992,
  "maximum":9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL 정수]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"integer",
  "최소":-2147483648,
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
  "최소":-32768,
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
  "최소":-128,
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
  "기본값":false
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
    <td>[!UICONTROL 배열]</td>
    <td></td>
    <td>기본 스칼라 형식(예: 문자열) 배열:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"array",
  "항목":{
    "type":"string"
  }
}</pre>
      다른 스키마로 정의된 개체 배열:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"array",
  "항목":{
    "$ref":"https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL 개체]</td>
    <td></td>
    <td><code>properties</code> 아래에 정의된 각 하위 필드의 <code>type</code> 속성은 스칼라 형식을 사용하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "속성":{
    "field1":{
      "type":"string"
    },
    "field2":{
      "type":"number"
    }
  }
}</pre>
      객체 유형 필드는 데이터 유형의 <code>$id</code>을 참조하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "$ref":"https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL 맵]</td>
    <td></td>
    <td>맵 <strong>은(는) 속성을 정의하지 않아야 합니다.</strong> 맵 내에 포함된 값 유형을 설명하는 <strong>은 단일 </strong> 스키마를 정의해야 합니다(각 맵은 단일 데이터 유형만 포함할 수 있음). <code>additionalProperties</code> 값은 유효한 XDM <code>type</code> 특성 또는 <code>$ref</code> 특성을 사용하는 다른 스키마에 대한 참조일 수 있습니다.<br/><br/>문자열 유형 값이 있는 맵 필드:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "type":"string"
  }
}</pre>
    값에 대한 문자열 배열이 있는 지도 필드:
      <pre class="JSON language-JSON hljs">
"sampleField":{
  "type":"object",
  "additionalProperties":{
    "type":"array",
    "항목":{
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

{style=&quot;table-layout:auto&quot;}
