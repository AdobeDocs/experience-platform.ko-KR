---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;내보내기 작업;api;
solution: Experience Platform
title: 세그먼트 내보내기 작업 API 끝점
topic-legacy: developer guide
description: 내보내기 작업은 대상 세그먼트 구성원을 데이터 세트에 유지하는 데 사용되는 비동기 프로세스입니다. Adobe Experience Platform 세그멘테이션 서비스 API에서 /export/jobs 엔드포인트를 사용할 수 있으며, 이 엔드포인트를 통해 프로그래밍 방식으로 내보내기 작업을 검색, 만들기 및 취소할 수 있습니다.
exl-id: 5b504a4d-291a-4969-93df-c23ff5994553
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 2%

---

# 세그먼트 내보내기 작업 끝점

내보내기 작업은 대상 세그먼트 구성원을 데이터 세트에 유지하는 데 사용되는 비동기 프로세스입니다. 를 사용할 수 있습니다 `/export/jobs` 프로그래밍 방식으로 내보내기 작업을 검색, 만들기 및 취소할 수 있는 Adobe Experience Platform 세그멘테이션 API의 끝점입니다.

>[!NOTE]
>
>이 안내서에서는 의 내보내기 작업 사용에 대해 설명합니다 [!DNL Segmentation API]. 내보내기 작업 관리 방법에 대한 자세한 내용 [!DNL Real-Time Customer Profile] 데이터, 다음 안내서를 참조하십시오. [프로필 API에서 작업 내보내기](../../profile/api/export-jobs.md)

## 시작하기

이 안내서에서 사용되는 엔드포인트는 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 [시작 안내서](./getting-started.md) 필수 헤더 및 예제 API 호출을 읽는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보입니다.

## 내보내기 작업 목록 검색 {#retrieve-list}

IMS 조직에 대해 GET 요청을 수행하여 모든 내보내기 작업 목록을 검색할 수 있습니다 `/export/jobs` 엔드포인트.

**API 형식**

다음 `/export/jobs` endpoint는 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 고가의 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 종단점을 호출하면 조직에서 사용할 수 있는 모든 내보내기 작업이 검색됩니다. 여러 매개 변수를 앰퍼샌드( )로 구분하여 포함할 수 있습니다`&`).

```http
GET /export/jobs
GET /export/jobs?limit={LIMIT}
GET /export/jobs?offset={OFFSET}
GET /export/jobs?status={STATUS}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{LIMIT}` | 반환된 내보내기 작업 수를 지정합니다. |
| `{OFFSET}` | 결과 페이지의 오프셋을 지정합니다. |
| `{STATUS}` | 상태에 따라 결과를 필터링합니다. 지원되는 값은 &quot;NEW&quot;, &quot;SUCCEEDED&quot; 및 &quot;FAILED&quot;입니다. |

**요청**

