---
keywords: Experience Platform;segmentation;segmentation service;troubleshooting;API;seg;segment;Segment;search;segment search;
title: 세그먼트 검색 끝점
topic: guide
description: 세그먼트 검색은 다양한 데이터 소스에 포함된 필드를 검색하고 거의 실시간으로 반환하는 데 사용됩니다. 이 안내서에서는 세그먼트 검색을 더 잘 이해할 수 있도록 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---


# 세그먼트 검색 끝점

세그먼트 검색은 다양한 데이터 소스에 포함된 필드를 검색하고 거의 실시간으로 반환하는 데 사용됩니다.

이 안내서에서는 세그먼트 검색을 더 잘 이해할 수 있도록 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

이 안내서에 사용되는 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md) 에서 필수 머리글 및 예제 API 호출 읽기 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

시작하기 섹션에 요약된 필수 헤더 외에 세그먼트 검색 종단점에 대한 모든 요청에는 다음과 같은 추가 헤더가 필요합니다.

- x-ups-search-version:&quot;1.0&quot;

### 여러 네임스페이스 검색

이 검색 끝점을 사용하여 다양한 네임스페이스에서 검색하면 검색 수 결과 목록이 반환됩니다. 여러 매개 변수를 앰퍼샌드(&amp;)로 구분하여 사용할 수 있습니다.

