---
title: Reactor API에서 응답 필터링
description: Reactor API에서 리소스를 나열할 때 결과를 필터링하는 방법을 알아봅니다.
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Reactor API에서 응답 필터링

Reactor API에서 목록(GET) 끝점을 사용하는 경우 반환된 결과를 레코드의 하위 집합으로 제한해야 할 수도 있습니다. 이를 위해 많은 API의 목록 종단점이 특정 속성별로 필터링하는 기능을 지원합니다. 대신 API에 구조화된 쿼리를 만들려면 다음에 대한 안내서를 참조하십시오 [검색](./search.md).

## 필터링 구문

다음 예에서는 GET 요청에 대한 필터를 구현하는 방법을 설명합니다.

**API 형식**

지정된 목록 끝점에 대한 응답을 필터링하려면 `filter` 요청 경로의 쿼리 매개 변수입니다.

>[!NOTE]
>
>아래 템플릿은 대괄호(`[]`가독성을 위해 ) 및 공백 문자를 사용할 수 있습니다. 실제로 이러한 문자는 다음과 같이 URI로 인코딩해야 합니다. [RFC 3986](https://tools.ietf.org/html/rfc3986). 올바르게 인코딩된 요청 경로의 예는 이 안내서의 뒷부분에 나와 있습니다.
>
>필터의 구조가 잘못된 경우 필터가 적용되지 않고 전체 결과 세트가 반환됩니다.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 속성 | 설명 |
| --- | --- |
| `{ENDPOINT}` | 필터 매개 변수를 지원하는 Reactor API의 목록 끝점입니다. |
| `{ATTRIBUTE_NAME}` | 결과를 필터링할 특정 속성의 이름입니다. 다른 종단점이 필터링을 위해 다른 특성을 지원한다는 점을 기억하십시오. 사용 가능한 필터링 특성 목록에 대해서는 작업 중인 끝점에 대한 참조 안내서 를 참조하십시오. |
| `{OPERATOR}` | 제공된 항목에 대해 결과가 평가되는 방법을 결정하는 연산자입니다. `{VALUE}`. 지원되는 연산자는 [부록 섹션](#supported-operators). |
| `{VALUE}` | 반환된 결과를 비교할 값입니다. 평형을 비교할 때 `EQ` 연산자인 경우 응답에 포함하려면 값이 대소문자를 구분하는 정확한 일치여야 합니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

아래 예제 요청은 라이브러리의 `state` 속성이 같음 `published`.

URI 인코딩 전에 요청 경로의 이 필터의 구문은 다음과 비슷합니다.

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

경로 및 쿼리 매개 변수가 URI로 인코딩되면 아래와 같이 API 요청에 사용할 수 있습니다.

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 여러 값에 대한 필터링 {#multiple-values}

단일 속성에 대해 여러 값으로 필터링하려면 값을 쉼표로 구분된 목록으로 제공합니다.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 여러 필터 사용

여러 속성에 필터를 적용하려면 `filter` 각 속성에 대한 매개 변수입니다. 매개 변수는 앰퍼샌드(`&`) 문자를 사용할 수 없습니다.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>동일한 요청의 여러 필터에 동일한 속성을 지정하는 경우 해당 속성에 대해 마지막으로 제공된 필터만 적용됩니다.

## 부록

다음 섹션에는 Reactor API에서 필터 작업을 위한 추가 정보가 포함되어 있습니다.

### 지원되는 필터 연산자 {#operators}

다음 표에는 필터 매개 변수에 대해 지원되는 연산자 값이 나열되어 있습니다. 필터링 중인 속성에 따라 문자열 속성에 &quot;보다 작음&quot; 또는 &quot;보다 큼&quot; 연산자 사용과 같이 사용 가능한 모든 필터 연산자를 적용할 수 없다는 점을 유의하십시오.

| 연산자 | 설명 |
| --- | --- |
| `EQ` | 속성은 제공된 값과 같아야 합니다. |
| `NOT` | 속성은 제공된 값과 같지 않아야 합니다. |
| `LT` | 속성은 제공된 값보다 작아야 합니다. |
| `GT` | 특성은 제공된 값보다 커야 합니다. |
| `BETWEEN` | 특성은 지정된 값 범위 내에 있어야 합니다. 이 연산자를 사용하는 경우, [두 값](#multiple-values) 원하는 범위의 최소값과 최대값을 나타내려면 을 제공해야 합니다. |
| `CONTAINS` | 속성에는 문자열 속성 내의 문자 세트와 같이 제공된 값을 포함해야 합니다. |
