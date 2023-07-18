---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 프로필 내보내기 작업 API 끝점
type: Documentation
description: 실시간 고객 프로필을 사용하면 속성 데이터와 행동 데이터를 모두 포함하여 여러 소스의 데이터를 함께 가져와서 Adobe Experience Platform 내의 개별 고객에 대한 단일 보기를 구축할 수 있습니다. 그런 다음 프로필 데이터를 데이터 세트로 내보내 추가 처리할 수 있습니다.
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 2%

---

# 프로필 내보내기 작업 엔드포인트

[!DNL Real-Time Customer Profile] 속성 데이터와 행동 데이터를 모두 포함하여 여러 소스의 데이터를 통합하여 개별 고객에 대한 단일 뷰를 구축할 수 있습니다. 그런 다음 프로필 데이터를 데이터 세트로 내보내 추가 처리할 수 있습니다. 예를 들어, [!DNL Profile] 대상자를 만들어 활성화를 위해 데이터를 내보내고 보고를 위해 프로필 속성을 내보낼 수 있습니다.

이 문서에서는 다음을 사용하여 내보내기 작업을 만들고 관리하는 단계별 지침을 제공합니다. [프로필 API](https://www.adobe.com/go/profile-apis-en).

>[!NOTE]
>
>이 안내서에서는 의 내보내기 작업 사용에 대해 설명합니다. [!DNL Profile API]. Adobe Experience Platform 세그멘테이션 서비스의 내보내기 작업을 관리하는 방법에 대한 자세한 내용은 [세분화 API의 작업 내보내기](../../profile/api/export-jobs.md).

내보내기 작업을 생성하는 것 외에도 [!DNL Profile] 를 사용하는 데이터 `/entities` 끝점(&quot;이라고도 함)[!DNL Profile Access]&quot;. 다음을 참조하십시오. [엔티티 끝점 안내서](./entities.md) 추가 정보. 에 액세스하는 방법에 대한 단계 [!DNL Profile] ui를 사용하는 데이터는 [사용 안내서](../ui/user-guide.md).

## 시작하기

이 안내서에 사용된 API 엔드포인트는 [!DNL Real-Time Customer Profile] API. 계속하기 전에 다음을 검토하십시오. [시작 안내서](getting-started.md) 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기에 대한 안내서 및 를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보 [!DNL Experience Platform] API.

## 내보내기 작업 만들기

내보내기 [!DNL Profile] 데이터를 사용하려면 먼저 데이터를 내보낼 데이터 세트를 만든 다음 새 내보내기 작업을 시작해야 합니다. 두 단계 모두 Experience Platform API를 사용하여 수행할 수 있습니다. 전자는 카탈로그 서비스 API를 사용하고 후자는 실시간 고객 프로필 API를 사용합니다. 각 단계를 완료하기 위한 자세한 지침은 다음 섹션에 설명되어 있습니다.

### 타겟 데이터 세트 만들기

내보낼 때 [!DNL Profile] 데이터. 먼저 대상 데이터 세트를 만들어야 합니다. 내보내기가 성공하도록 데이터 세트를 올바르게 구성해야 합니다.

주요 고려 사항 중 하나는 데이터 세트의 기반이 되는 스키마 입니다(`schemaRef.id` (아래 API 샘플 요청). 프로필 데이터를 내보내려면 데이터 세트가 [!DNL XDM Individual Profile] 유니온 스키마 (`https://ns.adobe.com/xdm/context/profile__union`). 유니온 스키마는 동일한 클래스를 공유하는 스키마의 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 이 경우 [!DNL XDM Individual Profile] 클래스. 유니온 보기 스키마에 대한 자세한 내용은 다음을 참조하십시오. [스키마 컴포지션 기본 사항 안내서의 유니온 섹션](../../xdm/schema/composition.md#union).

이 자습서의 다음 단계에서는 다음을 참조하는 데이터 세트를 만드는 방법을 간략하게 설명합니다. [!DNL XDM Individual Profile] 유니온 스키마 사용 [!DNL Catalog] API. 다음을 사용할 수도 있습니다 [!DNL Platform] 유니온 스키마를 참조하는 데이터 세트를 만드는 사용자 인터페이스입니다. UI 사용 단계는에 설명되어 있습니다. [대상자 내보내기를 위한 이 UI 튜토리얼](../../segmentation/tutorials/create-dataset-export-segment.md) 하지만 여기서도 적용 가능합니다. 완료되면 이 자습서로 돌아가 의 단계를 진행할 수 있습니다. [새 내보내기 작업 시작](#initiate).

이미 호환되는 데이터 세트가 있고 해당 ID를 알고 있는 경우 다음 단계로 직접 진행할 수 있습니다. [새 내보내기 작업 시작](#initiate).

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
| `schemaRef.id` | 데이터 세트와 연결할 유니온 뷰(스키마)의 ID입니다. |

**응답**

성공한 응답은 새로 만든 데이터 세트의 읽기 전용, 시스템 생성 고유 ID가 포함된 배열을 반환합니다. 프로필 데이터를 내보내려면 제대로 구성된 데이터 세트 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 내보내기 작업 시작 {#initiate}

결합을 유지하는 데이터 세트가 있으면 POST에 요청을 하여 프로필 데이터를 데이터 세트에 유지하는 내보내기 작업을 생성할 수 있습니다. `/export/jobs` 실시간 고객 프로필 API의 끝점으로, 요청 본문에 내보낼 데이터의 세부 정보를 제공합니다.

**API 형식**

```http
POST /export/jobs
```

**요청**

다음 요청은 페이로드에 구성 매개 변수를 제공하는 새 내보내기 작업을 만듭니다.

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
| `fields` | *(선택 사항)* 내보내기에 포함될 데이터 필드를 이 매개변수에 제공된 필드로만 제한합니다. 이 값을 생략하면 내보낸 데이터에 모든 필드가 포함됩니다. |
| `mergePolicy` | *(선택 사항)* 내보낸 데이터를 제어하는 병합 정책을 지정합니다. 내보내는 대상이 여러 개 있는 경우 이 매개 변수를 포함하십시오. |
| `mergePolicy.id` | 병합 정책의 ID입니다. |
| `mergePolicy.version` | 사용할 병합 정책의 특정 버전입니다. 이 값을 생략하면 기본적으로 최신 버전이 사용됩니다. |
| `additionalFields.eventList` | *(선택 사항)* 다음 설정 중 하나 이상을 제공하여 하위 객체 또는 연관된 객체에 대해 내보낸 시계열 이벤트 필드를 제어합니다.<ul><li>`eventList.fields`: 내보낼 필드를 제어합니다.</li><li>`eventList.filter`: 연결된 오브젝트에서 포함된 결과를 제한하는 기준을 지정합니다. 내보내기에 필요한 최소값(일반적으로 날짜)이 필요합니다.</li><li>`eventList.filter.fromIngestTimestamp`: 시계열 이벤트를 제공된 타임스탬프 후 수집된 이벤트로 필터링합니다. 이는 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다.</li></ul> |
| `destination` | **(필수)** 내보낸 데이터의 대상 정보:<ul><li>`destination.datasetId`: **(필수)** 데이터를 내보낼 데이터 세트의 ID입니다.</li><li>`destination.segmentPerBatch`: *(선택 사항)* 제공하지 않을 경우 기본값이 로 설정되는 부울 값 `false`. 값 `false` 모든 세그먼트 정의 ID를 단일 배치 ID로 내보냅니다. 값 `true` 하나의 세그먼트 정의 ID를 하나의 배치 ID로 내보냅니다. 값을 로 설정하는 것에 유의하십시오. `true` 일괄 내보내기 성능에 영향을 줄 수 있습니다.</li></ul> |
| `schema.name` | **(필수)** 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |

>[!NOTE]
>
>프로필 데이터만 내보내고 관련 시계열 데이터는 포함하지 않으려면 요청에서 &quot;additionalFields&quot; 개체를 제거하십시오.

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

에 대한 GET 요청을 수행하여 특정 조직에 대한 모든 내보내기 작업 목록을 반환할 수 있습니다. `export/jobs` 엔드포인트. 이 요청은 쿼리 매개 변수도 지원합니다 `limit` 및 `offset`아래에 표시된 대로 를 클릭합니다.

**API 형식**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `start` | 요청의 생성 시간에 따라 반환된 결과 페이지를 오프셋합니다. 예: `start=4` |
| `limit` | 반환되는 결과 수를 제한합니다. 예: `limit=10` |
| `page` | 요청 생성 시간에 따라 결과의 특정 페이지를 반환합니다. 예: `page=2` |
| `sort` | 특정 필드를 기준으로 오름차순으로 결과 정렬( **`asc`** ) 또는 내림차순( **`desc`** ) 순서. 여러 결과 페이지를 반환할 때 정렬 매개 변수가 작동하지 않습니다. 예: `sort=updateTime:asc` |

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

응답에는 다음이 포함됩니다. `records` 조직에서 생성한 내보내기 작업이 포함된 객체입니다.

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

## 내보내기 진행 상황 모니터링

GET 특정 내보내기 작업의 세부 정보를 보거나 처리할 때 해당 상태를 모니터링하려면 다음을 요청할 수 있습니다. `/export/jobs` 끝점 및 포함 `id` 경로의 내보내기 작업. 내보내기 작업이 완료되면 다음과 같은 작업이 완료됩니다. `status` 필드는 &quot;SUCCEEDED&quot; 값을 반환합니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 다음 `id` 에 대해 설명합니다. |

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
| `batchId` | 프로필 데이터를 읽을 때 조회 목적으로 사용할 성공적인 내보내기로 생성된 일괄 처리의 식별자입니다. |

## 내보내기 작업 취소

Experience Platform을 사용하면 기존 내보내기 작업을 취소할 수 있습니다. 이 작업은 내보내기 작업이 완료되지 않았거나 처리 단계에서 중단된 경우 등 여러 가지 이유로 유용할 수 있습니다. 내보내기 작업을 취소하려면에 대한 DELETE 요청을 수행할 수 있습니다. `/export/jobs` 끝점 및 포함 `id` 요청 경로로 취소할 내보내기 작업의 이름입니다.

**API 형식**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 다음 `id` 에 대해 설명합니다. |

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

성공적인 삭제 요청은 취소 작업이 성공했음을 나타내는 HTTP 상태 204(컨텐츠 없음)와 빈 응답 본문을 반환합니다.

## 다음 단계

내보내기가 완료되면 Experience Platform의 데이터 레이크 내에서 데이터를 사용할 수 있습니다. 그런 다음 를 사용할 수 있습니다. [데이터 액세스 API](https://www.adobe.io/experience-platform-apis/references/data-access/) 을 사용하여 데이터에 액세스 `batchId` 내보내기와 연결되었습니다. 내보내기의 크기에 따라 데이터가 청크 단위로 제공될 수 있으며 배치는 여러 파일로 구성될 수 있습니다.

데이터 액세스 API를 사용하여 배치 파일에 액세스하고 다운로드하는 방법에 대한 단계별 지침은 다음을 따르십시오. [데이터 액세스 자습서](../../data-access/tutorials/dataset-data.md).

Adobe Experience Platform 쿼리 서비스를 사용하여 성공적으로 내보낸 실시간 고객 프로필 데이터에 액세스할 수도 있습니다. UI 또는 RESTful API를 사용하여 쿼리 서비스를 사용하면 데이터 레이크 내의 데이터에 대해 쿼리를 작성, 유효성 검사 및 실행할 수 있습니다.

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 [쿼리 서비스 설명서](../../query-service/home.md).

## 부록

다음 섹션에는 프로필 API의 내보내기 작업에 대한 추가 정보가 포함되어 있습니다.

### 추가 내보내기 페이로드 예

의 섹션에 표시된 예제 API 호출 [내보내기 작업 시작](#initiate) 프로필(레코드) 및 이벤트(시계열) 데이터를 모두 포함하는 작업을 만듭니다. 이 섹션에서는 하나의 데이터 유형 또는 다른 데이터 유형을 포함하도록 내보내기를 제한하는 추가 요청 페이로드 예를 제공합니다.

다음 페이로드는 프로필 데이터만 포함하는 내보내기 작업을 만듭니다(이벤트 없음).

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

이벤트 데이터만 포함하는 내보내기 작업(프로필 속성 없음)을 만들려면 페이로드는 다음과 유사할 수 있습니다.

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

### 대상자 내보내기

내보내기 작업 끝점을 사용하여 대상자를 내보내는 대신 [!DNL Profile] 데이터. 다음 안내서를 참조하십시오 [세분화 API의 작업 내보내기](../../segmentation/api/export-jobs.md) 추가 정보.