다음 요청은 IMS 조직 내에서 마지막 두 내보내기 작업을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 요청 경로에 제공된 쿼리 매개 변수를 기반으로 성공적으로 완료된 내보내기 작업 목록과 함께 HTTP 상태 200을 반환합니다.

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
                        "status": ["realized", "existing"]
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
| `destination` | 내보낸 데이터에 대한 대상 정보:<ul><li>`datasetId`: 데이터를 내보낸 데이터 세트의 ID입니다.</li><li>`segmentPerBatch`: 세그먼트 ID가 통합되었는지 여부를 표시하는 부울 값입니다. 값이 &quot;false&quot;이면 모든 세그먼트 ID가 단일 배치 ID로 내보내집니다. 값이 &quot;true&quot;이면 하나의 세그먼트 ID가 하나의 배치 ID로 내보내집니다. **참고:** 값을 true로 설정하면 배치 내보내기 성능에 영향을 줄 수 있습니다.</li></ul> |
| `fields` | 내보낸 필드의 목록을 쉼표로 구분합니다. |
| `schema.name` | 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |
| `filter.segments` | 내보낸 세그먼트입니다. 다음 필드가 포함되어 있습니다.<ul><li>`segmentId`: 프로필을 내보낼 세그먼트 ID입니다.</li><li>`segmentNs`: 지정된 세그먼트의 세그먼트 네임스페이스 `segmentID`.</li><li>`status`: 에 대한 상태 필터를 제공하는 문자열 배열입니다 `segmentID`. 기본적으로 `status` 에는 값이 있습니다. `["realized", "existing"]` 현재 시간에 세그먼트에 속하는 모든 프로필을 나타냅니다. 가능한 값은 다음과 같습니다. &quot;실현됨&quot;, &quot;기존&quot; 및 &quot;종료됨&quot; 값이 &quot;실현됨&quot;이면 프로필이 세그먼트를 입력하고 있음을 의미합니다. 값이 &quot;기존&quot;이면 프로필이 세그먼트에 계속 있을 것임을 의미합니다. 값이 &quot;종료&quot;이면 프로필이 세그먼트를 종료함을 의미합니다.</li></ul> |
| `mergePolicy` | 내보낸 데이터에 대한 정책 정보를 병합합니다. |
| `metrics.totalTime` | 내보내기 작업을 실행하는 데 걸린 총 시간을 나타내는 필드입니다. |
| `metrics.profileExportTime` | 프로필을 내보내는 데 걸린 시간을 나타내는 필드입니다. |
| `page` | 요청된 내보내기 작업의 페이지 매김에 대한 정보입니다. |
| `link.next` | 내보내기 작업의 다음 페이지에 대한 링크. |

## 새 내보내기 작업 만들기 {#create}

에 POST 요청을 수행하여 새 내보내기 작업을 만들 수 있습니다 `/export/jobs` 엔드포인트.

**API 형식**

