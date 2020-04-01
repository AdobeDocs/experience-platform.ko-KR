---
keywords: Experience Platform;download scores;customer ai;popular topics
solution: Experience Platform
title: 고객 AI에서 점수 다운로드
topic: Downloading scores
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 고객 AI에서 점수 다운로드

이 문서는 고객 AI에 대한 점수 다운로드에 대한 가이드로 사용됩니다.

## 시작하기

고객 AI를 사용하면 점수를 쪽모이 세공 마루 파일 형식으로 다운로드할 수 있습니다. 이 자습서에서는 [시작하기](./getting-started.md) 안내서의 고객 AI 점수 다운로드 섹션을 읽고 완료해야 합니다.

또한 고객 AI의 점수에 액세스하려면 성공적인 실행 상태의 서비스 인스턴스를 사용할 수 있어야 합니다. 새 서비스 인스턴스를 만들려면 고객 AI [사용 안내서를](./user-guide.md)참조하십시오. 최근에 서비스 인스턴스를 만들었는데 여전히 트레이닝과 점수 지정 중이라면 24시간 후에 실행을 완료하십시오.

현재 고객 AI 점수를 다운로드하는 방법은 두 가지가 있습니다.

1. 개별 수준에서 점수를 다운로드하거나 실시간 고객 프로필을 사용하지 않으려면 먼저 데이터 세트 ID [찾기로 이동합니다](#dataset-id).
2. 프로필을 활성화한 상태에서 고객 AI를 사용하여 구성한 세그먼트를 다운로드하려면 고객 AI로 구성된 세그먼트를 [다운로드하십시오](#segment).

## Find your dataset ID {#dataset-id}

고객 AI 인사이트의 서비스 인스턴스 내에서 오른쪽 상단 탐색에서 *추가 작업* 드롭다운을 클릭한 다음 액세스 점수를 **선택합니다**.

![추가 작업](./images/insights/more-actions.png)

다운로드 점수 설명서 및 현재 인스턴스에 대한 데이터 세트 ID에 대한 링크가 포함된 새 대화 상자가 나타납니다. 데이터 집합 ID를 클립보드에 복사하고 다음 단계로 진행합니다.

![데이터 집합 ID](./images/download-scores/access-scores.png)

## 배치 ID 검색

이전 단계에서 데이터 세트 ID를 사용하여 일괄 처리 ID를 검색하려면 카탈로그 API를 호출해야 합니다. 조직에 속한 배치 목록 대신 단일 배치를 반환하기 위해 이 API 호출에 추가 쿼리 매개 변수가 사용됩니다. 사용 가능한 쿼리 매개 변수 유형에 대한 자세한 내용은 쿼리 매개 변수를 [사용하여 카탈로그 데이터](../../catalog/api/filter-data.md)필터링에 대한 가이드를 참조하십시오.

**API 형식**

```http
GET /batches?&dataSet={DATASET_ID}&orderBy=desc:created&limit=1
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | &quot;액세스 점수&quot; 대화 상자에서 사용할 수 있는 데이터 집합 ID입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?dataSet=5cd9146b31dae914b75f654f&orderBy=desc:created&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 점수 배치 ID 개체가 포함된 페이로드를 반환합니다. 이 예에서 개체는 `5e602f67c2f39715a87f46b1`입니다.

score batch ID 개체 내에는 `relatedObjects` 배열이 있습니다. 이 배열에는 두 개의 객체가 포함되어 있습니다. 첫 번째 개체에는 &quot;batch&quot; `type` 값이 있으며 ID도 포함되어 있습니다. 아래 예제 응답에서 배치 ID는 `035e2520-5e69-11ea-b624-51evfeba55d1`입니다. 다음 API 호출에 사용할 배치 ID를 복사합니다.

```json
{   
    "5e602f67c2f39715a87f46b1": {
        "imsOrg": "{IMS_ORG}",
        "relatedObjects": [
            {
                "id": "5c01a91863540e14cd3d0432",
                "type": "dataSet"
            },
            {
                "id": "035e2520-5e69-11ea-b624-51evfeba55d1",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsRead": 46721830,
            "recordsWritten": 46721830,
            "avgNumExecutorsPerTask": 33,
            "startTime": 1583362385336,
            "inputSizeInKb": 10242034,
            "endTime": 1583363197517
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    }
}
```

## 배치 ID로 다음 API 호출 검색

배치 ID가 있으면 새 GET 요청을 만들 수 `/batches`있습니다. 요청은 다음 API 요청으로 사용되는 링크를 반환합니다.

**API 형식**

```http
GET batches/{BATCH_ID}/files
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BATCH_ID}` | 이전 단계에서 검색한 배치 ID는 배치 ID를 [검색합니다](#retrieve-your-batch-id). |

**요청**

자신의 배치 ID를 사용하여 다음 요청을 수행합니다.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/035e2520-5e69-11ea-b624-51evfeba55d1/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `_links` 개체를 포함하는 페이로드를 반환합니다. 객체 `_links` 내에서 는 새로운 API `href` 호출을 값으로 사용합니다. 이 값을 복사하여 다음 단계로 진행합니다.

```json
{
    "data": [
        {
            "dataSetFileId": "035e2520-5e69-11ea-b624-51ecfeba55d0-1",
            "dataSetViewId": "5e3b2fe3fe4b9f18a8b7a3db",
            "version": "1.0.0",
            "created": "1583361894479",
            "updated": "1583361894479",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1"
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

## 파일 검색

이전 단계에서 얻은 `href` 값을 API 호출로 사용하여 새 GET 요청을 만들어 파일 디렉토리를 검색합니다.

**API 형식**

```http
GET files/{DATASETFILE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID는 `href` 이전 단계의 [](#retrieve-the-next-api-call-with-your-batch-id)값으로 반환됩니다. 객체 유형 아래의 `data` 배열에서 액세스할 수도 `dataSetFileId`있습니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답에는 단일 항목이 있거나 해당 디렉토리에 속하는 파일 목록이 있는 데이터 배열이 포함됩니다. 아래 예제는 파일 목록을 포함하며 가독성을 위해 요약되어 있습니다. 이 시나리오에서는 파일에 액세스하려면 각 파일의 URL을 따라야 합니다.

```json
{
    "data": [
        {
            "name": "part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet",
            "length": "16214531",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet"
                }
            }
        },
        {
            "name": "...",
            "length": "16235375",
            "_links": {
                "self": {
                    "href": "..."
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 100
    },
    "_links": {
        "next": {
            "href": "..."
        },
        "page": {
            "href": "...",
            "templated": true
        }
    }
}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `_links.self.href` | 디렉토리에 파일을 다운로드하는 데 사용되는 GET 요청 URL입니다. |


배열에 있는 모든 파일 객체의 `href` `data` 값을 복사한 다음 다음 다음 단계로 진행합니다.

## 파일 데이터 다운로드

파일 데이터를 다운로드하려면 이전 단계에서 복사한 `"href"` 값에 대해 GET 요청을 [만들어 파일을](#retrieving-your-files)검색합니다.

>[!NOTE] 이 요청을 명령줄에서 직접 수행하는 경우 요청 헤더 뒤에 출력을 추가하라는 메시지가 표시될 수 있습니다. 다음 요청 예는 `--output {FILENAME.FILETYPE}`사용합니다.

**API 형식**

```http
GET files/{DATASETFILE_ID}?path={FILE_NAME}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASETFILE_ID}` | dataSetFile ID는 `href` 이전 단계의 [](#retrieve-the-next-api-call-with-your-batch-id)값으로 반환됩니다. |
| `{FILE_NAME}` | 파일의 이름입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io:443/data/foundation/export/files/035e2520-5e69-11ea-b624-51ecfeba55d0-1?path=part-00000-tid-7597930103898538622-a25f1890-efa9-40eb-a2cb-1b378e93d582-528-1-c000.snappy.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -O 'filename.parquet'
```

>[!TIP] GET 요청을 하기 전에 파일을 저장할 올바른 디렉토리 또는 폴더에 있는지 확인합니다.

**응답**

응답으로 현재 디렉토리에서 요청한 파일이 다운로드됩니다. 이 예에서 파일 이름은 &quot;filename.쪽모이 세공&quot;입니다.

![터미널](./images/download-scores/response.png)

## 고객 AI로 구성된 세그먼트 다운로드 {#segment}

점수 데이터를 다운로드하는 또 다른 방법은 고객을 데이터 세트로 내보내는 것입니다. 세그멘테이션 작업이 성공적으로 완료된 후( `status` 속성 값이 &quot;성공&quot;됨), 대상을 액세스 및 작동 가능한 데이터 세트로 내보낼 수 있습니다. 세그멘테이션에 대한 자세한 내용은 [세그멘테이션 개요를](../../segmentation/home.md)참조하십시오.

>[!IMPORTANT] 이러한 내보내기 방식을 활용하려면 데이터 세트에 대해 실시간 고객 프로필을 활성화해야 합니다.

세그먼트 평가 안내서의 세그먼트 [](../../segmentation/tutorials/evaluate-a-segment.md) 내보내기 섹션에서는 대상 데이터 세트를 내보내는 데 필요한 단계를 다룹니다. 안내선 개요를 보고 다음 예를 제공합니다.

- **타겟 데이터 세트 만들기:** 데이터 세트를 만들어 대상 멤버를 보유합니다.
- **데이터 세트에서 고객 프로파일 생성:** 세그먼트 작업 결과를 기반으로 XDM 개별 프로필로 데이터 세트를 채웁니다.
- **내보내기 진행 상태 모니터링:** 내보내기 프로세스의 현재 진행 상태를 확인합니다.
- **고객 데이터 읽기:** 대상 구성원을 나타내는 결과 XDM 개별 프로필을 검색합니다.

## 다음 단계

이 문서에서는 고객 AI 점수를 다운로드하는 데 필요한 단계를 간략하게 설명합니다. 이제 제공되는 다른 [지능형 서비스](../home.md) 및 가이드를 계속 검색할 수 있습니다.
