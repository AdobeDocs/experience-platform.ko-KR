---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;믹신;믹싱;데이터 유형;데이터 유형;데이터 유형;데이터 유형;데이터 유형;스키마 디자인;데이터 유형;데이터 유형;데이터 유형;데이터 유형;스키마;스키마;스키마 디자인;맵;맵;맵;스키마;home;publicin;mixin;mixin;data types;data;
solution: Experience Platform
title: XDM 필드 유형 제한
topic: overview
description: 매핑할 수 있는 다른 직렬화 형식 및 API에서 고유한 필드 유형을 정의하는 방법을 포함한 XDM 필드 유형 제약 조건에 대한 참조입니다.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 5%

---


# XDM 필드 유형 제약 조건

스키마에 대해 선택하는 XDM 필드 유형은 해당 필드에 포함할 수 있는 데이터 종류를 제한합니다. 이 문서에서는 매핑할 수 있는 다른 일련화 형식 및 다른 제한 조건을 적용하기 위해 API에서 고유한 필드 유형을 정의하는 방법을 포함하여 각 핵심 필드 유형에 대한 개요를 제공합니다.

## 시작하기

이 안내서를 사용하기 전에 스키마 컴포지션](./composition.md)의 [기본 사항을 검토하여 XDM 스키마, 클래스 및 혼합에 대한 소개를 확인하십시오.

고유한 필드 유형을 정의할 계획인 경우 [스키마 레지스트리 개발자 가이드](../api/getting-started.md)로 시작하여 사용자 정의 필드를 포함할 혼합과 데이터 유형을 만드는 방법을 학습하는 것이 좋습니다.

## XDM 유형을 다른 형식으로 매핑

아래 표에서는 각 XDM 유형(`meta:xdmType`)과 다른 직렬화 형식 간의 매핑을 설명합니다.

| XDM 유형<br>(meta:xdmType) | JSON<br>(JSON 스키마) | Parentheet<br>(type/annotation) | [!DNL Spark] SQL | Java | 스칼라 | .NET | CosmosDB | MongoDB | 공기스파이크 | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| string | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | 문자열 | System.String | 문자열 | 문자열 | 문자열 | 문자열 |
| number | 문자:숫자 | DOUBLE | DoubleType | java.lang.Double | 이중 | System.Double | 숫자 | 이중 | 이중 | 이중 |
| long | type:integer<br>최대값:2^53+1<br>최소값:-2^53+1 | INT64 | LongType | java.lang.Long | Long | System.Int64 | 숫자 | long | 정수 | int64 |
| int | type:integer<br>maximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | 숫자 | int | 정수 | int32 |
| short | type:integer<br>maximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | Short | System.Int16 | 숫자 | int | 정수 | int32 |
| byte | type:integer<br>maximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | 바이트 | System.SByte | 숫자 | int | 정수 | int32 |
| 부울 | type:boolean | 부울 | BooleanType | java.lang.Boolean | 부울 | System.Boolean | 부울 | 보올 | 정수 | 정수 | 보올 |
| 날짜 | type:string<br>format:date<br>(RFC 3339, 섹션 5.6) | INT32/날짜 | DateType | java.util.Date | java.util.Date | System.DateTime | 문자열 | 날짜 | 정수<br>(unix 밀리) | int64<br>(unix millis) |
| date-time | type:string<br>format:date-time<br>(RFC 3339, 섹션 5.6) | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | 문자열 | timestamp | 정수<br>(unix 밀리) | int64<br>(unix millis) |
| 지도 | 개체 | 맵 주석 그룹<br><br>&lt;<span>key_type</span>> MUST STRING<br><br>&lt;<span>value_type</span> 맵 값 유형 | MapType<br><br>&quot;keyType&quot;은 맵 값의 유형입니다.<br><br> | java.util.Map | 맵 | — | 개체 | 개체 | 지도 | map&lt;<span>key_type, value_type</span>> |

## API {#define-fields}에서 XDM 필드 유형 정의

XDM 스키마는 [JSON 스키마](https://json-schema.org/) 표준 및 기본 필드 유형을 사용하여 정의되며, [!DNL Experience Platform]에 의해 수행되는 필드 이름에 대한 추가 제약 조건이 있습니다. [스키마 레지스트리 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)에서는 형식 및 선택적 제약 조건을 사용하여 추가 필드 유형을 정의할 수 있습니다. XDM 필드 유형은 필드 수준 특성 `meta:xdmType`에 의해 노출됩니다.

>[!NOTE]
>
>`meta:xdmType` 은 시스템에서 생성된 값이므로 해당 필드의 JSON에 이 속성을 추가할 필요가 없습니다. 아래 표에 정의된 대로 적절한 최소/최대 제약 조건과 함께 JSON 스키마 유형(예: 문자열 및 정수)을 사용하는 것이 좋습니다.

다음 표에서는 선택적 속성을 사용하여 스칼라 필드 유형과 보다 구체적인 필드 유형을 정의하는 적절한 서식에 대해 대략적으로 설명합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/type.html)를 통해 확인할 수 있습니다.

시작하려면 원하는 필드 유형을 찾아 [mixin](../api/mixins.md#create) 또는 [데이터 유형 만들기 API 요청을 작성하기 위해 제공된 샘플 코드를 사용하십시오](../api/data-types.md#create).

<table>
  <tr>
    <th>원하는 유형<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON 스키마)</th>
    <th>코드 샘플</th>
  </tr>
  <tr>
    <td>문자열</td>
    <td>type:string<br/><br/><strong>선택적 속성:</strong><br/>
      <ul>
        <li>패턴</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
            "type":"string",
            "패턴":"^[A-Z]{2}$",
            "maxLength":2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type:string<br/>형식:uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"string",
          "format":"uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType:문자열)</td>
    <td>type:string<br/><br/><strong>선택적 속성:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>"meta:enum"을 사용하여 고객을 대면하는 옵션 레이블을 지정합니다.
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
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>number</td>
    <td>type:숫자<br/>최소:magazine 2.23×10^308<br/>최대:magazine 1.80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>long</td>
    <td>type:정수<br/>최대값:2^53+1<br>최소값:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"integer",
          "최소":-9007199254740992,
          "maximum":9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type:정수<br/>최대값:2^31<br>최소값:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"integer",
          "최소":-2147483648,
          "maximum":2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>short</td>
    <td>type:정수<br/>최대값:2^15<br>최소값:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"integer",
          "최소":-32768,
          "maximum":32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>byte</td>
    <td>type:정수<br/>최대값:2^7<br>최소값:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"integer",
          "최소":-128,
          "maximum":128년
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>부울</td>
    <td><br/>type:boolean<br/>{true, false}<br/><br/><strong>선택적 속성:</strong><br/>
      <ul>
        <li>default</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"boolean",
          "기본값":false
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>날짜</td>
    <td>type:string<br/>형식:date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"string",
          "format":"date",
          "예":["2004-10-23"]
        }
      </pre>
      <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 339, 5.6</a>에 의해 정의된 날짜. 여기서 "full-date" = date-fullyear "-" date-month "-" date-mday (YYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type:string<br/>형식:date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"string",
          "format":"date-time",
          "예":["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 339, 5.6</a>에 의해 정의된 날짜-시간. 여기서 "date-time" = full-date "T" full-time:<br/>(YYYY-MM-DD'T'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>array</td>
    <td>type:array</td>
    <td>items.type은 스칼라 형식을 사용하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"array",
          "항목":{
            "type":"string"
          }
        }
      </pre>
      다른 스키마에서 정의된 개체 배열:<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"array",
          "항목":{
            "$ref":"id"
          }
        }
      </pre>
      여기서 "id"는 참조 스키마의 {id}입니다.
    </td>
  </tr>
  <tr>
    <td>개체</td>
    <td>type:개체</td>
    <td>액세스해야 합니다.{field}.type은 임의의 스칼라 유형을 사용하여 정의할 수 있습니다.
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
        }
      </pre>
      참조 스키마로 정의된 "object" 유형의 필드:
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"object",
          "$ref":"id"
        }
      </pre>
      여기서 "id"는 참조 스키마의 {id}입니다.
    </td>
  </tr>
  <tr>
    <td>지도</td>
    <td>type:개체<br/><br/><strong>참고:</strong><br/>'map' 데이터 유형의 사용은 업계 및 공급업체 스키마 사용을 위해 예약되었으며 임차인 정의 필드에서 사용할 수 없습니다. 데이터가 특정 값에 매핑되는 키로 표현되거나, 정적 스키마에 키를 합리적으로 포함할 수 없고 데이터 값으로 처리되어야 하는 경우 표준 스키마에 사용됩니다.</td>
    <td>'맵'은 속성을 정의하지 않아야 합니다. 'map'에 포함된 값 유형을 설명하는 단일 "[!UICONTROL additionalProperties]" 스키마를 정의해야 합니다. XDM의 'map'은 단일 데이터 유형만 포함할 수 있습니다. 값은 배열 또는 개체를 포함한 유효한 XDM 스키마 정의이거나 다른 스키마에 대한 참조일 수 있습니다($ref 사용).<br/><br/>'string' 유형의 값이 있는 맵 필드:
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"object",
          "additionalProperties":{
            "type":"string"
          }
        }
      </pre>
    문자열 배열인 값이 있는 필드 매핑:
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"object",
          "additionalProperties":{
            "type":"array",
            "항목":{
              "type":"string"
            }
          }
        }
      </pre>
    다른 스키마를 참조하는 맵 필드:
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          "type":"object",
          "additionalProperties":{
            "$ref":"id"
          }
        }
      </pre>
      여기서 "id"는 참조 스키마의 {id}입니다.
    </td>
  </tr>
</table>
