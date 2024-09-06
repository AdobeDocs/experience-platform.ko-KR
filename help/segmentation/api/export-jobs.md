---
solution: Experience Platform
title: 세그먼트 내보내기 작업 API 끝점
description: 내보내기 작업은 대상 세그먼트 구성원을 데이터 세트로 지속하는 데 사용되는 비동기 프로세스입니다. Adobe Experience Platform Segmentation Service API에서 /export/jobs 끝점을 사용하여 내보내기 작업을 프로그래밍 방식으로 검색, 생성 및 취소할 수 있습니다.
role: Developer
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 1%

---

# 세그먼트 내보내기 작업 엔드포인트

내보내기 작업은 대상 세그먼트 구성원을 데이터 세트로 지속하는 데 사용되는 비동기 프로세스입니다. Adobe Experience Platform Segmentation API에서 내보내기 작업을 프로그래밍 방식으로 검색, 만들기 및 취소할 수 있는 `/export/jobs` 끝점을 사용할 수 있습니다.

>[!NOTE]
>
>이 안내서에서는 [!DNL Segmentation API]에서 내보내기 작업을 사용하는 방법에 대해 설명합니다. [!DNL Real-Time Customer Profile] 데이터의 내보내기 작업을 관리하는 방법에 대한 자세한 내용은 프로필 API의 [내보내기 작업](../../profile/api/export-jobs.md)에 대한 안내서를 참조하십시오.

## 시작하기

이 가이드에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 내보내기 작업 목록 검색 {#retrieve-list}

`/export/jobs` 끝점에 대한 GET 요청을 수행하여 조직에 대한 모든 내보내기 작업 목록을 검색할 수 있습니다.

**API 형식**

`/export/jobs` 끝점은 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 값비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 내보내기 작업을 검색합니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다.

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

**쿼리 매개 변수**

+++ 사용 가능한 쿼리 매개 변수 목록입니다.

| 매개변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `limit` | 반환된 내보내기 작업 수를 지정합니다. | `limit=10` |
| `offset` | 결과 페이지의 오프셋을 지정합니다. | `offset=1540974701302_96` |
| `status` | 상태를 기반으로 결과를 필터링합니다. 지원되는 값은 &quot;NEW&quot;, &quot;SUCCEEDED&quot; 및 &quot;FAILED&quot;입니다. | `status=NEW` |

+++

**요청**

다음 요청은 조직 내에서 마지막 두 개의 내보내기 작업을 검색합니다.

+++ 내보내기 작업을 검색하는 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

다음 응답은 요청 경로에 제공된 쿼리 매개 변수를 기반으로 성공적으로 완료된 내보내기 작업 목록과 함께 HTTP 상태 200을 반환합니다.

+++ 내보내기 작업을 검색할 때의 샘플 응답입니다.

```json
{
    "records": [
        {
            "id": 100,
            "jobType": "BATCH",
            "destination": {
                "datasetId": "5b7c86968f7b6501e21ba9df",
                "segmentPerBatch": false,
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
            },
            "fields": "identities.id,personalEmail.address",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "status": "SUCCEEDED",
            "filter": {
                "segments": [
                    {
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "ups",
                        "status": [
                            "realized"
                        ]
                    }
                ]
            },
            "mergePolicy": {
                "id": "timestampOrdered-none-mp",
                "version": 1
            },
            "profileInstanceId": "ups",
            "errors": [
                {
                    "code": "0100000003",
                    "msg": "Error in Export Job",
                    "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger"
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "profileExportTime": {
                    "startTimeInMs": 123456789000,
                    "endTimeInMs": 123456799000,
                    "totalTimeInMs": 10000
                },
                "totalExportedProfileCounter": 20,
                "exportedProfileByNamespaceCounter": {
                    "namespace1": 10,
                    "namespace2": 5
                }
            },
            "computeGatewayJobId": {
                "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
            },
            "creationTime": 1538615973895,
            "updateTime": 1538616233239,
            "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
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
                        "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                        "segmentNs": "AAM",
                        "status": ["realized"]
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
                "segmentPerBatch": false,
                "batchId": "IWEQ6920712f9475762D"
            },
            "updateTime": 1538573922551,
            "imsOrgId": "1BD6382559DF0C130A49422D@AdobeOrg",
            "creationTime": 1538573416687
        }
    ],
    "page":{
        "sortField": "createdTime",
        "sort": "desc",
        "pageOffset": "1540974701302_96",
        "pageSize": 2
    },
    "link":{
        "next": "/export/jobs/?limit=2&offset=1538573416687_722"
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `destination` | 내보낸 데이터의 대상 정보:<ul><li>`datasetId`: 데이터를 내보낸 데이터 세트의 ID입니다.</li><li>`segmentPerBatch`: 세그먼트 ID의 통합 여부를 보여 주는 부울 값입니다. 값이 &quot;false&quot;이면 모든 세그먼트 ID를 단일 배치 ID로 내보내는 것을 의미합니다. 값이 &quot;true&quot;이면 하나의 세그먼트 ID를 하나의 배치 ID로 내보내는 것을 의미합니다. **참고:** 값을 true로 설정하면 일괄 내보내기 성능에 영향을 줄 수 있습니다.</li></ul> |
| `fields` | 내보낸 필드의 목록(쉼표로 구분됨). |
| `schema.name` | 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |
| `filter.segments` | 내보내는 세그먼트입니다. 다음 필드가 포함되어 있습니다.<ul><li>`segmentId`: 프로필을 내보낼 세그먼트 ID입니다.</li><li>`segmentNs`: 지정된 `segmentID`에 대한 세그먼트 네임스페이스입니다.</li><li>`status`: `segmentID`에 대한 상태 필터를 제공하는 문자열 배열입니다. 기본적으로 `status`은(는) 현재 시간에 세그먼트에 속하는 모든 프로필을 나타내는 값 `["realized"]`을(를) 갖습니다. 가능한 값은 `realized` 및 `exited`입니다. `realized` 값은 프로필이 세그먼트에 적합함을 의미합니다. 값이 `exiting`이면 프로필이 세그먼트를 종료하는 것입니다.</li></ul> |
| `mergePolicy` | 내보낸 데이터에 대한 병합 정책 정보. |
| `metrics.totalTime` | 내보내기 작업을 실행하는 데 걸린 총 시간을 나타내는 필드입니다. |
| `metrics.profileExportTime` | 프로필을 내보내는 데 걸린 시간을 나타내는 필드. |
| `page` | 요청한 내보내기 작업의 페이지 매김에 대한 정보입니다. |
| `link.next` | 내보내기 작업의 다음 페이지에 대한 링크입니다. |

+++

## 새 내보내기 작업 만들기 {#create}

`/export/jobs` 끝점에 대한 POST 요청을 수행하여 새 내보내기 작업을 만들 수 있습니다.

**API 형식**

```http
POST /export/jobs
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 내보내기 작업을 만듭니다.

+++ 내보내기 작업 생성에 대한 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "string",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z",
                "toIngestTimestamp": "2020-01-01T00:00:00Z"
            }
        }
    },
    "destination":{
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false
    },
    "schema":{
        "name": "_xdm.context.profile"
    },
    "evaluationInfo": {
        "segmentation": true
    }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `fields` | 내보낸 필드의 목록(쉼표로 구분됨). 비워 두면 모든 필드가 내보내집니다. |
