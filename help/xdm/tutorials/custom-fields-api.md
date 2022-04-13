---
title: 스키마 레지스트리 API에서 XDM 필드 정의
description: 스키마 레지스트리 API에서 사용자 지정 XDM(Experience Data Model) 리소스를 만들 때 다양한 필드를 정의하는 방법을 알아봅니다.
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# 스키마 레지스트리 API에서 XDM 필드 정의

모든 XDM(경험 데이터 모델) 필드는 표준을 사용하여 정의됩니다 [JSON 스키마](https://json-schema.org/) 필드 유형에 적용되는 제한 조건 및 Adobe Experience Platform에 의해 적용되는 필드 이름에 대한 추가 제한. 스키마 레지스트리 API를 사용하면 형식 및 선택적 제약 조건을 사용하여 스키마에서 사용자 지정 필드를 정의할 수 있습니다. XDM 필드 유형은 필드 수준 특성에 의해 노출됩니다. `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 는 시스템에서 생성한 값이므로 API를 사용할 때(단, [사용자 지정 맵 유형 만들기](#maps)). 가장 좋은 방법은 JSON 스키마 유형(예: `string` 및 `integer`)을 클릭하여 아래 표에 정의된 대로 적절한 최소/최대 제한을 지정합니다.

다음 표에서는 선택적 속성이 있는 필드 유형을 포함하여 다른 필드 유형을 정의하는 데 적합한 형식에 대해 설명합니다. 선택적 속성 및 유형별 키워드에 대한 자세한 내용은 [JSON 스키마 설명서](https://json-schema.org/understanding-json-schema/reference/type.html).

시작하려면 원하는 필드 유형을 찾아 제공된 샘플 코드를 사용하여 API 요청을 작성합니다 [필드 그룹 만들기](../api/field-groups.md#create) 또는 [데이터 유형 만들기](../api/data-types.md#create).

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
"sampleField": { "type": "string", "pattern": "^[A-Z]{2}$", "maxLength": 2 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "uri" }</pre>
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
    <td>제약 있는 열거형 값은 <code>enum</code> 배열이지만 각 값에 대한 선택적 고객 대상 레이블은 <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "enum": ["value1", "value2", "value3" ], "meta:enum": { "value1": "값 1", "값2": "값 2", "value3": "Value 3" }, "default": "value1" }</pre>
    <br>다음 사항에 유의하십시오. <code>meta:enum</code> 값은 <strong>not</strong> 열거형을 선언하거나 데이터 유효성 검사를 직접 구동합니다. 대부분의 경우 <code>meta:enum</code> 다음 항목에서도 제공됩니다. <code>enum</code> 가 있어야 합니다. 그러나 다음과 같은 몇 가지 사용 사례가 있습니다 <code>meta:enum</code> 이(가) 해당 없이 제공됩니다 <code>enum</code> 배열입니다. 다음에서 자습서를 참조하십시오. <a href="../tutorials/suggested-values.md">추천 값 정의</a> 추가 정보.
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "number" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -9007199254740992, "최대값": 9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Integer]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -2147483648, "최대값": 2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -32768, "최대값": 32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "integer", "minimum": -128, "최대값": 128 }</pre>
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
"sampleField": { "type": "boolean", "default": false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL 날짜]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date", "example": ["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "string", "format": "date time", "example": ["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>기본 스칼라 형식(예: 문자열)의 배열입니다.
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "type": "string" }</pre>
      다른 스키마에 의해 정의된 개체 배열:<br/>
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "array", "items": { "$ref": "https://ns.adobe.com/xdm/data/paymentitem" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Object]</td>
    <td></td>
    <td>다음 <code>type</code> 아래에 정의된 각 하위 필드의 속성 <code>properties</code> 스칼라 형식을 사용하여 정의할 수 있습니다.
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "properties": { "field1": { "type": "string" }, "field2": { "type": "number" } }</pre>
      개체 유형 필드는 <code>$id</code> 데이터 유형:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Map]</td>
    <td></td>
    <td>맵 유형 필드는 기본적으로 제약 없는 키 세트가 있는 객체 유형 필드입니다. 물체와 마찬가지로 지도에도 <code>type</code> 값 <code>object</code>하지만, <code>meta:xdmType</code> 은 명시적으로 로 설정됩니다. <code>map</code>.<br><br>맵 <strong>필수가 아니어야 합니다.</strong> 속성을 정의합니다. It <strong>반드시</strong> 단일 정의 <code>additionalProperties</code> 맵 내에 포함된 값 유형을 설명하는 스키마입니다(각 맵에는 단일 데이터 유형만 포함할 수 있음). 다음 <code>type</code> 값은 다음 중 하나여야 합니다. <code>string</code> 또는 <code>integer</code>.<br/><br/>문자열 유형 값이 있는 맵 필드:
      <pre class="JSON language-JSON hljs">
"sampleField": { "type": "object", "meta:xdmType": "map", "additionalProperties":{ "type": "string" }</pre>
    XDM에서 사용자 지정 맵 유형을 만드는 방법에 대한 자세한 내용은 아래 섹션을 참조하십시오.
    </td>
  </tr>
</table>

## 사용자 지정 맵 유형 만들기 {#maps}

XDM에서 &quot;맵 유사&quot; 데이터를 효율적으로 지원하기 위해 개체에 주석을 달 수 있습니다 `meta:xdmType` 설정 `map` 키 세트가 제약 없는 것처럼 개체를 관리해야 함을 명확히 하려면 맵 필드에 수집되는 데이터는 문자열 키, 문자열 또는 정수 값만 사용해야 합니다(결정된 대로) `additionalProperties.type`).

XDM에서는 이 저장소 힌트의 사용에 대해 다음과 같은 제한을 둡니다.

* 맵 유형은 형식이어야 합니다. `object`.
* 맵 유형에는 속성이 정의되어 있지 않아야 합니다(즉, &quot;빈&quot; 개체를 정의함).
* 맵 유형은 다음을 포함해야 합니다. `additionalProperties.type` 맵 내에 배치할 수 있는 값을 설명하는 필드입니다. `string` 또는 `integer`.

다음 성능 단점이 있으므로 반드시 필요한 경우에만 맵 유형 필드를 사용해야 합니다.

* Adobe Experience Platform 쿼리 서비스의 응답 시간은 1억 개의 레코드에 대해 3초에서 10초로 줄어듭니다.
* 맵에는 16개 미만의 키가 있어야 하며, 그렇지 않으면 더 큰 성능 저하가 발생할 수 있습니다.

Platform 사용자 인터페이스에는 맵 유형 필드의 키를 추출하는 방법에 대한 제한 사항도 있습니다. 객체 유형 필드를 확장할 수 있지만 맵은 대신 단일 필드로 표시됩니다.

## 다음 단계

이 안내서에서는 API에서 다른 필드 유형을 정의하는 방법을 다룹니다. XDM 필드 유형의 형식 지정 방법에 대한 자세한 내용은 안내서 를 참조하십시오 [XDM 필드 유형 제한](../schema/field-constraints.md).
