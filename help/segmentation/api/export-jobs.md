---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 내보내기 작업
topic: developer guide
translation-type: tm+mt
source-git-commit: 16ebff522c5b08e4c100f5d2f972ef4db64656a7

---


# 내보내기 작업

intro

- 내보내기 작업 목록 검색
- 새 내보내기 작업 만들기
- 특정 내보내기 작업 검색
- 특정 내보내기 작업 취소 또는 삭제

## 시작하기

이 안내서에서 사용되는 API 끝점은 세그멘테이션 API의 일부입니다. 계속하기 전에 세그멘테이션 개발자 [안내서를](./getting-started.md)검토하십시오.

특히 세그멘테이션 개발자 안내서의 [시작 섹션은](./getting-started.md#getting-started) 관련 항목에 대한 링크, 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## 내보내기 작업 목록 검색

IMS에 대한 모든 내보내기 작업 목록을 `/export/jobs` 끝점에 GET 요청을 만들어 검색할 수 있습니다.

**API 형식**

```http
GET /export/jobs
GET /export/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*선택*&#x200B;사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다.

**쿼리 매개 변수**

다음은 내보내기 작업을 나열하기 위한 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 내보내기 작업이 검색됩니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `limit` | 반환된 내보내기 작업 수를 지정합니다. |
| `offset` | 결과 페이지의 오프셋을 지정합니다. |
| `status` | 상태에 따라 결과를 필터링합니다. 지원되는 값은 `NEW`, `SUCCEEDED`및 `FAILED`입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 내보내기 작업 목록이 있는 HTTP 상태 200을 JSON으로 반환합니다. 다음 응답은 IMS 조직에 대해 성공한 모든 내보내기 작업 목록을 반환합니다.

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
        "batches": {
          "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
          "segmentNs": "ups",
          "status": [
            "realized"
          ],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        }
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
            "fromIngestTimestamp": "2018-01-01T00:00:00Z"
          }
        }
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
        "aCPDatasetWriteTime": {
          "startTimeInMs": 123456789000,
          "endTimeInMs": 123456799000,
          "totalTimeInMs": 10000
        }
      },
      "computeGatewayJobId": {
        "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
        "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "creationTime": 1538615973895,
      "updateTime": 1538616233239,
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
    }
  ],
  "page": {
    "sortField": "createdTime",
    "sort": "desc",
    "pageOffset": "1540974701302_96",
    "pageSize": 10
  },
  "link": {
    "next": "string"
  }
}
```

## 새 내보내기 작업 만들기

종단점에 POST 요청을 만들어 새 내보내기 작업을 만들 수 `/export/jobs` 있습니다.

**API 형식**

```http
POST /export/jobs
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/export/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
  },
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df"
  },
  "schema": {
    "name": "_xdm.context.profile"
  }
 }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `fields` | 선택 사항입니다. 내보낸 필드의 목록입니다. 비워 두면 모든 필드를 내보냅니다. |
| `mergePolicy` | 선택 사항입니다. 제공되지 않으면 내보내기는 지정된 세그먼트와 동일한 병합 정책을 사용합니다. |
| `filter` | 선택 사항입니다. 비워 두면 모든 데이터가 내보내집니다. |
| `filter.segments` | 선택 사항입니다. 내보내기 작업의 세그먼트 필터입니다. |
| `filter.segmentQualificationTime` | 선택 사항입니다. 세그먼트 자격 조건 시간에 대한 필터입니다. 시작 및/또는 종료 시간을 제공할 수 있습니다. |
| `filter.fromIngestTimestamp` | 선택 사항입니다. RFC-3339 형식 타임스탬프 |
| `destination.datasetId` | 필수 여부. 데이터를 내보낼 데이터 집합의 `id` 값입니다. |
| `segments.segmentId` | 필수 여부. 내보낼 세그먼트의 `id` 값입니다. |
| `segments.sgementNs` | 선택 사항입니다. 지정된 `namespace` 세그먼트에 대한 내용입니다. |



**응답**

성공적인 응답은 새로 만든 내보내기 작업의 세부 사항과 함께 HTTP 상태 200을 반환합니다.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## 특정 내보내기 작업 검색

GET 요청을 `/export/jobs` 끝점에 만들고 요청 경로에 내보내기 작업의 `id` 값을 제공하여 특정 내보내기 작업에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`:검색할 내보내기 작업의 `id` 값입니다.

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 내보내기 작업에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "id": 100,
  "jobType": "BATCH",
  "destination": {
    "datasetId": "5b7c86968f7b6501e21ba9df",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52",
    "batches": {
      "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff",
      "segmentNs": "ups",
      "status": [
        "realized"
      ],
      "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
    }
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
        "fromIngestTimestamp": "2018-01-01T00:00:00Z"
      }
    }
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
    "aCPDatasetWriteTime": {
      "startTimeInMs": 123456789000,
      "endTimeInMs": 123456799000,
      "totalTimeInMs": 10000
    }
  },
  "computeGatewayJobId": {
    "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
    "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
  },
  "creationTime": 1538615973895,
  "updateTime": 1538616233239,
  "requestId": "d995479c-8a08-4240-903b-af469c67be1f"
}
```

## 특정 내보내기 작업 취소 또는 삭제

끝점에 DELETE 요청을 만들고 요청 경로에 내보내기 작업의 `/export/jobs` `id` 값을 제공하여 지정된 내보내기 작업을 삭제하도록 요청할 수 있습니다.

**API 형식**

```http
DELETE /export/jobs/{EXPORT_JOB_ID}
```

- `{EXPORT_JOB_ID}`:삭제할 내보내기 작업의 `id` 값.

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/export/jobs/{EXPORT_JOB_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 200을 반환합니다.

```json
{
  "status": true,
  "message": "Export job has been marked for cancelling"
}
```

## 다음 단계
