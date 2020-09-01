---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: 스키마 레지스트리 개발자 부록
description: 이 문서에서는 스키마 레지스트리 API 작업과 관련된 보충 정보를 제공합니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 4%

---


# 부록

이 문서에서는 [!DNL Schema Registry] API 작업과 관련된 추가 정보를 제공합니다.

## 호환성 모드

[!DNL Experience Data Model] (XDM)은 디지털 경험의 상호 운용성, 풍부한 표현 능력 및 성능을 개선하기 위해 Adobe을 기반으로 공개적으로 문서화된 사양입니다. Adobe은 GitHub의 [오픈 소스 프로젝트에서 소스 코드와 공식 XDM 정의를 유지 관리합니다](https://github.com/adobe/xdm/). 이러한 정의는 XDM 스키마를 정의하는 문법으로 JSON-LD(JavaScript Object Notation for Linked Data) 및 JSON 스키마를 사용하여 XDM 표준 표기법으로 작성됩니다.

공용 저장소에서 공식 XDM 정의를 살펴보면 표준 XDM이 Adobe Experience Platform에 있는 내용과 다른 것을 확인할 수 있습니다. 호환성 모드 [!DNL Experience Platform] 에서 볼 수 있는 것은 표준 XDM과 표준 XDM을 사용하는 방법 간의 간단한 매핑을 제공하는 [!DNL Platform]것입니다.

### 호환성 모드 작동 방식

호환성 모드를 사용하면 XDM JSON-LD 모델이 표준 XDM 내의 값을 변경하여 기존 데이터 인프라와 연동하고 의미론도 동일하게 유지할 수 있습니다. 중첩된 JSON 구조를 사용하여 트리 형식의 스키마를 표시합니다.

표준 XDM과 호환성 모드 간의 주요 차이점은 필드 이름에 대한 &quot;xdm:&quot; 접두어가 제거된다는 것입니다.

다음은 표준 XDM과 호환성 모드 모두에서 생일 관련 필드(&quot;description&quot; 속성이 제거됨)를 보여주는 나란히 비교입니다. 호환성 모드 필드에는 &quot;meta:xdmField&quot; 및 &quot;meta:xdmType&quot; 속성에 XDM 필드 및 해당 데이터 유형에 대한 참조가 포함되어 있습니다.

<table>
  <th>표준 XDM</th>
  <th>호환성 모드</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:birthDate":{ "title":"생년월일", "유형":"string", "format":"date", }, "xdm:birthDayAndMonth":{ "title":"생년월일", "유형":"string", "pattern":"[0-1][0-9]-[0-9][0-9]", }, "xdm:birthYear":{ "title":"생년월일", "유형":"integer", "minimum":1, "최대":32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "birthDate":{ "title":"생년월일", "유형":"string", "format":"date", "meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":"생년월일", "유형":"string", "pattern":"[0-1][0-9]-[0-9][0-9]", "meta:xdmField":"xdm:birthDayAndMonth", "meta:xdmType":"string" }, "birthYear":{ "title":"생년월일", "유형":"integer", "minimum":1, "최대":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 호환성 모드가 필요한 이유는 무엇입니까?

Adobe Experience Platform은 기술적 문제와 제한 사항을 가진 다양한 솔루션 및 서비스를 사용하도록 설계되었습니다(예: 특정 기술이 특수 문자를 처리하는 방법). 이러한 제한 사항을 극복하기 위해 호환성 모드가 개발되었습니다.

표준 XDM [!DNL Experience Platform] 을 [!DNL Catalog]대신하여, [!DNL Data Lake]및 [!DNL Real-time Customer Profile] [!DNL Compatibility Mode] 사용하는 대부분의 서비스 API는 [!DNL Schema Registry] 또한 사용하고 이 문서의 [!DNL Compatibility Mode]예는 모두 를 사용하여 표시됩니다 [!DNL Compatibility Mode].

표준 XDM과 표준 XDM의 운영 방식 사이에서 매핑이 이루어지는 것은 [!DNL Experience Platform]유용하지만 [!DNL Platform] 서비스 사용에 영향을 미치지 않습니다.

오픈 소스 프로젝트를 사용할 수 있지만, 를 통해 리소스와 상호 작용하는 경우 이 문서의 API 예는 알고 따라야 하는 우수 사례를 [!DNL Schema Registry]제공합니다.

## API에서 XDM 필드 유형 정의 {#field-types}

XDM 스키마는 JSON 스키마 표준 및 기본 필드 유형을 사용하여 정의되며, 필드 이름에 대한 추가 제한 사항은 에서 [!DNL Experience Platform]적용됩니다. XDM을 사용하면 형식 및 선택적 제약 조건을 사용하여 추가 필드 유형을 정의할 수 있습니다. XDM 필드 유형은 필드 수준 속성으로 노출됩니다 `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 은 시스템에서 생성된 값이므로 필드의 JSON에 이 속성을 추가할 필요가 없습니다. 아래 표에 정의된 대로 적절한 최소/최대 제약 조건과 함께 JSON 스키마 유형(문자열 및 정수 등)을 사용하는 것이 좋습니다.

다음 표에서는 선택적 속성을 사용하여 스칼라 필드 형식과 더 구체적인 필드 유형을 정의하는 적절한 서식 개요를 제공합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서를 참조하십시오](https://json-schema.org/understanding-json-schema/reference/type.html).

시작하려면 원하는 필드 유형을 찾아 제공된 샘플 코드를 사용하여 API 요청을 작성합니다.

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


## XDM 유형을 다른 포맷으로 매핑

아래 표에서는 &quot;meta:xdmType&quot;과 다른 직렬화 형식 간의 매핑을 설명합니다.

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
