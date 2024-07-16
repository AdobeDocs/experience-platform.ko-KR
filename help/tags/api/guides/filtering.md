---
title: Reactor API에서 응답 필터링
description: Reactor API에서 리소스를 나열할 때 결과를 필터링하는 방법을 알아봅니다.
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Reactor API에서 응답 필터링

Reactor API에서 목록(GET) 끝점을 사용하는 경우 반환된 결과를 레코드의 하위 집합으로 제한해야 할 수 있습니다. 이를 위해 많은 API 목록 엔드포인트가 특정 속성별로 필터링하는 기능을 지원합니다. 대신 API에 대한 구조화된 쿼리를 만들려면 [검색](./search.md)에 대한 안내서를 참조하십시오.

## 필터링 구문

다음 예에서는 GET 요청에 대한 필터를 구현하는 방법을 설명합니다.

**API 형식**

지정된 목록 끝점에 대한 응답을 필터링하려면 요청 경로에 `filter` 쿼리 매개 변수를 제공해야 합니다.

>[!NOTE]
>
>아래 템플릿은 가독성을 위해 대괄호(`[]`)와 공백 문자를 사용합니다. 실제로 이러한 문자는 [RFC 3986](https://tools.ietf.org/html/rfc3986)에 요약된 대로 URI로 인코딩되어야 합니다. 올바르게 인코딩된 요청 경로의 예는 이 안내서의 뒷부분에 나와 있습니다.
>
>필터의 구조가 잘못된 경우 필터가 적용되지 않고 전체 결과 세트가 반환됩니다.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| 속성 | 설명 |
| --- | --- |
| `{ENDPOINT}` | 필터 매개 변수를 지원하는 Reactor API의 목록 엔드포인트. |
| `{ATTRIBUTE_NAME}` | 결과를 필터링할 특정 속성의 이름입니다. 서로 다른 엔드포인트가 필터링에 대해 서로 다른 속성을 지원한다는 점을 기억하십시오. 사용 가능한 필터링 특성 목록은 작업 중인 엔드포인트에 대한 참조 안내서를 참조하십시오. |
| `{OPERATOR}` | 제공된 `{VALUE}`에 대해 결과를 평가하는 방법을 결정하는 연산자입니다. 지원되는 연산자는 [부록 섹션](#supported-operators)에 나열되어 있습니다. |
| `{VALUE}` | 반환된 결과를 비교할 값입니다. `EQ` 연산자를 사용하여 같음 여부를 비교할 때 값이 대소문자를 구분하는 정확한 일치여야 응답에 포함될 수 있습니다. |

{style="table-layout:auto"}

**요청**

아래 예제 요청은 라이브러리의 `state` 특성이 `published`과(와) 같아야 하는 필터를 적용하여 게시된 라이브러리 목록을 검색합니다.

URI를 인코딩하기 전에 요청 경로의 이 필터에 대한 구문은 다음과 유사합니다.

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

경로 및 쿼리 매개 변수가 URI로 인코딩되면 아래 요청과 같이 API 요청에 사용할 수 있습니다.

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## 여러 값에 대한 필터링 {#multiple-values}

단일 속성에 대해 여러 값을 기준으로 필터링하려면 값을 쉼표로 구분된 목록으로 제공합니다.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## 여러 필터 사용

여러 특성에 필터를 적용하려면 각 특성에 `filter` 매개 변수를 제공하십시오. 매개 변수는 앰퍼샌드(`&`) 문자로 구분해야 합니다.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>동일한 요청에 대해 여러 필터에 동일한 속성을 지정하는 경우 해당 속성에 대해 마지막으로 제공된 필터만 적용됩니다.

## 부록

다음 섹션에는 Reactor API의 필터 작업에 대한 추가 정보가 포함되어 있습니다.

### 지원되는 필터 연산자 {#operators}

다음 표에는 필터 매개 변수에 지원되는 연산자 값이 나와 있습니다. 필터링 기준으로 사용하는 속성에 따라 문자열 속성에 &quot;less than&quot; 또는 &quot;greater than&quot; 연산자를 사용하는 것과 같이 사용 가능한 모든 필터 연산자를 적용할 수 있는 것은 아닙니다.

| 연산자 | 설명 |
| --- | --- |
| `EQ` | 속성은 제공된 값과 같아야 합니다. |
| `NOT` | 속성은 제공된 값과 같지 않아야 합니다. |
| `LT` | 속성은 제공된 값보다 작아야 합니다. |
| `GT` | 속성은 제공된 값보다 커야 합니다. |
| `BETWEEN` | 속성은 지정된 값 범위 내에 있어야 합니다. 이 연산자를 사용할 때 원하는 범위의 최소값과 최대값을 나타내려면 [두 개의 값](#multiple-values)을 제공해야 합니다. |
| `CONTAINS` | 속성은 문자열 속성 내의 문자 집합과 같이 제공된 값을 포함해야 합니다. |