**API 형식**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 매개 변수 | 설명 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(필수)** 여기서 {SCHEMA}은 검색 개체와 관련된 스키마 클래스 값을 나타냅니다. 현재, 만 `_xdm.context.segmentdefinition` 지원됩니다. |
| `s={SEARCH_TERM}` | *(선택 사항)* 여기서 {SEARCH_TERM}은(는) Microsoft의 [Lucene의 검색 구문 구현을 준수하는 쿼리를 나타냅니다](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 검색어를 지정하지 않으면 연결된 모든 레코드가 `schema.name` 반환됩니다. 더 자세한 설명은 이 문서의 [부록에](#appendix) 나와 있다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

이 검색 끝점을 사용하여 지정된 네임스페이스 내의 전체 텍스트 인덱스 개체 목록을 모두 검색할 수 있습니다. 여러 매개 변수를 앰퍼샌드(&amp;)로 구분하여 사용할 수 있습니다.

**API 형식**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 매개 변수 | 설명 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(필수)** {SCHEMA}에 검색 개체와 관련된 스키마 클래스 값이 포함된 경우 현재, 만 `_xdm.context.segmentdefinition` 지원됩니다. |
| `namespace={NAMESPACE}` | **(필수)** {NAMESPACE}에 검색할 네임스페이스가 포함되어 있습니다. |
| `s={SEARCH_TERM}` | *(선택 사항)* {SEARCH_TERM}에 Microsoft의 [Lucene 검색 구문 구현을 준수하는 쿼리가 포함되어 있는 경우](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 검색어를 지정하지 않으면 연결된 모든 레코드가 `schema.name` 반환됩니다. 더 자세한 설명은 이 문서의 [부록에](#appendix) 나와 있다. |
| `entityId={ENTITY_ID}` | *(선택 사항)* {ENTITY_ID}로 지정된 지정된 폴더 내에서 검색을 제한합니다. |
| `limit={LIMIT}` | *(선택 사항)* 여기서 {LIMIT}은(는) 반환할 검색 결과 수를 나타냅니다. 기본값은 50입니다. |
| `page={PAGE}` | *(선택 사항)* 여기서 {PAGE}은(는) 검색된 쿼리 결과의 페이지 매김에 사용되는 페이지 번호를 나타냅니다. 페이지 번호는 **0**&#x200B;부터 시작됩니다. |


**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**응답**

성공적인 응답은 검색 쿼리와 일치하는 결과가 있는 HTTP 상태 200을 반환합니다.

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

### 검색 개체에 대한 구조 정보 가져오기

이 검색 끝점을 사용하여 요청된 검색 개체에 대한 구조적 정보를 가져올 수 있습니다.

**API 형식**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 매개 변수 | 설명 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **(필수)** {SCHEMA}에 검색 개체와 관련된 스키마 클래스 값이 포함된 경우 현재, 만 `_xdm.context.segmentdefinition` 지원됩니다. |
| `namespace={NAMESPACE}` | **(필수)** {NAMESPACE}에 검색할 네임스페이스가 포함되어 있습니다. |
| `entityId={ENTITY_ID}` | **(필수)** {ENTITY_ID}로 지정된 구조 정보를 가져올 검색 개체의 ID입니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**응답**

성공적인 응답은 요청된 검색 개체에 대한 자세한 구조 정보가 포함된 HTTP 상태 200을 반환합니다.

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

이제 이 안내서를 읽고 세그먼트 검색 방법을 더 잘 이해할 수 있습니다.

## 부록 {#appendix}

다음 섹션에서는 검색어 작동 방식에 대한 추가 정보를 제공합니다. 검색 쿼리는 다음과 같은 방법으로 작성됩니다. `s={FieldName}:{SearchExpression}`. 예를 들어 AAM 또는 라는 세그먼트를 검색하려면 다음 검색 쿼리 [!DNL Platform]를 사용합니다. `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] 최상의 방법을 위해 검색 표현식은 위에 표시된 예와 같이 HTML로 인코딩되어야 합니다.

### 검색 필드 {#search-fields}

다음 표에는 검색 쿼리 매개 변수 내에서 검색할 수 있는 필드가 나와 있습니다.

| 필드 이름 | 설명 |
| ---------- | ----------- |
| folderId | 지정한 검색의 폴더 ID가 있는 폴더 또는 폴더. |
| folderLocation | 지정된 검색의 폴더 위치가 있는 위치 또는 위치입니다. |
| parentFolderId | 지정된 검색의 상위 폴더 ID가 있는 세그먼트 또는 폴더. |
| segmentId | 세그먼트는 지정된 검색의 세그먼트 ID와 일치합니다. |
| segmentName | 세그먼트는 지정된 검색의 세그먼트 이름과 일치합니다. |
| segmentDescription | 세그먼트는 지정된 검색에 대한 세그먼트 설명과 일치합니다. |

### 검색 표현식 {#search-expression}

다음 표에는 세그먼트 검색 API를 사용할 때 검색 쿼리가 작동하는 방식에 대한 세부 사항이 나와 있습니다.

>!![NOTE] 다음 예는 HTML이 아닌 인코딩 형식으로 표시되므로 명확성이 향상됩니다. 최상의 방법을 위해 HTML은 검색 표현식을 인코딩합니다.

| 검색 표현식 예 | 설명 |
| ------------------------- | ----------- |
| foo | 아무 단어나 검색하세요. 검색 가능한 필드에 &quot;foo&quot;라는 단어가 있으면 결과가 반환됩니다. |
| foo AND bar | 부울 검색입니다. 검색 가능한 필드 중 하나에서 &quot;foo&quot;와 &quot;bar&quot;라는 **두** 단어를 모두 찾으면 결과가 반환됩니다. |
| OR 막대 | 부울 검색입니다. 검색 가능한 필드에 &quot;foo&quot; **** 단어 또는 &quot;bar&quot;라는 단어가 있으면 결과가 반환됩니다. |
| foo NOT bar | 부울 검색입니다. &quot;foo&quot;라는 단어를 찾았지만 검색 가능한 필드에 &quot;bar&quot;라는 단어를 찾을 수 없으면 결과가 반환됩니다. |
| name:foo AND bar | 부울 검색입니다. &quot;name&quot; 필드에 &quot;foo&quot;와 &quot;bar&quot;라는 **두** 단어가 모두 있는 경우 결과가 반환됩니다. |
| run* | 와일드카드 검색입니다. 별표(*)를 사용하면 0개 이상의 문자가 검색됩니다. 즉, 검색 가능한 필드의 내용에 &quot;run&quot;으로 시작하는 단어가 포함된 경우 결과가 반환됩니다. 예를 들어 단어 &quot;runs&quot;, &quot;running&quot;, &quot;runt&quot; 또는 &quot;runt&quot;가 나타나면 결과를 반환합니다. |
| 캠? | 와일드카드 검색입니다. 물음표(?) 사용 검색 가능한 필드의 내용이 &quot;cam&quot;과 추가 문자로 시작하는 경우 결과가 반환됩니다. 예를 들어 &quot;camp&quot; 또는 &quot;camams&quot;라는 단어가 나타나면 결과를 반환하지만 &quot;camera&quot; 또는 &quot;campfire&quot;라는 단어가 나타나면 결과를 반환하지 않습니다. |
| &quot;블루 우산&quot; | 구문 검색. 검색 가능한 필드 컨텐츠에 전체 구문 &quot;파란색 우산&quot;이 포함된 경우 결과가 반환됩니다. |
| 파란색\~ | 모호한 검색. 선택 사항으로 물결표(~) 뒤에 0-2 사이의 숫자를 입력하여 편집 거리를 지정할 수 있습니다. 예를 들어 &quot;blue\~1&quot;은 &quot;blue&quot;, &quot;blues&quot; 또는 &quot;gurl&quot;을 반환합니다. 퍼지 검색은 **구문이 아니라 용어에만** 적용할 수 있습니다. 하지만 구문의 각 단어 끝에 물결표를 추가할 수 있습니다. 예를 들어, &quot;camping\~ in\~ the\~ summer\~&quot;은 &quot;camping in the summer&quot; 와 일치합니다. |
| &quot;호텔 공항&quot;\~5 | 근접 검색 이 유형의 검색은 문서에서 서로 가까운 용어를 찾는 데 사용됩니다. 예를 들어 문구는 문서에서 5단어 내에 &quot;hotel&quot;과 &quot;airport&quot;라는 용어를 찾습니다. `"hotel airport"~5` |
| `/a[0-9]+b$/` | 정규 표현식 검색. 이 유형의 검색은 RegExp 클래스에 설명된 대로 슬래시 &quot;/&quot; 사이의 컨텐츠를 기준으로 일치를 찾습니다. 예를 들어 &quot;motel&quot; 또는 &quot;hotel&quot;이 포함된 문서를 찾으려면 을 지정합니다 `/[mh]otel/`. 정규 표현식 검색은 단일 단어와 일치합니다. |

쿼리 구문에 대한 자세한 설명은 Lucene 쿼리 구문 설명서를 [참조하십시오](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).
