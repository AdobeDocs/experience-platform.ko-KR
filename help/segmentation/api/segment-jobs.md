---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;segment jobs;segment job;API;api;
solution: Experience Platform
title: 세그먼트 작업
topic: developer guide
description: 이 안내서에서는 세그먼트 작업을 더 잘 이해하는 데 도움이 되는 정보를 제공하고 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 3%

---


# 세그먼트 작업 끝점

세그먼트 작업은 새 대상 세그먼트를 만드는 비동기 프로세스입니다. 프로필 조각에 겹치는 속성을 병합하는 방법을 제어하는 [병합 정책과](./segment-definitions.md)세그먼트 정의를 [참조합니다](../../profile/api/merge-policies.md) [!DNL Real-time Customer Profile] . 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생한 오류와 대상의 최종 크기 등 세그먼트에 대한 다양한 정보를 수집할 수 있습니다.

이 안내서에서는 세그먼트 작업을 더 잘 이해하는 데 도움이 되는 정보를 제공하고 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

이 안내서에 사용되는 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md) 에서 필수 머리글 및 예제 API 호출 읽기 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 세그먼트 작업 목록 검색 {#retrieve-list}

종단점에 GET 요청을 하여 IMS 조직에 대한 모든 세그먼트 작업 목록을 검색할 수 `/segment/jobs` 있습니다.

**API 형식**

끝점은 결과를 필터링하는 데 도움이 되는 여러 쿼리 매개 변수를 지원합니다. `/segment/jobs` 이러한 매개 변수는 선택 사항이지만 값비싼 오버헤드를 줄이려면 매개 변수를 사용하는 것이 좋습니다. 매개 변수가 없는 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 내보내기 작업이 검색됩니다. 여러 매개 변수를 앰퍼샌드(앰퍼샌드)로 구분하여 포함할 수`&`있습니다.

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**쿼리 매개 변수**

| 매개 변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `start` | 반환된 세그먼트 작업의 시작 오프셋을 지정합니다. | `start=1` |
| `limit` | 페이지당 반환되는 세그먼트 작업 수를 지정합니다. | `limit=20` |
| `status` | 상태에 따라 결과를 필터링합니다. 지원되는 값은 신규, 대기 중, 처리 중, 성공, 실패, 취소, 취소됨 | `status=NEW` |
| `sort` | 반환된 세그먼트 작업을 주문합니다. 형식을 사용합니다 `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | 세그먼트 작업을 필터링하고 주어진 필터에 대한 정확한 일치를 가져옵니다. 다음 형식 중 하나로 작성할 수 있습니다. <ul><li>`[jsonObjectPath]==[value]` - 개체 키 필터링</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - 배열 내에서 필터링</li></ul> | `property=segments~segmentId==workInUS` |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 세그먼트 작업 목록이 있는 HTTP 상태 200을 JSON으로 반환합니다. 다음 응답은 IMS 조직에 대해 성공한 모든 세그먼트 작업 목록을 반환합니다.

>[!NOTE]
>
>다음 응답은 공간에 대해 잘렸고 첫 번째 반환된 작업만 표시됩니다.

```json
{
    "_page": {
        "totalCount": 14,
        "pageSize": 14
    },
    "children": [
        {
            "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "profileInstanceId": "ups",
            "source": "scheduler",
            "status": "SUCCEEDED",
            "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
            "computeJobId": 8811,
            "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "metrics": {
                "totalTime": {
                    "startTimeInMs": 1573203617195,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 778460
                },
                "profileSegmentationTime": {
                    "startTimeInMs": 1573204266727,
                    "endTimeInMs": 1573204395655,
                    "totalTimeInMs": 128928
                },
                "totalProfiles": 0,
                "segmentedProfileCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": 0,
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": 0
                },
                "segmentedProfileByNamespaceCounter": {
                    "30230300-ccf1-48ad-8012-c5563a007069": {},
                    "ca763983-5572-4ea4-809c-b7dff7e0d79b": {}
                }
            },
            "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "properties": {
                "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
                "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
            },
            "_links": {
                "cancel": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "DELETE"
                },
                "checkStatus": {
                    "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
                    "method": "GET"
                }
            },
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 세그먼트 작업의 시스템 생성 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 상태에 대한 잠재적 값에는 &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELED&quot;, &quot;FAILED&quot; 및 &quot;SUCCESS&quot;가 포함됩니다. |
| `segments` | 세그먼트 작업 내에서 반환되는 세그먼트 정의에 대한 정보가 포함된 객체입니다. |
| `segments.segment.id` | 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL으로 작성된 세그먼트 정의 표현식에 대한 정보를 포함하는 개체입니다. |
| `metrics` | 세그먼트 작업에 대한 진단 정보가 포함된 개체입니다. |

## 새 세그먼트 작업 만들기 {#create}

종단점에 POST 요청을 만들고 본문에 새 대상을 만들 세그먼트 정의의 ID를 포함하여 새 세그먼트 작업을 만들 수 있습니다. `/segment/jobs`

**API 형식**

