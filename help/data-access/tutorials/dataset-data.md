---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;데이터 액세스 api;쿼리 데이터 액세스
solution: Experience Platform
title: 데이터 액세스 API를 사용하여 데이터 집합 데이터 보기
type: Tutorial
description: Adobe Experience Platform에서 데이터 액세스 API를 사용하여 데이터 세트 내에 저장된 데이터를 찾아 액세스하고 다운로드하는 방법을 알아봅니다. 페이징 및 부분 다운로드와 같은 데이터 액세스 API의 몇 가지 고유한 기능에도 도입됩니다.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---

# 을 사용하여 데이터 집합 데이터 보기 [!DNL Data Access] API

이 문서에서는 [!DNL Data Access] Adobe Experience Platform의 API. 또한 [!DNL Data Access] 페이징 및 부분 다운로드와 같은 API입니다.

## 시작하기

이 자습서에서는 데이터 세트를 만들고 채우는 방법에 대한 작업 이해를 필요로 합니다. 자세한 내용은 [데이터 세트 생성 자습서](../../catalog/datasets/create.md) 추가 정보.

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- 권한 부여: 베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

## 시퀀스 다이어그램

이 자습서에서는 아래의 시퀀스 다이어그램에 요약된 단계에 따라 의 핵심 기능을 강조 표시합니다 [!DNL Data Access] API.</br>
![](../images/sequence_diagram.png)

다음 [!DNL Catalog] API를 사용하면 배치 및 파일에 대한 정보를 검색할 수 있습니다. 다음 [!DNL Data Access] API를 사용하면 파일의 크기에 따라 HTTP를 통해 전체 또는 일부 다운로드로 이러한 파일에 액세스하고 다운로드할 수 있습니다.

## 데이터를 찾습니다

를 사용하기 전에 [!DNL Data Access] API인 경우 액세스하려는 데이터의 위치를 식별해야 합니다. 에서 [!DNL Catalog] API에는 조직의 메타데이터를 탐색하고, 액세스하려는 배치 또는 파일의 ID를 검색하는 데 사용할 수 있는 두 가지 엔드포인트가 있습니다.

- `GET /batches`: 조직 아래의 배치 목록 반환
- `GET /dataSetFiles`: 조직 아래의 파일 목록 반환

