---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 실시간 고객 프로파일 API 개발자 가이드
topic: guide
translation-type: tm+mt
source-git-commit: 95e002c60389ca7e4c1dcf32bbcf6f552cd55d95

---


# 프로필 검색

프로필 검색은 다양한 데이터 소스에 포함된 구성 가능한 필드를 검색하고 색인화하여 거의 실시간으로 반환하는 데 사용됩니다.

이 안내서에서는 프로필 검색을 보다 잘 이해하는 데 도움이 되는 정보를 제공하고 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

이 안내서에서 사용되는 API 끝점은 실시간 고객 프로필 API의 일부입니다. 계속하기 전에 실시간 [고객 프로필 개발자 안내서를](getting-started.md)참조하십시오.

특히 프로필 개발자 안내서의 [시작 섹션은](getting-started.md) 관련 항목에 대한 링크, 이 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

### 검색 결과 가져오기

검색 끝점을 사용하여 필수 매개 변수의 값과 추가 선택적 쿼리 매개 변수의 값을 기준으로 검색 결과를 가져올 수 있습니다. `schema.name` 앰퍼샌드(&amp;)로 구분하여 여러 매개 변수를 사용할 수 있습니다.

**API 형식**

```http
GET /search?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
|---|---|
| `schema.name` | **필수 여부.** 검색할 내용을 포함하는 스키마 클래스의 이름이며 점 표기법 형식으로 기록됩니다. 현재, `schema.name=_xdm.context.segmentdefinition` 만 지원됩니다. |
| `limit` | 반환할 검색 결과 수입니다. 기본값은 50입니다. |
| `page` | 검색된 쿼리 결과의 페이지 매김에 사용되는 페이지 번호입니다. |
| `s` | Microsoft의 Lucene 검색 구문 구현을 따르는 [쿼리입니다](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 검색어를 지정하지 않으면 연결된 모든 레코드가 `schema.name` 반환됩니다. 자세한 설명은 이 문서의 매개 변수 [검색](#search-parameters) 섹션에서 찾을 수 있습니다. |
| `namespace` | 매개 변수에 지정된 스키마 클래스에서 검색할 실제 데이터를 `schema.name` 식별합니다. |
| `organization.type` | 응답의 컨텐츠를 결정합니다. 반환되는 컨텐츠의 형식은 에 사용된 값에 따라 달라집니다 `schema.name`. 의 `_xdm.context.segmentdefinition`경우 유효한 값은 `hierarchy` 또는 `hierarchyinfo`입니다. |
| `organization.id` | **이`organization.type`지정된 경우 필요합니다.** 계층 구조에 사용할 때 지정된 조직의 계층을 `organization.type` 제공합니다. |

**요청**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 검색 기준을 충족하는 개체 배열을 반환합니다. 이 예에서는 `schema.name` 매개 변수가 `_xdm.context.segmentdefinition`사용되었으므로 세그먼트 정의 목록이 반환됩니다.

```json
{
  "aam-hierarchy": {
    "_xdm.context.segmentdefinition": [
      {
        "isFolder": true,
        "id": "100023",
        "name": "Segment Definition 1",
        "description": "Sample description.",
        "parentFolderId": "99970"
      },
      {
        "isFolder": false,
        "id": "1000028",
        "name": "Segment Definition 2",
        "description": "Sample description.",
        "parentFolderId": "103584"
      }
    ]
  },
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": "1",
    "pageSize": 2,
    "limit": 2
  }
}
```

### 프로비저닝 요청 만들기

종단점에 POST 요청을 수행하여 스키마에 대한 프로필 검색을 활성화하는 프로비저닝 요청을 만들 수 `/search/provisioning/component/init` 있습니다.

**요청**

>[!CAUTION]
>이 POST 요청에는 페이로드가 포함되어 있지 않으므로 콘텐츠 형식 헤더가 필요하지 않습니다. 또한 모든 데이터가 전역 샌드박스로 전송되므로 샌드박스 헤더가 없습니다.

```shell
curl -X POST \
    https://platform.adobe.io/data/core/ups/search/provisioning/component/init \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' 
```

**응답**

성공적인 응답은 HTTP 상태 201(작성됨) 및 다음 메시지를 반환합니다.

```plaintext
The request has been fulfilled and resulted in a new resource being created.
```

### 구성 요청 처리

구성 끝점을 사용하여 새 IMS 조직에 대한 적절한 인덱스, 인덱서 및 데이터 소스 연결을 설정할 수 있습니다. 구성 요청을 처리하려면 두 가지 속성이 필요합니다. `databaseName` 및 `containerName`Adobe

`databaseName` 은 구성할 조직에 대한 프로필 데이터베이스의 이름을 나타냅니다.

`containerName` 는 구성 중에 읽히는 데이터 커넥터로 채워진 컨테이너의 이름을 나타냅니다. POST 요청에는 두 개의 값이 `containerName`있고, 하나 또는 둘 다 사용할 수 있습니다.
- `_xdm.content.segmentdefinition`
- `_experience.audiencemanager.segmentfolder`

### 구성 요청 만들기

다음 API 호출은 요청 페이로드에 제공된 매개 변수를 기반으로 필요한 데이터 소스, 인덱서 및 인덱스를 생성합니다.

**API 형식**

```http
POST /search/configure
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**응답**