```http
POST /export/jobs
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 내보내기 작업을 만듭니다.

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
| `fields` | 내보낸 필드의 목록을 쉼표로 구분합니다. 비워 두면 모든 필드가 내보내집니다. |
| `mergePolicy` | 내보낸 데이터를 제어할 병합 정책을 지정합니다. 내보낼 세그먼트가 여러 개 있는 경우 이 매개 변수를 포함하십시오. 제공하지 않은 경우 내보내기는 주어진 세그먼트와 동일한 병합 정책을 수행합니다. |
| `filter` | 아래 나열된 하위 속성에 따라 ID, 자격 시간 또는 수집 시간으로 내보내기 작업에 포함할 세그먼트를 지정하는 객체입니다. 비워 두면 모든 데이터를 내보냅니다. |
| `filter.segments` | 내보낼 세그먼트를 지정합니다. 이 값을 생략하면 모든 프로필의 모든 데이터를 내보냅니다. 각각 다음 필드가 포함된 세그먼트 개체 배열을 허용합니다.<ul><li>`segmentId`: **(를 사용하는 경우 필수) `segments`)** 내보낼 프로필에 대한 세그먼트 ID입니다.</li><li>`segmentNs` *(선택 사항)* 지정된 세그먼트의 세그먼트 네임스페이스 `segmentID`.</li><li>`status` *(선택 사항)* 에 대한 상태 필터를 제공하는 문자열 배열입니다 `segmentID`. 기본적으로 `status` 에는 값이 있습니다. `["realized", "existing"]` 현재 시간에 세그먼트에 속하는 모든 프로필을 나타냅니다. 가능한 값은 다음과 같습니다. `"realized"`, `"existing"`, 및 `"exited"`.  값이 &quot;실현됨&quot;이면 프로필이 세그먼트를 입력하고 있음을 의미합니다. 값이 &quot;기존&quot;이면 프로필이 세그먼트에 계속 있을 것임을 의미합니다. 값이 &quot;종료&quot;이면 프로필이 세그먼트를 종료함을 의미합니다.</li></ul> |
| `filter.segmentQualificationTime` | 세그먼트 자격 시간을 기준으로 필터링합니다. 시작 시간 및/또는 종료 시간을 제공할 수 있습니다. |
| `filter.segmentQualificationTime.startTime` | 주어진 상태에 대한 세그먼트 ID에 대한 세그먼트 자격 시작 시간입니다. 제공되지 않으며, 세그먼트 ID 자격 시작 시간에 필터가 없습니다. 타임스탬프를 [RFC 3339](https://tools.ietf.org/html/rfc3339) 형식 지정 |
| `filter.segmentQualificationTime.endTime` | 주어진 상태에 대한 세그먼트 ID에 대한 세그먼트 자격 종료 시간입니다. 제공되지 않으며, 세그먼트 ID 자격 종료 시간에는 필터가 없습니다. 타임스탬프를 [RFC 3339](https://tools.ietf.org/html/rfc3339) 형식 지정 |
| `filter.fromIngestTimestamp ` | 내보낸 프로필에는 이 타임스탬프 이후에 업데이트된 프로필만 포함하도록 제한합니다. 타임스탬프를 [RFC 3339](https://tools.ietf.org/html/rfc3339) 형식 지정 <ul><li>`fromIngestTimestamp` 대상 **프로필**, 제공된 경우: 병합된 업데이트된 타임스탬프가 지정된 타임스탬프보다 큰 병합된 모든 프로필을 포함합니다. 지원 `greater_than` 피연산자</li><li>`fromIngestTimestamp` 대상 **events**: 이 타임스탬프 이후에 수집된 모든 이벤트는 결과 프로필 결과에 따라 내보내집니다. 이벤트 시간 자체가 아니라 이벤트의 수집 시간입니다.</li> |
| `filter.emptyProfiles` | 빈 프로필에 대해 필터링할지 여부를 나타내는 부울 값입니다. 프로필에는 프로필 레코드, ExperienceEvent 레코드 또는 둘 다 포함할 수 있습니다. 프로필 레코드가 없고 ExperienceEvent 레코드만 있는 프로필을 &quot;emptyProfiles&quot;라고 합니다. &quot;emptyProfiles&quot;를 포함하여 프로필 저장소의 모든 프로필을 내보내려면 값을 다음과 같이 설정합니다. `emptyProfiles` to `true`. If `emptyProfiles` 가 로 설정되어 있습니다. `false`로 설정되면 저장소에 프로필 레코드가 있는 프로필만 내보내집니다. 기본적으로 `emptyProfiles` 속성은 포함되지 않으며 프로필 레코드가 포함된 프로필만 내보내집니다. |
| `additionalFields.eventList` | 다음 설정 중 하나 이상을 제공하여 자식 또는 관련 개체에 대해 내보낸 시계열 이벤트 필드를 제어합니다.<ul><li>`fields`: 내보낼 필드를 제어합니다.</li><li>`filter`: 연관된 객체에서 포함된 결과를 제한하는 기준을 지정합니다. 내보내기에 필요한 최소값(일반적으로 날짜)이 필요합니다.</li><li>`filter.fromIngestTimestamp`: 시계열 이벤트를 제공된 타임스탬프 이후에 수집된 이벤트로 필터링합니다. 이벤트 시간 자체가 아니라 이벤트의 수집 시간입니다.</li><li>`filter.toIngestTimestamp`: 제공된 타임스탬프 전에 수집된 타임스탬프로 타임스탬프를 필터링합니다. 이벤트 시간 자체가 아니라 이벤트의 수집 시간입니다.</li></ul> |
| `destination` | **(필수)** 내보낸 데이터에 대한 정보:<ul><li>`datasetId`: **(필수)** 데이터를 내보낼 데이터 세트의 ID입니다.</li><li>`segmentPerBatch`: *(선택 사항)* 지정하지 않은 경우 기본값이 &quot;false&quot;로 설정되는 부울 값입니다. 값 &quot;false&quot;는 모든 세그먼트 ID를 단일 배치 ID로 내보냅니다. 값이 &quot;true&quot;이면 하나의 세그먼트 ID를 하나의 배치 ID로 내보냅니다. 값을 &quot;true&quot;로 설정하면 배치 내보내기 성능에 영향을 줄 수 있습니다.</li></ul> |
| `schema.name` | **(필수)** 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |
| `evaluationInfo.segmentation` | *(선택 사항)* 지정하지 않은 경우 기본값이 로 설정되는 부울 값 `false`. 값 `true` 내보내기 작업에서 세분화를 수행해야 함을 나타냅니다. |

**응답**

성공적인 응답은 새로 만든 내보내기 작업의 세부 사항과 함께 HTTP 상태 200을 반환합니다.

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
| `id` | 방금 생성된 내보내기 작업을 식별하는 시스템에서 생성한 읽기 전용 값입니다. |

또는, `destination.segmentPerBatch` 이(가) `true`, `destination` 위의 객체에는 `batches` 배열입니다.

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

## 특정 내보내기 작업 검색 {#get}

에 GET 요청을 수행하여 특정 내보내기 작업에 대한 자세한 정보를 검색할 수 있습니다 `/export/jobs` 요청 경로에서 검색할 내보내기 작업의 ID를 제공하고 끝점입니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 다음 `id` 액세스하려는 내보내기 작업의 수입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/11037 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 내보내기 작업에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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
| `destination` | 내보낸 데이터에 대한 대상 정보:<ul><li>`datasetId`: 데이터를 내보낸 데이터 세트의 ID입니다.</li><li>`segmentPerBatch`: 세그먼트 ID가 통합되었는지 여부를 표시하는 부울 값입니다. 값 `false` 는 모든 세그먼트 ID가 단일 배치 ID에 있음을 의미합니다. 값 `true` 하나의 세그먼트 ID가 하나의 배치 ID로 내보내짐을 의미합니다.</li></ul> |
| `fields` | 내보낸 필드의 목록을 쉼표로 구분합니다. |
| `schema.name` | 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |
| `filter.segments` | 내보낸 세그먼트입니다. 다음 필드가 포함되어 있습니다.<ul><li>`segmentId`: 내보낼 프로필에 대한 세그먼트 ID입니다.</li><li>`segmentNs`: 지정된 세그먼트의 세그먼트 네임스페이스 `segmentID`.</li><li>`status`: 에 대한 상태 필터를 제공하는 문자열 배열입니다 `segmentID`. 기본적으로 `status` 에는 값이 있습니다. `["realized", "existing"]` 현재 시간에 세그먼트에 속하는 모든 프로필을 나타냅니다. 가능한 값은 다음과 같습니다. &quot;실현됨&quot;, &quot;기존&quot; 및 &quot;종료됨&quot;  값이 &quot;실현됨&quot;이면 프로필이 세그먼트를 입력하고 있음을 의미합니다. 값이 &quot;기존&quot;이면 프로필이 세그먼트에 계속 있을 것임을 의미합니다. 값이 &quot;종료&quot;이면 프로필이 세그먼트를 종료함을 의미합니다.</li></ul> |
| `mergePolicy` | 내보낸 데이터에 대한 정책 정보를 병합합니다. |
| `metrics.totalTime` | 내보내기 작업을 실행하는 데 걸린 총 시간을 나타내는 필드입니다. |
| `metrics.profileExportTime` | 프로필을 내보내는 데 걸린 시간을 나타내는 필드입니다. |
| `totalExportedProfileCounter` | 모든 배치에서 내보낸 총 프로필 수입니다. |

## 특정 내보내기 작업 취소 또는 삭제 {#delete}

에 DELETE 요청을 수행하여 지정된 내보내기 작업을 삭제하도록 요청할 수 있습니다 `/export/jobs` 요청 경로에서 삭제할 내보내기 작업의 ID를 제공하고 끝점입니다.

**API 형식**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{EXPORT_JOB_ID}` | 다음 `id` 삭제할 내보내기 작업의 수입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 204를 반환합니다.

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 다음 단계

이 안내서를 읽은 후에는 내보내기 작업의 작동 방식을 더 잘 이해할 수 있습니다.
