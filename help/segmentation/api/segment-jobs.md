---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;세그먼트 작업;세그먼트 작업;API;API;
solution: Experience Platform
title: 세그먼트 작업 API 엔드포인트
description: Adobe Experience Platform Segmentation Service API의 세그먼트 작업 끝점을 사용하면 조직의 세그먼트 작업을 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 105481c2-1c25-4f0e-8fb0-c6577a4616b3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 2%

---

# 세그먼트 작업 엔드포인트

세그먼트 작업은 요청 시 대상 세그먼트를 만드는 비동기 프로세스입니다. 을(를) 참조합니다. [세그먼트 정의](./segment-definitions.md)및 기타 [병합 정책](../../profile/api/merge-policies.md) 방법 제어 [!DNL Real-Time Customer Profile] 은 프로필 조각에서 겹치는 속성을 병합합니다. 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생할 수 있는 오류와 대상자의 최종 크기 등 세그먼트에 대한 다양한 정보를 수집할 수 있습니다.

이 안내서에서는 세그먼트 작업을 더 잘 이해하는 데 도움이 되는 정보를 제공하며 API를 사용하여 기본 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 시작하기

이 안내서에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 세그먼트 작업 목록 검색 {#retrieve-list}

에 GET 요청을 하여 조직의 모든 세그먼트 작업 목록을 검색할 수 있습니다. `/segment/jobs` 엔드포인트.

**API 형식**

다음 `/segment/jobs` 엔드포인트는 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 값비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 내보내기 작업을 검색합니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`).

```http
GET /segment/jobs
GET /segment/jobs?{QUERY_PARAMETERS}
```

**쿼리 매개 변수**

| 매개변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `start` | 반환된 세그먼트 작업의 시작 오프셋을 지정합니다. | `start=1` |
| `limit` | 페이지당 반환되는 세그먼트 작업 수를 지정합니다. | `limit=20` |
| `status` | 상태를 기반으로 결과를 필터링합니다. 지원되는 값은 NEW, QUEUED, PROCESSING, SUCCEEDED, FAILED, CANCELLING, CANCELLED입니다. | `status=NEW` |
| `sort` | 반환된 세그먼트 작업의 순서를 지정합니다. 형식으로 작성됨 `[attributeName]:[desc|asc]`. | `sort=creationTime:desc` |
| `property` | 작업을 필터링하고 지정된 필터와 정확히 일치하는 항목을 가져옵니다. 다음 형식 중 하나로 쓸 수 있습니다. <ul><li>`[jsonObjectPath]==[value]` - 개체 키 필터링</li><li>`[arrayTypeAttributeName]~[objectKey]==[value]` - 배열 내 필터링</li></ul> | `property=segments~segmentId==workInUS` |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs?status=SUCCEEDED \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 조직에 대한 세그먼트 작업 목록이 JSON인 HTTP 상태 200을 반환합니다. 하지만 세그먼트 작업 내의 세그먼트 수에 따라 응답이 달라집니다.

**세그먼트 작업에서 1500개 이하의 세그먼트**

세그먼트 작업에서 1500개 미만의 세그먼트가 실행되는 경우 모든 세그먼트의 전체 목록이 `children.segments` 특성.

>[!NOTE]
>
>다음 응답은 공백으로 잘렸으며, 반환된 첫 번째 작업만 표시합니다.

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
                        "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                        "mergePolicy": {
                            "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
                "totalProfiles":13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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

**1500개 이상의 세그먼트**

세그먼트 작업에서 1500개가 넘는 세그먼트가 실행되는 경우 `children.segments` 속성이 표시됨 `*`모든 세그먼트가 평가됨을 나타냅니다.

>[!NOTE]
>
>다음 응답은 공백으로 잘렸으며, 반환된 첫 번째 작업만 표시합니다.

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
                    "segmentId": "*",
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
                "totalProfiles": 13146432,
                "segmentedProfileCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":1033
                },
                "segmentedProfileByNamespaceCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "tenantiduserobjid":1033,
                        "campaign_profile_mscom_mkt_prod2":1033
                    }
                },
                "segmentedProfileByStatusCounter":{
                    "94509dba-7387-452f-addc-5d8d979f6ae8":{
                        "exited":144646,
                        "realized":2056
                    }
                },
                "totalProfilesByMergePolicy":{
                    "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
| `id` | 세그먼트 작업에 대해 시스템에서 생성한 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 상태에 대한 잠재적 값에는 &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; 및 &quot;SUCCEEDED&quot;가 있습니다. |
| `segments` | 세그먼트 작업 내에서 반환된 세그먼트 정의에 대한 정보를 포함하는 객체입니다. |
| `segments.segment.id` | 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL로 작성된 세그먼트 정의의 표현식에 대한 정보가 포함된 객체입니다. |
| `metrics` | 세그먼트 작업에 대한 진단 정보를 포함하는 개체입니다. |
| `metrics.totalTime` | 세분화 작업이 시작 및 종료된 시간과 총 소요 시간에 대한 정보가 포함된 개체입니다. |
| `metrics.profileSegmentationTime` | 세분화 평가가 시작되고 종료된 시간 및 총 소요 시간에 대한 정보가 포함된 개체입니다. |
| `metrics.segmentProfileCounter` | 세그먼트 기준으로 적격한 프로필 수입니다. |
| `metrics.segmentedProfileByNamespaceCounter` | 각 세그먼트 기준으로 각 ID 네임스페이스에 적합한 프로필 수입니다. |
| `metrics.segmentProfileByStatusCounter` | 각 상태에 대한 프로필 수입니다. 다음 세 가지 상태가 지원됩니다. <ul><li>&quot;실현됨&quot; - 세그먼트에 적합한 프로필 수입니다.</li><li>&quot;종료됨&quot; - 더 이상 세그먼트에 존재하지 않는 프로필 세그먼트 수입니다.</li></ul> |
| `metrics.totalProfilesByMergePolicy` | 병합 정책별 병합된 총 프로필 수입니다. |

## 새 세그먼트 작업 만들기 {#create}

에 POST 요청을 하여 새 세그먼트 작업을 만들 수 있습니다. `/segment/jobs` 엔드포인트 및 새 대상자를 만들려는 세그먼트 정의의 ID가 본문에 포함됩니다.

**API 형식**

```http
POST /segment/jobs
```

새 세그먼트 작업을 만들 때 세그먼트 작업 내의 세그먼트 수에 따라 요청 및 응답이 달라집니다.

**세그먼트 작업에서 1500개 이하의 세그먼트**

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    }
 ]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `segmentId` | 세그먼트 작업을 생성할 세그먼트 정의의 ID입니다. 이러한 세그먼트 정의는 다른 병합 정책에 속할 수 있습니다. 세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 엔드포인트 안내서](./segment-definitions.md). |

**응답**

성공적인 응답은 새로 생성된 세그먼트 작업에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 생성된 세그먼트 작업에 대한 시스템에서 생성한 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 세그먼트 작업이 새로 생성되므로 상태는 항상 &quot;NEW&quot;가 됩니다. |
| `segments` | 이 세그먼트 작업이 실행 중인 세그먼트 정의에 대한 정보를 포함하는 개체입니다. |
| `segments.segment.id` | 제공한 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL로 작성된 세그먼트 정의의 표현식에 대한 정보가 포함된 객체입니다. |

**1500개 이상의 세그먼트**

**요청**

>[!NOTE]
>
>1500개가 넘는 세그먼트로 세그먼트 작업을 만들 수 있지만 이는 **매우 권장되지 않음**.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "segments": [
        {
            "segmentId": "*"
        }
    ]
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `schema.name` | 세그먼트에 대한 스키마의 이름입니다. |
| `segments.segmentId` | 1500개가 넘는 세그먼트로 세그먼트 작업을 실행하는 경우 다음을 전달해야 합니다 `*` 모든 세그먼트에서 세그먼테이션 작업을 실행함을 나타내는 세그먼트 ID입니다. |

**응답**

성공적인 응답은 새로 생성된 세그먼트 작업의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
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
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "*"
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 새로 생성된 세그먼트 작업에 대한 시스템에서 생성한 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 세그먼트 작업이 새로 생성되므로 상태는 항상 입니다. `NEW`. |
| `segments` | 이 세그먼트 작업이 실행 중인 세그먼트 정의에 대한 정보를 포함하는 개체입니다. |
| `segments.segment.id` | 다음 `*` 는 조직 내의 모든 세그먼트에 대해 이 세그먼트 작업이 실행 중임을 의미합니다. |

## 특정 세그먼트 작업 검색 {#get}

에 GET 요청을 하여 특정 세그먼트 작업에 대한 자세한 정보를 검색할 수 있습니다. `/segment/jobs` 엔드포인트 및 요청 경로에서 검색하려는 세그먼트 작업의 ID 제공.

**API 형식**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 다음 `id` 검색할 세그먼트 작업의 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 세그먼트 작업에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.  하지만 세그먼트 작업 내의 세그먼트 수에 따라 응답이 달라집니다.

**세그먼트 작업에서 1500개 이하의 세그먼트**

세그먼트 작업에서 1500개 미만의 세그먼트가 실행되는 경우 모든 세그먼트의 전체 목록이 `children.segments` 특성.

```json
{
    "id": "d3b4a50d-dfea-43eb-9fca-557ea53771fd",
    "imsOrgId": "{ORG_ID}",
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

**1500개 이상의 세그먼트**

세그먼트 작업에서 1500개가 넘는 세그먼트가 실행되는 경우 `children.segments` 속성이 표시됨 `*`모든 세그먼트가 평가됨을 나타냅니다.

```json
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
            "segmentId": "*"
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
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
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
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 세그먼트 작업에 대해 시스템에서 생성한 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 상태에 대한 잠재적 값에는 &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; 및 &quot;SUCCEEDED&quot;가 있습니다. |
| `segments` | 세그먼트 작업 내에서 반환된 세그먼트 정의에 대한 정보를 포함하는 객체입니다. |
| `segments.segment.id` | 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL로 작성된 세그먼트 정의의 표현식에 대한 정보가 포함된 객체입니다. |
| `metrics` | 세그먼트 작업에 대한 진단 정보를 포함하는 개체입니다. |

## 세그먼트 작업 일괄 검색 {#bulk-get}

에 POST 요청을 하여 여러 세그먼트 작업에 대한 자세한 정보를 검색할 수 있습니다. `/segment/jobs/bulk-get` 엔드포인트 및 제공  `id` 요청 본문에 있는 세그먼트 작업의 값입니다.

**API 형식**

```http
POST /segment/jobs/bulk-get
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs/bulk-get \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공적인 응답은 요청된 세그먼트 작업과 함께 HTTP 상태 207을 반환합니다. 그러나 의 값은 `children.segments` 속성은 세그먼트 작업이 1500개 이상의 세그먼트에 대해 실행 중인지 여부에 따라 다릅니다.

>[!NOTE]
>
>다음 응답은 공간에 대해 잘렸으며, 각 세그먼트 작업의 일부 세부 정보만 표시합니다. 전체 응답에는 요청된 세그먼트 작업에 대한 전체 세부 정보가 나열됩니다.

```json
{
    "results": {
        "cc3419d3-0389-47f1-b174-fead6b3c830d": {
            "id": "cc3419d3-0389-47f1-b174-fead6b3c830d",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
            "status": "SUCCEEDED",
            "segments": [
                {
                    "segmentId": "*"
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
| `id` | 세그먼트 작업에 대해 시스템에서 생성한 읽기 전용 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 상태에 대한 잠재적 값에는 &quot;NEW&quot;, &quot;PROCESSING&quot;, &quot;CANCELING&quot;, &quot;CANCELLED&quot;, &quot;FAILED&quot; 및 &quot;SUCCEEDED&quot;가 있습니다. |
| `segments` | 세그먼트 작업 내에서 반환된 세그먼트 정의에 대한 정보를 포함하는 객체입니다. |
| `segments.segment.id` | 세그먼트 정의의 ID입니다. |
| `segments.segment.expression` | PQL로 작성된 세그먼트 정의의 표현식에 대한 정보가 포함된 객체입니다. |

## 특정 세그먼트 작업 취소 또는 삭제 {#delete}

에 DELETE 요청을 하여 특정 세그먼트 작업을 삭제할 수 있습니다. `/segment/jobs` 엔드포인트 및 요청 경로에 삭제할 세그먼트 작업의 ID 제공

>[!NOTE]
>
>삭제 요청에 대한 API 응답은 즉시 입니다. 하지만 세그먼트 작업의 실제 삭제는 비동기적입니다. 즉, 세그먼트 작업에 대한 삭제 요청이 수행된 시점과 적용되는 시점 사이에 시간 차이가 있습니다.

**API 형식**

```http
DELETE /segment/jobs/{SEGMENT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- | 
| `{SEGMENT_JOB_ID}` | 다음 `id` 삭제할 세그먼트 작업의 값입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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

이제 이 안내서를 읽고 세그먼트 작업이 작동하는 방식을 보다 잘 이해할 수 있습니다.
