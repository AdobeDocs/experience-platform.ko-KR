---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 세그먼트 작업
topic: developer guide
translation-type: tm+mt
source-git-commit: db4cdbfb7719d94919c896162ca7875fdf7d2502

---


# 세그먼트 작업 개발자 가이드

세그먼트 작업은 새 대상 세그먼트를 만드는 비동기 프로세스입니다. 세그먼트 정의뿐만 아니라 실시간 고객 프로파일을 프로필 조각에 겹치는 속성을 병합하는 방법을 제어하는 모든 병합 정책을 참조합니다. 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생한 오류와 대상의 최종 크기 등 세그먼트에 대한 다양한 정보를 수집할 수 있습니다.

이 안내서에서는 세그먼트 작업을 더 잘 이해하는 데 도움이 되는 정보를 제공하고 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

이 안내서에서 사용되는 API 끝점은 세그멘테이션 API의 일부입니다. 계속하기 전에 세그멘테이션 개발자 [안내서를](./getting-started.md)검토하십시오.

특히 세그멘테이션 개발자 안내서의 [시작 섹션은](./getting-started.md#getting-started) 관련 항목에 대한 링크, 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## 세그먼트 작업 목록 검색

IMS에 대한 모든 세그먼트 작업 목록을 `/segment/jobs` 끝점에 GET 요청을 수행하여 검색할 수 있습니다.

**API 형식**

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*선택*&#x200B;사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다.

**쿼리 매개 변수**

다음은 세그먼트 작업을 나열하기 위한 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 세그먼트 작업이 검색됩니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `start` | 반환된 세그먼트 작업의 시작 오프셋을 지정합니다. |
| `limit` | 페이지당 반환되는 세그먼트 작업 수를 지정합니다. |
| `status` | 상태에 따라 결과를 필터링합니다. 지원되는 값은 신규, 대기 중, 처리 중, 성공, 실패, 취소, 취소됨 |
| `sort` | 반환된 세그먼트 작업을 주문합니다. 형식으로 `[attributeName]:[desc|asc]`작성됩니다. |
| `property` | 세그먼트 작업을 필터링하고 주어진 필터에 대한 정확한 일치를 가져옵니다. 다음 형식 중 하나로 작성할 수 있습니다. <ul><li>`[jsonObjectPath]==[value]` - 개체 키 필터링</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - 배열 내에서 필터링</li></ul> |

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

>[!NOTE] 다음 응답은 공간에 대해 잘렸고 첫 번째 반환된 작업만 표시됩니다.

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

## 새 세그먼트 작업 만들기

종단점에 POST 요청을 만들어 새 세그먼트 작업을 만들 수 `/segment/jobs` 있습니다.

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
]
 '
```

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

## 특정 세그먼트 작업 검색

종단점에 GET 요청을 하고 요청 경로에서 세그먼트 작업의 `/segment/jobs` `id` 값을 제공하여 특정 세그먼트 작업에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 검색할 세그먼트 작업의 `id` 값입니다. |

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

## 특정 세그먼트 작업 취소 또는 삭제

종단점에 DELETE 요청을 하고 요청 경로에서 세그먼트 작업의 `/segment/jobs` `id` 값을 제공하여 지정된 세그먼트 작업을 삭제하도록 요청할 수 있습니다.

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

이제 이 가이드를 읽고 세그먼트 작업 작동 방식을 더 잘 이해할 수 있습니다. 세그멘테이션에 대한 자세한 내용은 세그멘테이션 [개요를](../home.md)참조하십시오.