의 종단점 전체 목록 [!DNL Catalog] API는 [API 참조](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 조직 아래에서 배치 목록을 검색합니다

사용 [!DNL Catalog] API를 사용하여 조직 아래에 배치 목록을 반환할 수 있습니다.

**API 형식**

```http
GET /batches
```

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 조직과 관련된 모든 배치를 나열하고 각 최상위 값은 배치를 나타냅니다. 개별 배치 객체에는 해당 특정 배치에 대한 세부 정보가 포함됩니다. 공간에 대해 아래 응답이 최소화되었습니다.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### 배치 목록 필터링

특정 사용 사례에 대한 관련 데이터를 검색하기 위해 필터를 사용하여 특정 일괄 처리를 찾는 경우가 많습니다. 매개 변수를 `GET /batches` 반환된 응답을 필터링하기 위한 요청. 아래 요청은 지정된 시간 이후에 생성된 모든 배치를 특정 데이터 세트 내에서 생성되었는지 기준으로 정렬하여 반환합니다.

**API 형식**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 시작 타임스탬프(밀리초)입니다(예: 1514836799000). |
| `{DATASET_ID}` | 데이터 집합 식별자입니다. |
| `{SORT_BY}` | 제공된 값별로 응답을 정렬합니다. 예, `desc:created` 작성 날짜별로 개체를 내림차순으로 정렬합니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

매개 변수 및 필터의 전체 목록은 [카탈로그 API 참조](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 특정 배치에 속하는 모든 파일의 목록을 검색합니다

액세스할 배치의 ID가 있으므로 [!DNL Data Access] 해당 배치에 속하는 파일 목록을 가져오는 API.

**API 형식**

```http
GET /batches/{BATCH_ID}/files
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 액세스하려는 배치의 배치 식별자입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `data._links.self.href` | 이 파일에 액세스할 URL입니다. |

응답에는 지정된 일괄 처리 내의 모든 파일을 나열하는 데이터 배열이 포함됩니다. 파일은 파일 ID에서 참조하며, `dataSetFileId` 필드.

## 파일 ID를 사용하여 파일 액세스

고유 파일 ID가 있는 경우 [!DNL Data Access] 파일 이름, 크기(바이트) 및 다운로드 링크 등 파일에 대한 특정 세부 정보에 액세스할 수 있는 API입니다.

**API 형식**

```http
GET /files/{FILE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 액세스할 파일의 식별자입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

파일 ID가 개별 파일을 가리키는지 아니면 디렉토리를 가리키는지에 따라 반환된 데이터 배열에 해당 디렉토리에 속하는 파일 목록이나 단일 항목이 포함될 수 있습니다. 각 파일 요소에는 파일 이름, 크기(바이트), 파일을 다운로드할 수 있는 링크 등의 세부 사항이 포함됩니다.

**사례 1: 파일 ID는 단일 파일을 가리킵니다**

**응답**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | 파일 이름입니다. |
| `_links.self.href` | 파일을 다운로드할 URL입니다. |

**사례 2: 파일 ID가 디렉터리를 가리킵니다**

**응답**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `data._links.self.href` | 연결된 파일을 다운로드할 URL입니다. |

이 응답은 ID가 있는 두 개의 개별 파일이 포함된 디렉토리를 반환합니다 `{FILE_ID_2}` 및 `{FILE_ID_3}`. 이 시나리오에서는 파일에 액세스하려면 각 파일의 URL을 따라야 합니다.

## 파일의 메타데이터 검색

HEAD 요청을 수행하여 파일의 메타데이터를 검색할 수 있습니다. 파일 크기와 파일 형식을 포함하여 파일의 메타데이터 헤더를 반환합니다.

**API 형식**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 파일의 식별자입니다. |
| `{FILE_NAME}` | 파일 이름(예: profiles.parquet) |

**요청**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 헤더에는 다음을 포함하여 쿼리된 파일의 메타데이터가 포함됩니다.
- `Content-Length`: 페이로드 크기(바이트)를 나타냅니다
- `Content-Type`: 파일 유형을 나타냅니다.

## 파일의 내용 액세스

또한 [!DNL Data Access] API.

**API 형식**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 파일의 식별자입니다. |
| `{FILE_NAME}` | 파일 이름(예: profiles.parquet)입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 파일의 내용이 반환됩니다.

## 파일의 부분 컨텐츠 다운로드

다음 [!DNL Data Access] API에서 파일을 청크 단위로 다운로드할 수 있습니다. 범위 헤더는 `GET /files/{FILE_ID}` 파일에서 특정 바이트 범위를 다운로드하도록 요청합니다. 범위를 지정하지 않으면 기본적으로 API가 전체 파일을 다운로드합니다.

의 HEAD 예 [이전 섹션](#retrieve-the-metadata-of-a-file) 은 특정 파일의 크기를 바이트 단위로 지정합니다.

**API 형식**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID} ` | 파일의 식별자입니다. |
| `{FILE_NAME}` | 파일 이름(예: profiles.parquet) |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| 속성 | 설명 |
| -------- | ----------- | 
| `Range: bytes=0-99` | 다운로드할 바이트 범위를 지정합니다. 이 값을 지정하지 않으면 API가 전체 파일을 다운로드합니다. 이 예에서는 처음 100바이트가 다운로드됩니다. |

**응답**

상기 응답 본문은 상기 파일의 처음 100바이트(상기 요청의 &quot;범위&quot; 헤더에 의해 지정되는 대로)와 HTTP Status 206(Partial Contents)을 포함한다. 응답에는 다음 헤더도 포함됩니다.

- 컨텐츠 길이: 100(반환된 바이트 수)
- 컨텐츠 유형: 응용 프로그램/parquet(Parquet 파일이 요청되었으므로 응답 콘텐츠 유형은 다음과 같습니다. `parquet`)
- 컨텐츠 범위: 바이트 0-99/249058(요청된 범위(0-99)이 총 바이트 수(249058) 중)

## API 응답 페이지 매김 구성

내 응답 [!DNL Data Access] API의 페이지 매김입니다. 기본적으로 페이지당 최대 항목 수는 100개입니다. 페이징 매개 변수를 사용하여 기본 동작을 수정할 수 있습니다.

- `limit`: &quot;limit&quot; 매개 변수를 사용하여 요구 사항에 따라 페이지당 항목 수를 지정할 수 있습니다.
- `start`: 오프셋은 &quot;시작&quot; 쿼리 매개 변수로 설정할 수 있습니다.
- `&`: 앰퍼샌드를 사용하여 여러 매개 변수를 하나의 호출로 결합할 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 액세스하려는 배치의 배치 식별자입니다. |
| `{OFFSET}` | 결과 배열을 시작할 지정된 인덱스(예: start=0) |
| `{LIMIT}` | 결과 배열에 반환되는 결과 수를 제어합니다(예: limit=1). |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**:

응답에는 다음이 포함됩니다 `"data"` 요청 매개 변수에 지정된 대로 단일 요소가 있는 배열 `limit=1`. 이 요소는 `start=0` 요청의 매개 변수(0 기반 번호 지정에서 첫 번째 요소는 &quot;0&quot;임)입니다.

다음 `_links.next.href` 값에는 다음 응답 페이지에 대한 링크가 포함되어 있으며, 여기에서 `start` 매개 변수가 `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```
