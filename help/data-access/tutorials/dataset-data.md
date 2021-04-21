---
keywords: Experience Platform;홈;인기 항목;데이터 액세스;데이터 액세스 api;쿼리 데이터 액세스
solution: Experience Platform
title: 데이터 액세스 API를 사용하여 데이터 세트 데이터 보기
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform의 데이터 액세스 API를 사용하여 데이터 세트 내에 저장된 데이터를 찾고, 액세스하고, 다운로드하는 방법을 알아봅니다. 페이징 및 부분 다운로드와 같은 데이터 액세스 API의 몇 가지 고유한 기능을 소개합니다.
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 2%

---

# [!DNL Data Access] API를 사용하여 데이터 집합 데이터 보기

이 문서에서는 Adobe Experience Platform의 [!DNL Data Access] API를 사용하여 데이터 세트 내에 저장된 데이터를 검색, 액세스 및 다운로드하는 방법을 설명하는 단계별 자습서를 제공합니다. 페이지 지정 및 부분 다운로드와 같은 [!DNL Data Access] API의 일부 고유 기능을 소개합니다.

## 시작하기

이 자습서에서는 데이터 세트를 만들고 채우는 방법에 대한 내용을 이해해야 합니다. 자세한 내용은 [데이터 집합 만들기 자습서](../../catalog/datasets/create.md)를 참조하십시오.

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 시퀀스 다이어그램

이 자습서는 아래의 시퀀스 다이어그램에 나와 있는 단계에 따라 [!DNL Data Access] API의 핵심 기능을 강조 표시합니다.</br>
![](../images/sequence_diagram.png)

[!DNL Catalog] API를 사용하면 배치 및 파일에 대한 정보를 검색할 수 있습니다. [!DNL Data Access] API를 사용하면 파일 크기에 따라 HTTP를 통해 이러한 파일을 전체 또는 부분 다운로드로 액세스하고 다운로드할 수 있습니다.

## 데이터 찾기

[!DNL Data Access] API를 사용하기 전에 액세스하려는 데이터의 위치를 식별해야 합니다. [!DNL Catalog] API에는 조직의 메타데이터를 검색하고 액세스하려는 일괄 처리 또는 파일의 ID를 검색하는 데 사용할 수 있는 두 개의 끝점이 있습니다.

- `GET /batches`:조직 아래의 배치 목록을 반환합니다.
- `GET /dataSetFiles`:조직 아래의 파일 목록을 반환합니다.

[!DNL Catalog] API의 끝점 전체 목록을 보려면 [API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)를 참조하십시오.

## IMS 조직 아래의 배치 목록 검색

[!DNL Catalog] API를 사용하여 조직 아래에 배치 목록을 반환할 수 있습니다.

**API 형식**

```http
GET /batches
```

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 IMS 조직과 관련된 모든 배치를 나열하는 객체가 포함되며, 각 최상위 레벨 값은 배치를 나타냅니다. 개별 일괄 처리 객체에는 해당 특정 일괄 처리에 대한 세부 사항이 포함됩니다. 공간에 대한 아래 응답은 최소화되었습니다.

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{IMS_ORG}",
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

필터는 특정 사용 사례에 대한 관련 데이터를 검색하기 위해 특정 배치를 찾는 데 필요한 경우가 많습니다. 반환된 응답을 필터링하기 위해 매개 변수를 `GET /batches` 요청에 추가할 수 있습니다. 아래 요청은 특정 데이터 세트 내에서 지정된 시간 이후에 만들어진 모든 배치를 언제 생성했는지 기준으로 정렬하여 반환합니다.

**API 형식**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 시작 타임스탬프(밀리초)입니다(예: 1514836799000). |
| `{DATASET_ID}` | 데이터 집합 식별자입니다. |
| `{SORT_BY}` | 제공된 값별로 응답을 정렬합니다. 예를 들어 `desc:created`은 작성 날짜별로 개체를 내림차순으로 정렬합니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{IMS_ORG}",
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
        "imsOrg": "{IMS_ORG}",
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

매개 변수 및 필터의 전체 목록은 [카탈로그 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)에서 찾을 수 있습니다.

## 특정 일괄 처리에 속하는 모든 파일 목록 검색

액세스하려는 일괄 처리의 ID가 있으므로 [!DNL Data Access] API를 사용하여 해당 일괄 처리에 속하는 파일 목록을 가져올 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/files
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 액세스하려는 일괄 처리의 일괄 처리 식별자입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

응답에는 지정된 일괄 처리 내의 모든 파일을 나열하는 데이터 배열이 포함됩니다. 파일은 해당 파일 ID로 참조되며 이 ID는 `dataSetFileId` 필드 아래에 있습니다.

## 파일 ID를 사용하여 파일에 액세스

고유한 파일 ID가 있는 경우 [!DNL Data Access] API를 사용하여 파일 이름, 크기(바이트), 파일 다운로드 링크 등 파일의 세부 정보에 액세스할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

