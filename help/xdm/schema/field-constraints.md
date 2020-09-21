---
keywords: Experience Platform;home;popular topics;schema;Schema;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;schema design;datatype;Datatype;data type;Data type;schemas;Schemas;Schema design;map;Map;
solution: Experience Platform
title: XDM 필드 유형 제한
topic: overview
description: 매핑할 수 있는 다른 직렬화 형식 및 API에서 고유한 필드 유형을 정의하는 방법을 포함한 XDM 필드 유형 제약 조건에 대한 참조입니다.
translation-type: tm+mt
source-git-commit: 19167f58fae6fac7d938deb74182d2e19960beb3
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# XDM 필드 유형 제한

스키마에 대해 선택하는 XDM 필드 유형은 해당 필드에 포함할 수 있는 데이터 종류를 제한합니다. 이 문서에서는 매핑할 수 있는 다른 일련화 형식 및 다른 제한 사항을 적용하기 위해 API에서 고유한 필드 유형을 정의하는 방법을 포함하여 각 핵심 필드 유형에 대한 개요를 제공합니다.

## 시작하기

이 안내서를 사용하기 전에 스키마 구성 [](./composition.md) 기본 사항을 검토하여 XDM 스키마, 클래스 및 믹스에 대한 소개를 참조하십시오.

고유한 필드 유형을 정의할 계획인 경우 [스키마 레지스트리 개발자 가이드로](../api/getting-started.md) 시작하여 사용자 정의 필드를 포함할 혼합이나 데이터 유형을 만드는 방법을 배우는 것이 좋습니다.

## XDM 유형을 다른 포맷으로 매핑

아래 표에서는 각 XDM 유형(`meta:xdmType`)과 다른 직렬화 형식 간의 매핑을 설명합니다.