```http
POST /segment/jobs
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
[
  {
    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
  }
]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `segmentId` | 세그먼트 작업을 만들 세그먼트 정의의 ID입니다. 이러한 세그먼트 정의는 서로 다른 병합 정책에 속할 수 있습니다. 세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서를 참조하십시오](./segment-definitions.md). |

**응답**

성공적인 응답은 새로 만든 세그먼트 작업의 세부 사항과 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "NEW",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304260000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304260
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 만든 세그먼트 작업의 시스템 생성 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 세그먼트 작업이 새로 만들어지므로 상태는 항상 &quot;NEW&quot;입니다. |
| `segments` | 이 세그먼트 작업이 실행 중인 세그먼트 정의에 대한 정보가 포함된 개체입니다. |
| `segments.segment.id` | 제공한 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL으로 작성된 세그먼트 정의 표현식에 대한 정보를 포함하는 개체입니다. |

## 특정 세그먼트 작업 검색 {#get}

종단점에 GET 요청을 수행하고 요청 경로에서 검색할 세그먼트 작업의 ID를 제공하여 특정 세그먼트 작업에 대한 자세한 정보를 검색할 수 있습니다. `/segment/jobs`

**API 형식**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 검색할 세그먼트 작업의 `id` 값. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 세그먼트 작업에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "651fc109-3963-48d2-aa98-9e3cc2003bac",
    "computeJobId": 39312,
    "computeGatewayJobId": "a0099ab6-11ab-4c2b-a0ea-6162e16806bd",
    "segments": [
        {
            "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
            "segment": {
                "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                "mergePolicy": {
                    "id": "e161dae9-52f0-4c7f-b264-dc43dd903d56",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "Hw1jdAHeuWHVKVxcAPFrLCbbjkriDl9v",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 세그먼트 작업의 시스템 생성 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 상태에 대한 잠재적 값에는 &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELED&quot;, &quot;FAILED&quot; 및 &quot;SUCCESS&quot;가 포함됩니다. |
| `segments` | 세그먼트 작업 내에서 반환되는 세그먼트 정의에 대한 정보가 포함된 객체입니다. |
| `segments.segment.id` | 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL으로 작성된 세그먼트 정의 표현식에 대한 정보를 포함하는 개체입니다. |
| `metrics` | 세그먼트 작업에 대한 진단 정보가 포함된 개체입니다. |

## 세그먼트 일괄 검색 작업 {#bulk-get}

종단점에 POST 요청을 만들고 요청 본문에 세그먼트 작업의 `/segment/jobs/bulk-get` `id` 값을 제공하여 여러 세그먼트 작업에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
POST /segment/jobs/bulk-get
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "ids": [
            {
                "id": "cc3419d3-0389-47f1-b174-fead6b3c830d"
            },
            {
                "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8"
            }
        ]
    }'
```

**응답**

성공적인 응답은 요청된 세그먼트 작업이 있는 HTTP 상태 207을 반환합니다.

>[!NOTE]
>
>다음 응답이 공간에 대해 잘려서 각 세그먼트 작업의 일부 세부 정보만 표시합니다. 전체 응답에는 요청된 세그먼트 작업에 대한 전체 세부 정보가 표시됩니다.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "30230300-ccf1-48ad-8012-c5563a007069",
                    "segment": {
                        "id": "30230300-ccf1-48ad-8012-c5563a007069",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        },
        "c527dc3f-07fe-4b96-be4e-23f38e734ff8": {
            "id": "c527dc3f-07fe-4b96-be4e-23f38e734ff8",
            "imsOrgId": "{IMS_ORG}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                    "segment": {
                        "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
                        "expression": {
                            "type": "PQL",
                            "format": "pql/json",
                            "value": "{PQL_EXPRESSION}"
                        },
                        "mergePolicyId": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                        "mergePolicy": {
                            "id": "b83185bb-0bc6-489c-9363-0075eb30b4c8",
                            "version": 1
                        }
                    }
                }
            ],
            "updateTime": 1573204395000,
            "creationTime": 1573203600535,
            "updateEpoch": 1573204395
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 세그먼트 작업의 시스템 생성 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 상태에 대한 잠재적 값에는 &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELED&quot;, &quot;FAILED&quot; 및 &quot;SUCCESS&quot;가 포함됩니다. |
| `segments` | 세그먼트 작업 내에서 반환되는 세그먼트 정의에 대한 정보가 포함된 객체입니다. |
| `segments.segment.id` | 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL으로 작성된 세그먼트 정의 표현식에 대한 정보를 포함하는 개체입니다. |

## 특정 세그먼트 작업 취소 또는 삭제 {#delete}

종단점에 DELETE 요청을 만들고 요청 경로에서 삭제하려는 세그먼트 작업의 ID를 제공하여 특정 세그먼트 작업을 삭제할 수 있습니다. `/segment/jobs`

>[!NOTE]
>
>삭제 요청에 대한 API 응답이 즉시 나타납니다. 하지만 세그먼트 작업의 실제 삭제는 비동기적입니다. 즉, 세그먼트 작업에 대한 삭제 요청이 수행된 시점과 세그먼트 작업이 적용되는 시점 사이에 시간 차이가 있습니다.

**API 형식**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 삭제할 세그먼트 작업의 `id` 값. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 정보와 함께 HTTP 상태 204를 반환합니다.

```json
{
    "status": true,
    "message": "Segment job with id 'd3b4a50d-dfea-43eb-9fca-557ea53771fd' has been marked for cancelling"
}
```

## 다음 단계

이 안내서를 읽고 나면 세그먼트 작업 방식을 더 잘 이해할 수 있습니다.