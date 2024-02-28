---
title: 세그먼트 검색 API 끝점
description: Adobe Experience Platform 세그먼테이션 서비스 API에서 세그먼트 검색은 다양한 데이터 소스에 포함된 필드를 검색하고 이를 실시간에 가깝게 반환하는 데 사용됩니다. 이 안내서에서는 세그먼트 검색을 더 잘 이해하는 데 도움이 되는 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.
role: Developer
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---

# 세그먼트 검색 엔드포인트

세그먼트 검색은 다양한 데이터 소스에 걸쳐 포함된 필드를 검색하고 이를 실시간에 가깝게 반환하는 데 사용됩니다.

이 안내서에서는 세그먼트 검색을 더 잘 이해하는 데 도움이 되는 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

이 안내서에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

시작 섹션에 설명된 필수 헤더 외에도 세그먼트 검색 끝점에 대한 모든 요청에는 다음 추가 헤더가 필요합니다.

- x-ups-search-version: &quot;1.0&quot;

### 여러 네임스페이스 검색

이 검색 끝점을 사용하여 다양한 네임스페이스를 검색하고 검색 카운트 결과 목록을 반환할 수 있습니다. 여러 매개 변수를 사용하여 앰퍼샌드(&amp;)로 구분할 수 있습니다.

**API 형식**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 매개 변수 | 설명 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(필수)** 위치 {SCHEMA} 검색 객체와 연관된 스키마 클래스 값을 나타냅니다. 현재는 `_xdm.context.segmentdefinition` 은(는) 지원됩니다. |
| `s={SEARCH_TERM}` | *(선택 사항)* 위치 {SEARCH_TERM} 는 Microsoft의 구현을 준수하는 쿼리를 나타냅니다. [Lucene 검색 구문](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 검색어를 지정하지 않으면 연결된 모든 레코드가 `schema.name` 반환됩니다. 보다 자세한 설명은 [부록](#appendix) 이 문서. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**응답**

성공적인 응답은 다음 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### 개별 엔티티 검색

이 검색 끝점을 사용하여 지정된 네임스페이스 내의 모든 전체 텍스트 인덱스 개체 목록을 검색할 수 있습니다. 여러 매개 변수를 사용하여 앰퍼샌드(&amp;)로 구분할 수 있습니다.

**API 형식**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 매개 변수 | 설명 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(필수)** 위치 {SCHEMA} 검색 개체와 연결된 스키마 클래스 값을 포함합니다. 현재는 `_xdm.context.segmentdefinition` 은(는) 지원됩니다. |
| `namespace={NAMESPACE}` | **(필수)** 위치 {NAMESPACE} 검색할 네임스페이스를 포함합니다. |
| `s={SEARCH_TERM}` | *(선택 사항)* 위치 {SEARCH_TERM} Microsoft의 구현을 준수하는 쿼리 포함 [Lucene 검색 구문](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 검색어를 지정하지 않으면 연결된 모든 레코드가 `schema.name` 반환됩니다. 보다 자세한 설명은 [부록](#appendix) 이 문서. |
| `entityId={ENTITY_ID}` | *(선택 사항)* 지정된 폴더 내에서만 검색할 수 있도록 제한합니다. {ENTITY_ID}. |
| `limit={LIMIT}` | *(선택 사항)* 위치 {LIMIT} 반환할 검색 결과 수를 나타냅니다. 기본값은 50입니다. |
| `page={PAGE}` | *(선택 사항)* 위치 {PAGE} 검색된 쿼리의 결과를 페이지 지정하는 데 사용되는 페이지 번호를 나타냅니다. 페이지 번호 시작 위치: **0**. |


**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**응답**

성공적인 응답은 검색 쿼리와 일치하는 결과와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### 검색 개체에 대한 구조적 정보 가져오기

이 검색 끝점을 사용하여 요청된 검색 개체에 대한 구조적 정보를 가져올 수 있습니다.

**API 형식**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 매개 변수 | 설명 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(필수)** 위치 {SCHEMA} 검색 개체와 연결된 스키마 클래스 값을 포함합니다. 현재는 `_xdm.context.segmentdefinition` 은(는) 지원됩니다. |
| `namespace={NAMESPACE}` | **(필수)** 위치 {NAMESPACE} 검색할 네임스페이스를 포함합니다. |
| `entityId={ENTITY_ID}` | **(필수)** 구조 정보를 가져올 검색 개체의 ID로, 다음과같이 지정됩니다. {ENTITY_ID}. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**응답**

성공적인 응답은 요청된 검색 개체에 대한 자세한 구조적 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## 다음 단계

이제 이 안내서를 읽고 세그먼트 검색 작동 방식을 보다 잘 이해할 수 있습니다.

## 부록 {#appendix}

다음 섹션에서는 검색어의 작동 방식에 대한 추가 정보를 제공합니다. 검색 쿼리는 다음과 같은 방식으로 작성됩니다. `s={FieldName}:{SearchExpression}`. 따라서 예를 들어 AAM 또는 라는 세그먼트 정의를 검색하려면 [!DNL Platform], 다음 검색 쿼리를 사용합니다. `s=segmentName:AAM%20OR%20Platform`.

>  모범 사례의 경우 위에 표시된 예제와 같이 검색 표현식을 HTML으로 인코딩해야 합니다.

### 필드 검색 {#search-fields}

다음 표에는 검색 쿼리 매개 변수 내에서 검색할 수 있는 필드가 나열되어 있습니다.

| 필드 이름 | 설명 |
| ---------- | ----------- |
| folderId | 지정한 검색의 폴더 ID가 있는 폴더입니다. |
| folderLocation | 지정한 검색의 폴더 위치가 있는 위치. |
| parentFolderId | 지정된 검색의 상위 폴더 ID가 있는 세그먼트 정의 또는 폴더입니다. |
| segmentId | 지정된 검색의 세그먼트 ID와 일치하는 세그먼트 정의입니다. |
| segmentName | 지정된 검색의 세그먼트 이름과 일치하는 세그먼트 정의입니다. |
| segmentDescription | 지정된 검색의 세그먼트 설명과 일치하는 세그먼트 정의입니다. |

### 검색 표현식 {#search-expression}

다음 표에는 세그먼트 검색 API를 사용할 때 검색 쿼리가 작동하는 방식에 대한 세부 사항이 나와 있습니다.

>  다음 예는 더 나은 명확성을 위해 비-HTML 인코딩 형식으로 표시됩니다. 모범 사례를 위해 HTML은 검색 표현식을 인코딩합니다.

| 검색 표현식 예 | 설명 |
| ------------------------- | ----------- |
| foo | 아무 단어나 검색합니다. 검색 가능한 필드에 &quot;foo&quot;라는 단어가 있으면 결과가 반환됩니다. |
| foo 및 BAR | 부울 검색. 다음과 같은 경우 결과가 반환됩니다. **모두** 단어 &quot;foo&quot; 및 &quot;bar&quot;는 검색 가능한 필드에서 찾을 수 있습니다. |
| foo 또는 BAR | 부울 검색. 다음과 같은 경우 결과가 반환됩니다. **다음 중 하나** 단어 &quot;foo&quot; 또는 단어 &quot;bar&quot;는 검색 가능한 필드 중 하나에서 찾을 수 있습니다. |
| foo NOT 막대 | 부울 검색. 단어 &quot;foo&quot;를 찾았지만 단어 &quot;bar&quot;를 검색 가능한 필드에서 찾을 수 없는 경우 결과가 반환됩니다. |
| 이름: foo 및 막대 | 부울 검색. 다음과 같은 경우 결과가 반환됩니다. **모두** &quot;foo&quot; 및 &quot;bar&quot;라는 단어는 &quot;name&quot; 필드에 있습니다. |
| 실행* | 와일드카드 검색입니다. 별표(*)를 사용하면 0개 이상의 문자가 일치합니다. 즉, 검색 가능한 필드의 내용에 &quot;실행&quot;으로 시작하는 단어가 포함된 경우 결과가 반환됩니다. 예를 들어 &quot;runs&quot;, &quot;running&quot;, &quot;runner&quot; 또는 &quot;runt&quot;이라는 단어가 나타나는 경우 결과가 반환됩니다. |
| 캠? | 와일드카드 검색입니다. 물음표 사용(?) 는 정확히 하나의 문자만 일치합니다. 즉, 검색 가능한 필드의 내용이 &quot;cam&quot; 및 추가 문자로 시작하는 경우 결과를 반환합니다. 예를 들어 &quot;camp&quot; 또는 &quot;cams&quot;라는 단어가 나타나면 결과를 반환하지만, &quot;camera&quot; 또는 &quot;campfire&quot;라는 단어가 나타나면 결과를 반환하지 않습니다. |
| &quot;파란색 우산&quot; | 구문 검색입니다. 검색 가능한 필드의 내용에 &quot;파란색 우산&quot; 전체 구문이 포함된 경우 결과가 반환됩니다. |
| 파랑\~ | 흐릿한 검색입니다. 물결표 뒤에 0~2 사이의 숫자를 입력하여 편집 거리를 지정할 수도 있습니다. 예를 들어 &quot;blue\~1&quot;은 &quot;blue&quot;, &quot;blues&quot; 또는 &quot;glue&quot;를 반환합니다. 유사 항목 검색 가능 **전용** 구문이 아닌 용어에 적용됩니다. 그러나 각 단어의 끝에 물결표를 추가할 수 있습니다. 따라서 예를 들어 &quot;camping\~ in\~ the\~ summer\~&quot;는 &quot;여름의 캠핑&quot;과 일치합니다. |
| &quot;hotel airport&quot;\~5 | 근접 검색. 이 유형의 검색은 문서에서 서로 가까운 검색어를 찾는 데 사용됩니다. 예를 들어, 구 `"hotel airport"~5` 문서에서 서로 5단어 이내에 있는 &quot;hotel&quot;과 &quot;airport&quot;라는 용어를 찾습니다. |
| `/a[0-9]+b$/` | 정규 표현식 검색입니다. 이 유형의 검색은 RegExp 클래스에 설명된 대로 슬래시 &quot;/&quot; 사이의 내용을 기반으로 일치 항목을 찾습니다. 예를 들어 &quot;motel&quot; 또는 &quot;hotel&quot;이 포함된 문서를 찾으려면 `/[mh]otel/`. 정규 표현식 검색은 단일 단어에 대해 일치합니다. |

쿼리 구문에 대한 자세한 내용은 [Lucene 쿼리 구문 설명서](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