| XDM 유형<br>(meta:xdmType) | JSON<br>(JSON 스키마) | 쪽모이<br>세공(문자/주석) | [!DNL Spark] SQL | Java | Scala | .NET | CosmosDB | MongoDB | 공기 스파이크 | 프로토타입 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | 문자열 | System.String | 문자열 | string | 문자열 | string |
| number | type:number | DOUBLE | DoubleType | java.lang.Double | 이중 | System.Double | 숫자 | 이중 | 이중 | 이중 |
| long | type:<br>integermaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | 숫자 | long | 정수 | int64 |
| int | type:<br>integermaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | 정수 유형 | java.lang.Integer | Int | System.Int32 | 숫자 | int | 정수 | int32 |
| short | type:<br>integermaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Short | System.Int16 | 숫자 | int | 정수 | int32 |
| byte | type:<br>integermaximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | 바이트 | System.SByte | 숫자 | int | 정수 | int32 |
| 부울 | type:boolean | 부울 | BooleanType | java.lang.Boolean | 부울 | System.Boolean | 부울 | 보올 | 정수 | 정수 | 보올 |
| 날짜 | type:<br>stringformat:date<br>(RFC 339, section 5.6) | INT32/날짜 | DateType | java.util.Date | java.util.Date | System.DateTime | 문자열 | 날짜 | 정수<br>(unix 밀리) | int64<br>(unix millis) |
| date-time | type:<br>stringformat:date-time<br>(RFC 339, section 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | 문자열 | timestamp | 정수<br>(unix 밀리) | int64<br>(unix millis) |
| 지도 | 개체 | MAP 주석 그룹<br><br>&lt;<span>key_type</span>>은 맵 값의 STRING<br><br>&lt;<span>value_type</span>> 유형이어야 합니다. | MapType<br><br>&quot;keyType&quot;은 맵 값의<br><br>유형입니다. | java.util.Map | 맵 | --- | 개체 | 개체 | 지도 | map&lt;<span>key_type, value_type</span>> |

## API에서 XDM 필드 유형 정의

XDM 스키마는 [JSON 스키마](https://json-schema.org/) 표준 및 기본 필드 유형을 사용하여 정의되며, 필드 이름에 대한 추가 제한 사항은 [!DNL Experience Platform]다음과 같습니다. 스키마 [레지스트리 API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) 사용하면 형식 및 선택적 제약 조건을 사용하여 추가 필드 유형을 정의할 수 있습니다. XDM 필드 유형은 필드 수준 속성으로 노출됩니다 `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 은 시스템에서 생성된 값이므로 필드의 JSON에 이 속성을 추가할 필요가 없습니다. 아래 표에 정의된 대로 적절한 최소/최대 제약 조건과 함께 JSON 스키마 유형(문자열 및 정수 등)을 사용하는 것이 좋습니다.

다음 표에서는 선택적 속성을 사용하여 스칼라 필드 형식과 더 구체적인 필드 유형을 정의하는 적절한 서식 개요를 제공합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서를 참조하십시오](https://json-schema.org/understanding-json-schema/reference/type.html).

시작하려면 원하는 필드 유형을 찾아 제공된 샘플 코드를 사용하여 믹스를 [만들거나 데이터 유형을](../api/create-mixin.md) 만들기 위한 API 요청을 [작성합니다](../api/create-data-type.md).

<table>
  <tr>
    <th>원하는 유형<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON 스키마)</th>
    <th>코드 샘플</th>
  </tr>
  <tr>
    <td>string</td>
    <td>type:<br/><br/><strong>string선택적 속성:</strong><br/>
      <ul>
        <li>패턴</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "pattern":"^[A-Z]{2}$", "maxLength":2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type:<br/>문자열 형식:uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "format":"uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType:문자열)</td>
    <td>type:string<br/><br/><strong>Optional 속성:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>"meta:enum"을 사용하여 고객 대면 옵션 레이블을 지정합니다.
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "enum":["value1", "value2", "value3" ], "meta:enum":{ "value1":"Value 1", "value2":"Value 2", "value3":"Value 3" }, "default":"value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>number</td>
    <td>type:최소<br/>번호:랴그랴 현재 최대 2.23 × 10^308<br/>입니다.랴그아 1.80 × 10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type:<br/>integermaximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-9007199254740992, "최대":9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type:<br/>integermaximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-2147483648, "maximum":2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type:<br/>integermaximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-32768, "최대":32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type:<br/>integermaximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-128, "최대":128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>부울</td>
    <td><br/>type:boolean<br/>{true, false}<br/><br/><strong>Optional 속성:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"boolean", "default":false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>날짜</td>
    <td>type:<br/>문자열 형식:date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "format":"date", "examples":["2004-10-23"] }
      </pre>
      RFC 3339, <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">조항 5.6</a>, 여기서 "full-date" = date-fullyear "-" date-month "-" date-mday (YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type:<br/>문자열 형식:date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "format":"date-time", "examples":["2004-10-23T12:00:00-06:00"] }
      </pre>
      RFC 3339 <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">에 의해 정의된 날짜-시간, 조항 5.6</a>, 여기서 "date-time" = full-date "T" full-time:<br/>(YYY-MM-DD'T'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>배열</td>
    <td>type:배열</td>
    <td>items.type은 스칼라 형식을 사용하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"array", "items":{ "type":"string" } }
      </pre>
      다른 스키마로 정의된 개체 배열:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"array", "items":{ "$ref":"id" } }
      </pre>
      여기서 "id"는 참조 스키마의 {id}입니다.
    </td>
  </tr>
  <tr>
    <td>개체</td>
    <td>type:개체</td>
    <td>액세스해야 합니다.{field}.type은 스칼라 형식을 사용하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "properties":{ "field1":{ "type":"string" }, "field2":{ "type":"number" } } }
      </pre>
      참조 스키마로 정의된 "object" 유형의 필드:
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "$ref":"id" }
      </pre>
      여기서 "id"는 참조 스키마의 {id}입니다.
    </td>
  </tr>
  <tr>
    <td>지도</td>
    <td>type:<br/><br/><strong>objectNote:</strong><br/>'map' 데이터 유형의 사용은 업계 및 공급업체 스키마 사용을 위해 예약되어 테넌트 정의 필드에 사용할 수 없습니다. 데이터가 일부 값에 매핑되는 키로 표현되거나, 정적 스키마에 키를 합리적으로 포함할 수 없고 데이터 값으로 처리되어야 하는 경우 표준 스키마에 사용됩니다.</td>
    <td>'map'은 속성을 정의하지 않아야 합니다. 'map'에 포함된 값 유형을 설명하려면 단일 "[!UICONTROL additionalProperties]" 스키마를 정의해야 합니다. XDM의 'map'은 단일 데이터 유형만 포함할 수 있습니다. 값은 배열 또는 개체를 포함한 유효한 XDM 스키마 정의이거나 다른 스키마에 대한 참조일 수 있습니다($ref 사용).<br/><br/>'string' 유형의 값이 있는 맵 필드:
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "additionalProperties":{ "type":"string" } }
      </pre>
    값이 문자열 배열인 필드 매핑:
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "additionalProperties":{ "type":"array", "items":{ "type":"string" } } }
      </pre>
    다른 스키마를 참조하는 맵 필드:
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "additionalProperties":{ "$ref":"id" } }
      </pre>
      여기서 "id"는 참조 스키마의 {id}입니다.
    </td>
  </tr>
</table>
