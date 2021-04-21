---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 내보내기 작업 API 끝점
topic-legacy: guide
type: Documentation
description: 실시간 고객 프로파일을 사용하면 속성 데이터와 행동 데이터를 비롯한 다양한 소스의 데이터를 취합하여 Adobe Experience Platform 내에서 개별 고객에 대한 단일 뷰를 구축할 수 있습니다. 이후 처리를 위해 프로필 데이터를 데이터 세트로 내보낼 수 있습니다.
exl-id: d51b1d1c-ae17-4945-b045-4001e4942b67
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 2%

---

# 내보내기 작업 끝점

[!DNL Real-time Customer Profile] 속성 데이터와 행동 데이터를 모두 비롯한 다양한 소스에서 데이터를 취합하여 개별 고객에 대한 단일 뷰를 구축할 수 있습니다. 이후 처리를 위해 프로필 데이터를 데이터 세트로 내보낼 수 있습니다. 예를 들어 [!DNL Profile] 데이터의 대상 세그먼트를 활성화하도록 내보낼 수 있으며, 프로필 속성을 보고를 위해 내보낼 수 있습니다.

이 문서에서는 [프로필 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)를 사용하여 내보내기 작업을 만들고 관리하기 위한 단계별 지침을 제공합니다.

>[!NOTE]
>
>이 안내서에서는 [!DNL Profile API]에서 내보내기 작업 사용에 대해 설명합니다. Adobe Experience Platform 세그멘테이션 서비스에 대한 내보내기 작업을 관리하는 방법에 대한 자세한 내용은 세그멘테이션 API](../../profile/api/export-jobs.md)의 [내보내기 작업에 대한 안내서를 참조하십시오.

내보내기 작업을 만드는 것 외에도 `/entities` 끝점(&quot;[!DNL Profile Access]&quot;라고도 함)을 사용하여 [!DNL Profile] 데이터에 액세스할 수도 있습니다. 자세한 내용은 [개체 끝점 안내서](./entities.md)를 참조하십시오. UI를 사용하여 [!DNL Profile] 데이터에 액세스하는 방법에 대한 단계는 [사용자 안내서](../ui/user-guide.md)를 참조하십시오.

## 시작하기

이 안내서에 사용된 API 끝점은 [!DNL Real-time Customer Profile] API의 일부입니다. 계속하기 전에 [시작하기 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 내보내기 작업 만들기

[!DNL Profile] 데이터를 내보내려면 먼저 데이터를 내보낼 데이터 세트를 만든 다음 새 내보내기 작업을 시작해야 합니다. 이러한 두 단계 모두 Experience Platform API를 사용하여 수행할 수 있으며, 이전에 카탈로그 서비스 API를 사용한 단계 및 실시간 고객 프로필 API를 사용한 단계 중 하나를 사용할 수 있습니다. 각 단계를 완료하기 위한 자세한 지침은 다음 섹션에 요약되어 있습니다.

### 대상 데이터 세트 만들기

[!DNL Profile] 데이터를 내보낼 때 먼저 대상 데이터 세트를 만들어야 합니다. 내보내기가 성공하도록 데이터 세트를 올바르게 구성해야 합니다.

중요 고려 사항 중 하나는 데이터 세트가 기반이 되는 스키마(아래 API 샘플 요청에서 `schemaRef.id`)입니다. 프로필 데이터를 내보내려면 데이터 집합은 [!DNL XDM Individual Profile] 조합 스키마(`https://ns.adobe.com/xdm/context/profile__union`)를 기반으로 해야 합니다. 공용 스키마는 동일한 클래스를 공유하는 스키마 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 이 경우 이 클래스는 [!DNL XDM Individual Profile] 클래스입니다. 조합 보기 스키마에 대한 자세한 내용은 스키마 구성 안내서](../../xdm/schema/composition.md#union)의 기본 사항에 있는 [union 섹션을 참조하십시오.

이 자습서의 다음 단계는 [!DNL Catalog] API를 사용하여 [!DNL XDM Individual Profile] 결합 스키마를 참조하는 데이터 세트를 만드는 방법에 대해 설명합니다. 또한 [!DNL Platform] 사용자 인터페이스를 사용하여 조합 스키마를 참조하는 데이터 세트를 만들 수도 있습니다. UI 사용 단계는 세그먼트 내보내기](../../segmentation/tutorials/create-dataset-export-segment.md)에 대한 [이 UI 자습서에 요약되어 있지만 여기에도 적용됩니다. 완료되면 이 튜토리얼로 돌아가 [새 내보내기 작업](#initiate)을 시작하는 단계를 진행할 수 있습니다.

이미 호환되는 데이터 세트가 있고 해당 ID를 알고 있는 경우 [새 내보내기 작업](#initiate)을 시작하는 단계로 직접 진행할 수 있습니다.

**API 형식**

```http
POST /dataSets
```

**요청**

다음 요청은 페이로드에서 구성 매개 변수를 제공하는 새 데이터 세트를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Profile Data Export",
        "schemaRef": {
          "id": "https://ns.adobe.com/xdm/context/profile__union",
          "contentType": "application/vnd.adobe.xed+json;version=1"
        },
        "fileDescription": {
          "persisted": true
        }
      }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 데이터 세트에 대한 설명형 이름입니다. |
| `schemaRef.id` | 데이터 집합과 연결할 통합 보기(스키마)의 ID입니다. |
| `fileDescription.persisted` | `true`으로 설정하면 데이터 세트가 조합 보기에서 유지될 수 있도록 하는 부울 값입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트의 읽기 전용, 시스템 생성, 고유 ID가 포함된 배열을 반환합니다. 프로필 데이터를 성공적으로 내보내려면 제대로 구성된 데이터 집합 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 내보내기 작업 시작 {#initiate}

조합 지속 데이터 집합이 있으면 실시간 고객 프로필 API의 `/export/jobs` 끝점에 POST 요청을 만들고 요청 본문에 내보낼 데이터의 세부 정보를 제공하여 프로필 데이터를 데이터 집합에 유지하는 내보내기 작업을 만들 수 있습니다.

**API 형식**

```http
POST /export/jobs
```

**요청**

다음 요청은 페이로드에서 구성 매개 변수를 제공하는 새 내보내기 작업을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
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
| `mergePolicy` | *(선택 사항)* 내보낸 데이터를 제어하는 병합 정책을 지정합니다. 내보낼 세그먼트가 여러 개인 경우 이 매개 변수를 포함하십시오. |
| `mergePolicy.id` | 병합 정책의 ID. |
| `mergePolicy.version` | 사용할 병합 정책의 특정 버전입니다. 이 값을 생략하면 기본적으로 최신 버전이 사용됩니다. |
| `additionalFields.eventList` | *(선택 사항)* 다음 설정 중 하나 이상을 제공하여 하위 또는 연결된 개체에 대해 내보낸 시계열 이벤트 필드를 제어합니다.<ul><li>`eventList.fields`:내보낼 필드를 제어합니다.</li><li>`eventList.filter`:관련 개체에서 포함된 결과를 제한하는 기준을 지정합니다. 내보내기에 필요한 최소 값(일반적으로 날짜)을 예상합니다.</li><li>`eventList.filter.fromIngestTimestamp`:시간 시리즈 이벤트를 제공된 타임스탬프 이후에 인제스트된 이벤트로 필터링합니다. 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다.</li></ul> |
| `destination` | **(필수)** 내보낸 데이터에 대한 대상 정보:<ul><li>`destination.datasetId`: **(필수)** 데이터를 내보낼 데이터 세트의 ID입니다.</li><li>`destination.segmentPerBatch`: *(선택 사항)* 제공되지 않을 경우 기본적으로 제공되는 부울 값입니다 `false`. `false` 값은 모든 세그먼트 ID를 단일 배치 ID로 내보냅니다. `true` 값은 하나의 세그먼트 ID를 하나의 배치 ID로 내보냅니다. 값을 `true`으로 설정하면 일괄 내보내기 성능에 영향을 줄 수 있습니다.</li></ul> |
| `schema.name` | **(필수)** 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |

>[!NOTE]
>
>프로필 데이터만 내보내고 관련 시계열 데이터를 포함하지 않으려면 요청에서 &quot;additionalFields&quot; 개체를 제거합니다.

**응답**

성공적인 응답은 요청에 지정된 프로필 데이터로 채워진 데이터 세트를 반환합니다.

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
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

## 모든 내보내기 작업 나열

특정 IMS에 대한 모든 내보내기 작업 목록을 반환할 수 있습니다. 조직은 `export/jobs` 끝점에 GET 요청을 수행하여 이 목록을 반환합니다. 요청도 아래와 같이 쿼리 매개 변수 `limit` 및 `offset`를 지원합니다.

**API 형식**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `start` | 요청의 만들기 시간에 따라 반환된 결과 페이지를 오프셋합니다. 예: `start=4` |
| `limit` | 반환된 결과 수를 제한합니다. 예: `limit=10` |
| `page` | 요청의 만들기 시간에 따라 특정 결과 페이지를 반환합니다. 예: `page=2` |
| `sort` | 결과를 오름차순( **`asc`** ) 또는 내림차순( **`desc`** )으로 특정 필드별로 정렬합니다. 여러 결과 페이지를 반환할 때는 정렬 매개 변수가 작동하지 않습니다. 예: `sort=updateTime:asc` |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

응답에는 IMS 조직에서 만든 내보내기 작업이 포함된 `records` 개체가 포함됩니다.

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
      "imsOrgId": "{IMS_ORG}",
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
      "imsOrgId": "{IMS_ORG}",
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

## 내보내기 진행 상태 모니터링

특정 내보내기 작업의 세부 사항을 보거나 진행 상태를 모니터링하려면 `/export/jobs` 끝점에 GET 요청을 하고 해당 경로에 내보내기 작업의 `id`을 포함할 수 있습니다. `status` 필드가 &quot;SUCCEEDED&quot; 값을 반환하면 내보내기 작업이 완료됩니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 액세스하려는 내보내기 작업의 `id`. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": false,
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `batchId` | 프로파일 데이터를 읽을 때 조회 목적으로 사용될 성공적인 내보내기에서 생성된 배치의 식별자입니다. |

## 내보내기 작업 취소

Experience Platform을 사용하면 기존 내보내기 작업을 취소할 수 있습니다. 이 작업은 내보내기 작업이 완료되지 않았거나 처리 단계에 고정되었는지 등 다양한 이유로 유용할 수 있습니다. 내보내기 작업을 취소하려면 `/export/jobs` 끝점에 대한 DELETE 요청을 수행하고 요청 경로로 취소할 내보내기 작업의 `id`을(를) 포함할 수 있습니다.

**API 형식**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 액세스하려는 내보내기 작업의 `id`. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs/726 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

삭제 요청이 성공하면 취소 작업이 성공했음을 나타내는 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문을 반환합니다.

## 다음 단계

내보내기가 성공적으로 완료되면 Experience Platform의 Data Lake 내에서 데이터를 사용할 수 있습니다. 그런 다음 [데이터 액세스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)를 사용하여 내보내기와 연결된 `batchId`을 사용하여 데이터에 액세스할 수 있습니다. 내보내기 크기에 따라 데이터가 청크 단위일 수 있으며 일괄 처리는 여러 파일로 구성될 수 있습니다.

데이터 액세스 API를 사용하여 일괄 파일에 액세스하고 다운로드하는 방법에 대한 단계별 지침을 보려면 [데이터 액세스 자습서](../../data-access/tutorials/dataset-data.md)를 따르십시오.

Adobe Experience Platform 쿼리 서비스를 사용하여 실시간 고객 프로필 데이터를 성공적으로 내보낼 수도 있습니다. UI 또는 RESTful API를 사용하여 쿼리 서비스를 사용하여 데이터 레이크 내의 데이터에 대한 쿼리를 작성, 유효성 확인 및 실행할 수 있습니다.

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 [쿼리 서비스 문서](../../query-service/home.md)를 참조하십시오.

## 부록

다음 섹션에는 프로필 API의 내보내기 작업에 대한 추가 정보가 들어 있습니다.

### 추가 내보내기 페이로드 예

[내보내기 작업 시작 섹션에 표시된 예제 API 호출은 프로필(레코드) 데이터와 이벤트(시간 시리즈) 데이터가 모두 포함된 작업을 만듭니다. ](#initiate) 이 섹션에서는 내보내기를 하나의 데이터 유형이나 다른 데이터 유형으로 제한하기 위한 추가 요청 페이로드 예를 제공합니다.

다음 페이로드에서는 프로필 데이터(이벤트 없음)만 포함하는 내보내기 작업을 만듭니다.

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

이벤트 데이터(프로필 특성 없음)만 포함하는 내보내기 작업을 만들려면 페이로드가 다음과 유사할 수 있습니다.

```json
{
    "fields": "identityMap",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "additionalFields" : {
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

내보내기 작업 끝점을 사용하여 [!DNL Profile] 데이터 대신 대상 세그먼트를 내보낼 수도 있습니다. 자세한 내용은 세그멘테이션 API](../../segmentation/api/export-jobs.md)의 [내보내기 작업에 대한 안내서를 참조하십시오.
