---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 프로필 내보내기 작업 API 끝점
type: Documentation
description: 실시간 고객 프로필을 사용하면 특성 데이터와 행동 데이터를 모두 포함하여 여러 소스에서 데이터를 결합하여 Adobe Experience Platform 내에서 개별 고객에 대한 단일 보기를 작성할 수 있습니다. 그런 다음 추가적인 처리를 위해 프로필 데이터를 데이터 세트에 내보낼 수 있습니다.
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 2%

---

# 프로필 내보내기 작업 끝점

[!DNL Real-Time Customer Profile] 속성 데이터와 동작 데이터를 모두 포함하여 여러 소스에서 데이터를 결합하여 개별 고객에 대한 단일 뷰를 작성할 수 있습니다. 그런 다음 추가적인 처리를 위해 프로필 데이터를 데이터 세트에 내보낼 수 있습니다. 예를 들어 [!DNL Profile] 활성화를 위해 데이터를 내보낼 수 있고, 프로필 속성을 보고용으로 내보낼 수 있습니다.

이 문서에서는 [프로필 API](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>이 안내서에서는 의 내보내기 작업 사용에 대해 설명합니다 [!DNL Profile API]. Adobe Experience Platform 세그멘테이션 서비스의 내보내기 작업을 관리하는 방법에 대한 자세한 내용은 다음 안내서를 참조하십시오 [세분화 API에서 작업 내보내기](../../profile/api/export-jobs.md).

내보내기 작업을 만드는 것 외에도, [!DNL Profile] 데이터를 `/entities` 엔드포인트(&quot;라고도 함)[!DNL Profile Access]&quot;. 자세한 내용은 [엔티티 끝점 안내서](./entities.md) 추가 정보. 액세스 방법에 대한 절차 [!DNL Profile] UI를 사용하는 데이터는 [사용 안내서](../ui/user-guide.md).

## 시작하기

이 안내서에서 사용되는 API 엔드포인트는 [!DNL Real-Time Customer Profile] API. 계속하기 전에 [시작 안내서](getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 모든 호출을 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다 [!DNL Experience Platform] API.

## 내보내기 작업 만들기

내보내기 [!DNL Profile] 데이터를 사용하려면 먼저 데이터를 내보낼 데이터 세트를 만든 다음 새 내보내기 작업을 시작해야 합니다. 이 두 단계 모두 Experience Platform API를 사용하여 카탈로그 서비스 API를 사용하고 나머지 단계는 실시간 고객 프로필 API를 사용하여 수행할 수 있습니다. 각 단계를 완료하기 위한 자세한 지침은 다음에 나오는 섹션에 요약되어 있습니다.

### 대상 데이터 세트 만들기

내보내기 시 [!DNL Profile] 데이터 세트를 먼저 만들어야 합니다. 내보내기가 성공하도록 데이터 세트를 올바르게 구성해야 합니다.

주요 고려 사항 중 하나는 데이터 세트가 기반으로 하는 스키마입니다(`schemaRef.id` 를 반환합니다. 프로필 데이터를 내보내려면 데이터 세트가 [!DNL XDM Individual Profile] 결합 스키마 (`https://ns.adobe.com/xdm/context/profile__union`). 결합 스키마는 동일한 클래스를 공유하는 스키마의 필드를 집계하는 시스템에서 생성한 읽기 전용 스키마입니다. 이 경우, 이것이 [!DNL XDM Individual Profile] 클래스 이름을 지정합니다. 결합 보기 스키마에 대한 자세한 내용은 [스키마 구성 안내서의 기본 사항에 대한 결합 섹션](../../xdm/schema/composition.md#union).

이 자습서에서 수행하는 단계는 를 참조하는 데이터 세트를 만드는 방법을 간략하게 설명합니다 [!DNL XDM Individual Profile] 를 사용한 결합 스키마 [!DNL Catalog] API. 를 사용할 수도 있습니다 [!DNL Platform] 사용자 인터페이스를 사용하여 결합 스키마를 참조하는 데이터 세트를 만듭니다. UI 사용 단계는 [세그먼트 내보내기를 위한 이 UI 자습서](../../segmentation/tutorials/create-dataset-export-segment.md) 하지만 여기에 또한 적용됩니다. 완료되면 이 자습서로 돌아가서 다음 단계를 계속 진행할 수 있습니다. [새 내보내기 작업 시작](#initiate).

이미 호환되는 데이터 세트가 있고 해당 ID를 알고 있는 경우 다음 단계로 직접 진행할 수 있습니다 [새 내보내기 작업 시작](#initiate).

**API 형식**

```http
POST /dataSets
```

**요청**

다음 요청은 페이로드에 구성 매개 변수를 제공하는 새 데이터 세트를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        }
      }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 데이터 세트에 대한 수사적 이름입니다. |
| `schemaRef.id` | 데이터 집합과 연결할 결합 보기(스키마)의 ID입니다. |

**응답**

성공적인 응답은 새로 생성된 데이터 세트의 읽기 전용, 시스템 생성 및 고유 ID가 포함된 배열을 반환합니다. 프로필 데이터를 성공적으로 내보내려면 올바르게 구성된 데이터 세트 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 내보내기 작업 시작 {#initiate}

결합 유지 데이터 세트가 있는 경우에는 페이지에 POST 요청을 수행하여 프로필 데이터를 데이터 세트에 유지하는 내보내기 작업을 만들 수 있습니다 `/export/jobs` 실시간 고객 프로필 API의 종단점 및 요청 본문에서 내보낼 데이터의 세부 정보를 제공합니다.

**API 형식**

```http
POST /export/jobs
```

**요청**

다음 요청은 페이로드에 구성 매개 변수를 제공하여 새 내보내기 작업을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    }
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }' 
```

| 속성 | 설명 |
| -------- | ----------- |
| `fields` | *(선택 사항)* 내보내기에 포함할 데이터 필드를 이 매개 변수에 제공된 필드로만 제한합니다. 이 값을 생략하면 내보낸 데이터에 모든 필드가 포함됩니다. |
| `mergePolicy` | *(선택 사항)* 내보낸 데이터를 제어할 병합 정책을 지정합니다. 내보낼 세그먼트가 여러 개 있는 경우 이 매개 변수를 포함하십시오. |
| `mergePolicy.id` | 병합 정책의 ID입니다. |
| `mergePolicy.version` | 사용할 병합 정책의 특정 버전입니다. 이 값을 생략하면 기본적으로 최신 버전으로 설정됩니다. |
| `additionalFields.eventList` | *(선택 사항)* 다음 설정 중 하나 이상을 제공하여 자식 또는 관련 개체에 대해 내보낸 시계열 이벤트 필드를 제어합니다.<ul><li>`eventList.fields`: 내보낼 필드를 제어합니다.</li><li>`eventList.filter`: 연관된 객체에서 포함된 결과를 제한하는 기준을 지정합니다. 내보내기에 필요한 최소값(일반적으로 날짜)이 필요합니다.</li><li>`eventList.filter.fromIngestTimestamp`: 시계열 이벤트를 제공된 타임스탬프 이후에 수집된 이벤트로 필터링합니다. 이벤트 시간 자체가 아니라 이벤트의 수집 시간입니다.</li></ul> |
| `destination` | **(필수)** 내보낸 데이터에 대한 대상 정보:<ul><li>`destination.datasetId`: **(필수)** 데이터를 내보낼 데이터 세트의 ID입니다.</li><li>`destination.segmentPerBatch`: *(선택 사항)* 지정하지 않은 경우 기본값이 로 설정되는 부울 값 `false`. 값 `false` 모든 세그먼트 ID를 단일 배치 ID로 내보냅니다. 값 `true` 하나의 세그먼트 ID를 하나의 배치 ID로 내보냅니다. 값을 다음과 같이 설정합니다. `true` 배치 내보내기 성능에 영향을 줄 수 있습니다.</li></ul> |
| `schema.name` | **(필수)** 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |

>[!NOTE]
>
>프로필 데이터만 내보내고 관련 시계열 데이터를 포함하지 않으려면 요청에서 &quot;additionalFields&quot; 개체를 제거합니다.

**응답**

성공적인 응답은 요청에 지정된 대로 프로필 데이터로 채워진 데이터 세트를 반환합니다.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

## 모든 내보내기 작업 나열

에 GET 요청을 수행하여 특정 IMS 조직에 대한 모든 내보내기 작업 목록을 반환할 수 있습니다 `export/jobs` 엔드포인트. 이 요청은 쿼리 매개 변수도 지원합니다 `limit` 및 `offset`아래에 표시된 대로,

**API 형식**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `start` | 요청 만들기 시간에 따라 반환된 결과 페이지를 오프셋합니다. 예: `start=4` |
| `limit` | 반환된 결과 수를 제한합니다. 예: `limit=10` |
| `page` | 요청의 생성 시간에 따라 특정 결과 페이지를 반환합니다. 예: `page=2` |
| `sort` | 특정 필드별로 결과를 오름차순으로 정렬( **`asc`** ) 또는 내림차순( ) **`desc`** ) 순서를 지정합니다. 여러 결과 페이지를 반환하는 경우 정렬 매개 변수가 작동하지 않습니다. 예: `sort=updateTime:asc` |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

응답에는 다음이 포함됩니다 `records` IMS 조직에서 만든 내보내기 작업이 포함된 객체입니다.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{ORG_ID}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{ORG_ID}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

## 내보내기 진행 모니터링

특정 내보내기 작업의 세부 정보를 보거나 처리 시 해당 상태를 모니터링하려면 `/export/jobs` 엔드포인트 및 포함 `id` 경로에 있는 내보내기 작업의 수입니다. 내보내기 작업은 다음에 대한 `status` 필드는 값 &quot;SUCCEEDED&quot;를 반환합니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 다음 `id` 액세스하려는 내보내기 작업의 수입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId": "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{ORG_ID}",
    "creationTime": 1559674261657
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `batchId` | 프로필 데이터를 읽을 때 조회 목적으로 사용할 성공적인 내보내기에서 생성된 일괄 처리의 식별자입니다. |

## 내보내기 작업 취소

Experience Platform을 사용하면 기존 내보내기 작업을 취소할 수 있습니다. 내보내기 작업이 완료되지 않았거나 처리 단계에서 멈춘 경우를 포함하여 여러 가지 이유로 유용할 수 있습니다. 내보내기 작업을 취소하려면 `/export/jobs` 엔드포인트 및 포함 `id` 요청 경로로 취소할 내보내기 작업의 수입니다.

**API 형식**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 다음 `id` 액세스하려는 내보내기 작업의 수입니다. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

삭제 요청이 성공하면 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문을 반환하여 취소 작업이 성공적으로 수행되었음을 나타냅니다.

## 다음 단계

내보내기가 성공적으로 완료되면 Experience Platform의 Data Lake 내에서 데이터를 사용할 수 있습니다. 그런 다음 [데이터 액세스 API](https://www.adobe.io/experience-platform-apis/references/data-access/) 를 사용하여 데이터에 액세스하려면 `batchId` 내보내기와 연관됩니다. 내보내기 크기에 따라 데이터가 청크 단위일 수 있으며 배치는 여러 파일로 구성될 수 있습니다.

데이터 액세스 API를 사용하여 배치 파일에 액세스하고 다운로드하는 방법에 대한 단계별 지침은 [데이터 액세스 자습서](../../data-access/tutorials/dataset-data.md).

Adobe Experience Platform 쿼리 서비스를 사용하여 실시간 고객 프로필 데이터를 성공적으로 내보낼 수도 있습니다. UI 또는 RESTful API를 사용하는 쿼리 서비스를 사용하여 데이터 레이크 내의 데이터에 대한 쿼리를 작성, 유효성 검사 및 실행할 수 있습니다.

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 [Query Service 설명서](../../query-service/home.md).

## 부록

다음 섹션에는 프로필 API의 내보내기 작업에 대한 추가 정보가 포함되어 있습니다.

### 추가 내보내기 페이로드 예

API 호출 예 [내보내기 작업 시작](#initiate) 프로필(레코드)과 이벤트(시계열) 데이터를 모두 포함하는 작업을 만듭니다. 이 섹션에서는 내보내기를 한 데이터 유형 또는 다른 데이터 유형을 포함하도록 제한하는 추가적인 요청 페이로드 예를 제공합니다.

다음 페이로드는 프로필 데이터(이벤트 없음)만 포함하는 내보내기 작업을 만듭니다.

```json
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

이벤트 데이터(프로필 속성 없음)만 포함하는 내보내기 작업을 만들려면 페이로드가 다음과 유사할 수 있습니다.

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields": {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": false
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }
```

### 세그먼트 내보내기

내보내기 작업 종단점을 사용하여 대신 대상 세그먼트를 내보낼 수도 있습니다 [!DNL Profile] 데이터. 다음 안내서를 참조하십시오. [세분화 API에서 작업 내보내기](../../segmentation/api/export-jobs.md) 추가 정보.