성공적인 응답은 HTTP 상태 202(허용됨) 및 일반 텍스트 메시지를 반환합니다.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

### 구성 요청 삭제

다음 API 호출은 일치하는 인덱스 항목을 제거하고 요청 페이로드에서 제공된 매개 변수를 기반으로 인덱서 및 데이터 소스를 삭제합니다.

>[!NOTE]
>인덱스 자체는 공유 리소스이므로 삭제되지 않습니다.

**API 형식**

```http
DELETE /search/configure
```

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/search/configure \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "databaseName": {DATABASE_NAME},
    "containerName": "_xdm.context.segmentdefinition" "_experience.audiencemanager.segmentfolder"
  }'
```

**응답**

성공적인 응답은 HTTP 상태 202(허용됨) 및 일반 텍스트 메시지를 반환합니다.

```plaintext
The request has been accepted for processing, but the processing has not been completed.
```

## 다음 단계

이 가이드를 읽고 나면 실시간 고객 프로필 검색 작동 방식을 더 잘 이해할 수 있습니다. 실시간 고객 프로필에 대한 자세한 내용은 실시간 고객 [프로필 개요를](../home.md)참조하십시오. 세그멘테이션에 대한 자세한 내용은 세그멘테이션 [개요를](../../segmentation/home.md)참조하십시오.

## 부록 {#appendix}

### 매개 변수 검색 {#search-parameters}

다음 표에는 검색 API를 사용할 때 검색 매개 변수가 작동하는 방식에 대한 세부 사항이 나와 있습니다.

| 검색 쿼리 | 설명 |
|------------ | -----------|
| foo | 원하는 단어를 검색합니다. 검색 가능한 필드에 &quot;foo&quot;라는 단어가 있으면 결과가 반환됩니다. |
| foo AND bar | 부울 검색입니다. 검색 가능한 필드에 &quot;foo&quot;와 &quot;bar&quot; **라는 단어가 모두** 있는 경우 결과가 반환됩니다. |
| foo bar | 부울 검색입니다. 검색 가능한 필드에 &quot;foo&quot; **라는** 단어 또는 &quot;bar&quot;라는 단어가 있으면 결과가 반환됩니다. |
| foo NOT 막대 | 부울 검색입니다. &quot;foo&quot;라는 단어를 찾았지만 &quot;bar&quot;라는 단어를 검색 가능한 필드에 찾을 수 없으면 결과가 반환됩니다. |
| name:foo AND bar | 부울 검색입니다. &quot;name&quot; 필드에 &quot;foo&quot;와 &quot;bar&quot; **라는 단어가 모두** 있는 경우 결과가 반환됩니다. |
| run* | 와일드카드 검색입니다. 별표(*)를 사용하면 0개 이상의 문자와 일치합니다. 즉, 검색 가능한 필드의 내용에 &quot;run&quot;으로 시작하는 단어가 포함되어 있으면 결과가 반환됩니다. 예를 들어 &quot;runs&quot;, &quot;running&quot;, &quot;runt&quot; 또는 &quot;runt&quot;라는 단어가 나타나면 결과가 반환됩니다. |
| 캠? | 와일드카드 검색입니다. 물음표(?) 사용 검색 가능한 필드의 내용이 &quot;cam&quot; 및 추가 문자로 시작하는 경우 결과가 반환됩니다. 예를 들어 &quot;camp&quot; 또는 &quot;campaign&quot;이라는 단어가 나타나면 결과가 반환되지만 &quot;camera&quot; 또는 &quot;campfire&quot;라는 단어가 나타나면 결과가 반환되지 않습니다. |
| &quot;파란색 우산&quot; | 구문 검색. 검색 가능한 필드의 내용에 &quot;파란색 우산&quot;이라는 전체 구문이 포함된 경우 결과가 반환됩니다. |
| 파란색\~ | 모호한 검색. 선택 사항으로 물결표(~) 뒤에 0-2 사이의 숫자를 입력하여 편집 거리를 지정할 수 있습니다. 예를 들어 &quot;blue\~1&quot;은 &quot;blue&quot;, &quot;blues&quot; 또는 &quot;glus&quot;를 반환합니다. 퍼지 검색은 구문이 아닌 **용어에만** 적용할 수 있습니다. 하지만 구문의 각 단어 끝에 물결표를 추가할 수 있습니다. 예를 들어 &quot;camping\~ in\~ the\~ summer\~&quot;는 &quot;여름에 캠핑&quot;에서 일치합니다. |
| &quot;호텔 공항&quot;\~5 | 근접 검색 이 유형의 검색은 문서에서 서로 가까운 용어를 찾는 데 사용됩니다. 예를 들어 문구는 문서에서 5단어 내에 &quot;hotel&quot; 및 &quot;airport&quot;라는 용어를 `"hotel airport"~5` 찾습니다. |
| `/a[0-9]+b$/` | 정규 표현식 검색. 이 유형의 검색은 RegExp 클래스에 설명된 대로 슬래시 &quot;/&quot; 사이의 컨텐츠를 기준으로 일치를 찾습니다. 예를 들어 &quot;motel&quot; 또는 &quot;hotel&quot;이 포함된 문서를 찾으려면 을 `/[mh]otel/`지정합니다. 정규 표현식 검색은 단일 단어와 일치합니다. |

쿼리 구문에 대한 자세한 설명은 Lucene 쿼리 [구문 설명서를](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)참조하십시오.