파일 ID가 개별 파일 또는 디렉토리를 가리키는지 여부에 따라 반환된 데이터 배열에 해당 디렉토리에 속하는 파일 목록이나 단일 항목이 포함될 수 있습니다. 각 파일 요소에는 파일 이름, 바이트 크기 및 파일 다운로드 링크 등의 세부 사항이 포함됩니다.

**사례 1:파일 ID가 단일 파일을 가리킵니다.**

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
| `{FILE_NAME}.parquet` | 파일의 이름입니다. |
| `_links.self.href` | 파일을 다운로드할 URL입니다. |

**사례 2:파일 ID가 디렉토리를 가리킵니다.**

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

이 응답은 ID가 `{FILE_ID_2}` 및 `{FILE_ID_3}`인 두 개의 개별 파일이 포함된 디렉토리를 반환합니다. 이 시나리오에서는 파일에 액세스하려면 각 파일의 URL을 따라야 합니다.

## 파일의 메타데이터 검색

HEAD 요청을 수행하여 파일의 메타데이터를 검색할 수 있습니다. 파일의 크기(바이트 및 파일 형식)를 포함하여 파일의 메타데이터 헤더를 반환합니다.

**API 형식**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 파일의 식별자입니다. |
| `{FILE_NAME}` | 파일 이름(예: profiles.partional) |

**요청**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 헤더에는 다음을 포함하여 쿼리된 파일의 메타데이터가 포함됩니다.
- `Content-Length`:페이로드 크기(바이트)를 나타냅니다.
- `Content-Type`:파일 유형을 나타냅니다.

## 파일의 내용에 액세스

[!DNL Data Access] API를 사용하여 파일의 내용에 액세스할 수도 있습니다.

**API 형식**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID}` | 파일의 식별자입니다. |
| `{FILE_NAME}` | 파일 이름(예: profiles.partional). |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 파일의 내용을 반환합니다.

## 파일의 일부 내용 다운로드

[!DNL Data Access] API에서는 파일을 청크 단위로 다운로드할 수 있습니다. 파일에서 특정 바이트 범위를 다운로드하도록 `GET /files/{FILE_ID}` 요청 중에 범위 헤더를 지정할 수 있습니다. 범위가 지정되지 않은 경우 기본적으로 API는 전체 파일을 다운로드합니다.

[이전 섹션](#retrieve-the-metadata-of-a-file)의 HEAD 예제에서는 특정 파일의 크기를 바이트 단위로 지정합니다.

**API 형식**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_ID} ` | 파일의 식별자입니다. |
| `{FILE_NAME}` | 파일 이름(예: profiles.partional) |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| 속성 | 설명 |
| -------- | ----------- | 
| `Range: bytes=0-99` | 다운로드할 바이트 범위를 지정합니다. 지정하지 않으면 API에서 전체 파일을 다운로드합니다. 이 예에서 처음 100바이트는 다운로드됩니다. |

**응답**

응답 본문에는 HTTP 상태 206(부분 내용)과 함께 요청의 &quot;범위&quot; 헤더에 지정된 파일의 처음 100바이트가 포함됩니다. 응답에는 다음 헤더도 포함됩니다.

- 컨텐츠 길이:100(반환된 바이트 수)
- 컨텐츠 유형:응용 프로그램/쪽모이 세공 항목(요청 후 응답 컨텐트 유형은 `parquet`)입니다.
- 컨텐츠 범위:바이트 0-99/249058(요청된 범위(0-99)는 총 바이트 수(249058) 중)

## API 응답 페이지 매김 구성

[!DNL Data Access] API 내의 응답에 페이지가 매겨집니다. 기본적으로 페이지당 최대 항목 수는 100개입니다. 페이징 매개 변수를 사용하여 기본 동작을 수정할 수 있습니다.

- `limit`:&quot;limit&quot; 매개 변수를 사용하여 요구 사항에 따라 페이지당 항목 수를 지정할 수 있습니다.
- `start`:오프셋은 &quot;시작&quot; 쿼리 매개 변수로 설정할 수 있습니다.
- `&`:앰퍼샌드를 사용하여 한 번의 호출에서 여러 매개 변수를 결합할 수 있습니다.

**API 형식**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 액세스하려는 일괄 처리의 일괄 처리 식별자입니다. |
| `{OFFSET}` | 결과 배열을 시작할 지정된 인덱스(예: start=0) |
| `{LIMIT}` | 결과 배열에서 반환되는 결과 수를 제어합니다(예: limit=1). |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**:

응답에는 요청 매개 변수 `limit=1`에 지정된 대로 단일 요소가 있는 `"data"` 배열이 포함됩니다. 이 요소는 요청에 있는 `start=0` 매개 변수로 지정된 대로 사용 가능한 첫 번째 파일의 세부 사항을 포함하는 객체입니다(0부터 번호를 매기려면 첫 번째 요소는 &quot;0&quot;임).

`_links.next.href` 값에는 `start` 매개 변수가 `start=1`에 고급화된 것을 확인할 수 있는 다음 응답 페이지에 대한 링크가 포함되어 있습니다.

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