| `mergePolicy` | 내보낸 데이터를 제어하는 병합 정책을 지정합니다. 내보낼 세그먼트가 여러 개 있는 경우 이 매개 변수를 포함합니다. 제공하지 않은 경우 내보내기는 지정된 세그먼트와 동일한 병합 정책을 사용합니다. |
| `filter` | 아래 나열된 하위 속성에 따라 ID, 선별 시간 또는 수집 시간별로 내보내기 작업에 포함될 세그먼트를 지정하는 개체입니다. 비워 두면 모든 데이터가 내보내집니다. |
| `filter.segments` | 내보낼 세그먼트를 지정합니다. 이 값을 생략하면 모든 프로필의 모든 데이터를 내보냅니다. 각각 다음 필드가 포함된 세그먼트 오브젝트 배열을 허용합니다.<ul><li>`segmentId`: **(`segments`을(를) 사용하는 경우 필수)** 프로필을 내보낼 세그먼트 ID입니다.</li><li>지정된 `segmentID`에 대한 `segmentNs` *(선택 사항)* 세그먼트 네임스페이스입니다.</li><li>`status` *(선택 사항)* `segmentID`에 대한 상태 필터를 제공하는 문자열 배열입니다. 기본적으로 `status`은(는) 현재 시간에 세그먼트에 속하는 모든 프로필을 나타내는 값 `["realized"]`을(를) 갖습니다. 가능한 값은 `realized` 및 `exited`입니다.  `realized` 값은 프로필이 세그먼트에 적합함을 의미합니다. 값이 `exiting`이면 프로필이 세그먼트를 종료하는 것입니다.</li></ul> |
| `filter.segmentQualificationTime` | 세그먼트 선별 시간을 기반으로 필터링합니다. 시작 시간 및/또는 종료 시간이 제공될 수 있습니다. |
| `filter.segmentQualificationTime.startTime` | 주어진 상태에 대한 세그먼트 ID의 세그먼트 자격 시작 시간입니다. 제공되지 않으면 세그먼트 ID 자격에 대한 시작 시간에 필터가 없습니다. 타임스탬프는 [RFC 3339](https://tools.ietf.org/html/rfc3339) 형식으로 제공해야 합니다. |
| `filter.segmentQualificationTime.endTime` | 주어진 상태에 대한 세그먼트 ID의 세그먼트 자격 종료 시간. 제공되지 않으면 세그먼트 ID 자격에 대한 종료 시간에 대한 필터가 없습니다. 타임스탬프는 [RFC 3339](https://tools.ietf.org/html/rfc3339) 형식으로 제공해야 합니다. |
| `filter.fromIngestTimestamp ` | 내보낸 프로필은 이 타임스탬프 이후에 업데이트된 프로필만 포함하도록 제한됩니다. 타임스탬프는 [RFC 3339](https://tools.ietf.org/html/rfc3339) 형식으로 제공해야 합니다. <ul><li>**프로필**&#x200B;에 대한 `fromIngestTimestamp`(제공된 경우): 병합된 업데이트된 타임스탬프가 지정된 타임스탬프보다 큰 병합된 모든 프로필을 포함합니다. `greater_than` 피연산자 지원.</li><li>**이벤트**&#x200B;에 대한 `fromIngestTimestamp`: 이 타임스탬프 이후에 수집된 모든 이벤트는 결과 프로필 결과에 따라 내보내집니다. 이는 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다.</li> |
| `filter.emptyProfiles` | 빈 프로필을 필터링할지 여부를 나타내는 부울 값입니다. 프로필에는 프로필 레코드, ExperienceEvent 레코드 또는 둘 다를 포함할 수 있습니다. 프로필 레코드가 없고 ExperienceEvent 레코드만 있는 프로필을 &quot;emptyProfiles&quot;라고 합니다. &quot;emptyProfiles&quot;를 포함하여 프로필 저장소의 모든 프로필을 내보내려면 `emptyProfiles` 값을 `true`(으)로 설정하십시오. `emptyProfiles`이(가) `false`(으)로 설정된 경우 저장소에 프로필 레코드가 있는 프로필만 내보내집니다. 기본적으로 `emptyProfiles` 특성이 포함되지 않으면 프로필 레코드가 포함된 프로필만 내보내집니다. |
| `additionalFields.eventList` | 다음 설정 중 하나 이상을 제공하여 하위 객체 또는 연관된 객체에 대해 내보낸 시계열 이벤트 필드를 제어합니다.<ul><li>`fields`: 내보낼 필드를 제어합니다.</li><li>`filter`: 연결된 개체에서 포함된 결과를 제한하는 조건을 지정합니다. 내보내기에 필요한 최소값(일반적으로 날짜)이 필요합니다.</li><li>`filter.fromIngestTimestamp`: 제공된 타임스탬프 후에 수집된 시계열 이벤트를 필터링합니다. 이는 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다.</li><li>`filter.toIngestTimestamp`: 제공된 타임스탬프 전에 수집된 타임스탬프를 필터링합니다. 이는 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다.</li></ul> |
| `destination` | **(필수)** 내보낸 데이터에 대한 정보:<ul><li>`datasetId`: **(필수)** 데이터를 내보낼 데이터 집합의 ID입니다.</li><li>`segmentPerBatch`: *(선택 사항)* 제공되지 않을 경우 기본값이 &quot;false&quot;인 부울 값입니다. 값이 &quot;false&quot;이면 모든 세그먼트 ID가 단일 배치 ID로 내보내집니다. 값이 &quot;true&quot;이면 하나의 세그먼트 ID를 하나의 배치 ID로 내보냅니다. 값을 &quot;true&quot;로 설정하면 일괄 내보내기 성능이 영향을 받을 수 있습니다.</li></ul> |
| `schema.name` | **(필수)** 데이터를 내보낼 데이터 세트와 연결된 스키마 이름입니다. |
| `evaluationInfo.segmentation` | *(선택 사항)* 제공되지 않을 경우 기본값은 `false`인 부울 값입니다. `true` 값은 내보내기 작업에서 세그먼테이션을 수행해야 함을 나타냅니다. |

+++

**응답**

성공한 응답은 새로 생성된 내보내기 작업의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 내보내기 작업 생성 시 샘플 응답.

```json
{
    "id": 100,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "NEW",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status": [
                    "realized"
                ]
            }
        ],
        "segmentQualificationTime": {
            "startTime": "2018-01-01T00:00:00Z",
            "endTime": "2018-02-01T00:00:00Z"
        },
        "fromIngestTimestamp": "2018-01-01T00:00:00Z",
        "emptyProfiles": true
    },
    "additionalFields": {
        "eventList": {
            "fields": "_id, _experience",
            "filter": {
                "fromIngestTimestamp": "2018-01-01T00:00:00Z"
            }
        }
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
        }
    },
    "computeGatewayJobId": {
        "exportJob": ""    
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 방금 만든 내보내기 작업을 식별하는 시스템 생성 읽기 전용 값입니다. |

또는 `destination.segmentPerBatch`이(가) `true`(으)로 설정된 경우 위의 `destination` 개체는 아래와 같이 `batches` 배열을 갖습니다.

```json
    "destination": {
        "dataSetId": "{DATASET_ID}",
        "segmentPerBatch": true,
        "batches": [
            {
                "segmentId": "segment1",
                "segmentNs": "ups",
                "status": ["realized"],
                "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
            },
            {
                "segmentId": "segment2",
                "segmentNs": "AdCloud",
                "status": "exited",
                "batchId": "df4gssdfb93a09f7e37fa53ad52"
            }
        ]
    }
```

+++

## 특정 내보내기 작업 검색 {#get}

`/export/jobs` 끝점에 대한 GET 요청을 만들고 요청 경로에 검색할 내보내기 작업의 ID를 제공하여 특정 내보내기 작업에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 액세스하려는 내보내기 작업의 `id`입니다. |

**요청**

+++ 내보내기 작업을 검색하는 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공한 응답은 지정된 내보내기 작업에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 내보내기 작업을 검색할 때의 샘플 응답입니다.

```json
{
    "id": 11037,
    "jobType": "BATCH",
    "destination": {
        "datasetId": "5b7c86968f7b6501e21ba9df",
        "segmentPerBatch": false,
        "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    },
    "fields": "identities.id,personalEmail.address",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "status": "SUCCEEDED",
    "filter": {
        "segments": [
            {
                "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
                "segmentNs": "ups",
                "status":[
                    "realized"
                ]
            }
        ]
    },
    "mergePolicy": {
        "id": "timestampOrdered-none-mp",
        "version": 1
    },
    "profileInstanceId": "ups",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "profileExportTime": {
            "startTimeInMs": 123456789000,
            "endTimeInMs": 123456799000,
            "totalTimeInMs": 10000
        },
        "totalExportedProfileCounter": 20,
        "exportedProfileByNamespaceCounter": {
            "namespace1": 10,
            "namespace2": 5
        }
    },
    "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94"
    },
    "creationTime": 1538615973895,
    "updateTime": 1538616233239,
    "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `destination` | 내보낸 데이터의 대상 정보:<ul><li>`datasetId`: 데이터를 내보낸 데이터 세트의 ID입니다.</li><li>`segmentPerBatch`: 세그먼트 ID의 통합 여부를 보여 주는 부울 값입니다. `false` 값은 모든 세그먼트 ID가 단일 배치 ID에 있음을 의미합니다. 값이 `true`이면 하나의 세그먼트 ID를 하나의 배치 ID로 내보냅니다.</li></ul> |
| `fields` | 내보낸 필드의 목록(쉼표로 구분됨). |
| `schema.name` | 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |
| `filter.segments` | 내보내는 세그먼트입니다. 다음 필드가 포함되어 있습니다.<ul><li>`segmentId`: 내보낼 프로필의 세그먼트 ID입니다.</li><li>`segmentNs`: 지정된 `segmentID`에 대한 세그먼트 네임스페이스입니다.</li><li>`status`: `segmentID`에 대한 상태 필터를 제공하는 문자열 배열입니다. 기본적으로 `status`은(는) 현재 시간에 세그먼트에 속하는 모든 프로필을 나타내는 값 `["realized"]`을(를) 갖습니다. 가능한 값은 `realized` 및 `exited`입니다.  `realized` 값은 프로필이 세그먼트에 적합함을 의미합니다. 값이 `exiting`이면 프로필이 세그먼트를 종료하는 것입니다.</li></ul> |
| `mergePolicy` | 내보낸 데이터에 대한 병합 정책 정보. |
| `metrics.totalTime` | 내보내기 작업을 실행하는 데 걸린 총 시간을 나타내는 필드입니다. |
| `metrics.profileExportTime` | 프로필을 내보내는 데 걸린 시간을 나타내는 필드. |
| `totalExportedProfileCounter` | 모든 배치에서 내보낸 총 프로필 수입니다. |

+++

## 특정 내보내기 작업 취소 또는 삭제 {#delete}

`/export/jobs` 끝점에 DELETE 요청을 하고 요청 경로에 삭제할 내보내기 작업의 ID를 제공하여 지정된 내보내기 작업의 삭제를 요청할 수 있습니다.

**API 형식**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 삭제할 내보내기 작업의 `id`입니다. |

**요청**

+++ 내보내기 작업 삭제에 대한 샘플 요청입니다.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 204를 반환합니다.

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 다음 단계

이 안내서를 읽고 나면 이제 내보내기 작업이 작동하는 방식에 대해 더 잘 이해할 수 있습니다.
