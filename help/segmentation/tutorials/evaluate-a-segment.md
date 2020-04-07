---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 세그먼트 평가
topic: tutorial
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# 세그먼트 결과 평가 및 액세스

이 문서에서는 세그멘테이션 API를 사용하여 세그먼트를 평가하고 세그먼트 결과에 액세스하는 [자습서를 제공합니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## 시작하기

이 자습서에서는 대상 세그먼트 만들기와 관련된 다양한 Adobe Experience Platform 서비스에 대해 잘 이해해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 실시간으로 통합된 고객 프로파일을 제공합니다.
- [Adobe Experience Platform 세그멘테이션 서비스](../home.md):실시간 고객 프로필 데이터를 통해 고객 세그먼트를 만들 수 있습니다.
- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필수 헤더

또한 이 자습서에서는 플랫폼 API를 성공적으로 호출하려면 [인증 자습서를](../../tutorials/authentication.md) 완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

모든 POST, PUT 및 PATCH 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

## 세그먼트 평가

세그먼트 정의를 개발, 테스트 및 저장한 후에는 예약된 평가 또는 주문형 평가를 통해 세그먼트를 평가할 수 있습니다.

[예약된 평가](#scheduled-evaluation) (&#39;예약된 세그멘테이션&#39;이라고도 함)를 사용하면 특정 시간에 내보내기 작업을 실행하기 위한 반복 일정을 만들 수 있지만, [on-demand 평가는](#on-demand-evaluation) 세그먼트 작업을 만들어 대상을 즉시 만듭니다. 각 단계에 대한 지침은 아래에 요약되어 있습니다.

실시간 고객 프로필 API [자습서를 사용하여 세그먼트 만들기](./create-a-segment.md) 자습서를 아직 완료하지 않았거나 세그먼트 빌더를 사용하여 세그먼트 정의를 만든 [경우에는](../ui/overview.md)이 자습서를 진행하기 전에 먼저수행하십시오.

## 예약된 평가

예약된 평가를 통해 IMS 조직에서 반복 일정을 생성하여 자동으로 내보내기 작업을 실행할 수 있습니다.

>[!NOTE] XDM 개별 프로필에 대해 최대 5개의 병합 정책을 포함하는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다. 조직에서 단일 샌드박스 환경 내에서 XDM 개별 프로필에 대한 병합 정책이 5개 이상 있는 경우 예약된 평가를 사용할 수 없습니다.

### 일정 만들기

종단점에 POST 요청을 함으로써 일정을 만들고 일정을 실행해야 하는 특정 시간을 포함할 수 있습니다. `/config/schedules`

**API 형식**

```http
POST /config/schedules
```

**요청**

다음 요청은 페이로드에 제공된 사양에 따라 새 일정을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | **(필수)** 예약의 이름입니다. 문자열이어야 합니다. |
| `type` | **(필수)** 문자열 형식의 작업 유형입니다. 지원되는 유형은 `batch_segmentation` 및 `export`입니다. |
| `properties` | **(필수)** 예약과 관련된 추가 속성이 포함된 개체입니다. |
| `properties.segments` | **(`type`등일 때 필수)`batch_segmentation`** `["*"]` 을 사용하면 모든 세그먼트가 포함됩니다. |
| `schedule` | **(필수)** 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있으므로 24시간 동안 두 번 이상 실행되도록 작업을 예약할 수 없습니다. 표시된 예(`0 0 1 * * ?`)는 작업이 매일 1시 00분 UTC에 트리거됨을 의미합니다. 자세한 내용은 [cron 식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. |
| `state` | *(선택 사항)* 예약 상태를 포함하는 문자열입니다. 사용 가능한 값: `active` 및 `inactive`Adobe 기본값은 `inactive`입니다. IMS 조직은 하나의 스케줄만 생성할 수 있습니다. 일정을 업데이트하는 단계는 이 자습서의 후반부에서 확인할 수 있습니다. |

**응답**

성공적인 응답은 새로 만든 일정에 대한 세부 정보를 반환합니다.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### 일정 활성화

기본적으로 POST(Create) 요청 본문에 `state` 속성이 `active` 설정되어 있지 않으면 예약은 만들어지면 비활성화됩니다. PATCH 요청을 `state` 끝점에 만들고 경로에 예약의 ID를 포함하여 일정을 활성화(설정 `active``/config/schedules` )할 수 있습니다.

**API 형식**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**요청**

다음 요청에서는 [JSON 패치 서식을](http://jsonpatch.com/) 사용하여 `state` 일정의 내용을 `active`업데이트합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**응답**

업데이트가 성공하면 빈 응답 본문과 HTTP 상태 204(콘텐츠 없음)가 반환됩니다.

동일한 작업을 사용하여 이전 요청의 &quot;값&quot;을 &quot;비활성&quot;으로 대체하여 일정을 비활성화할 수 있습니다.

### 예약 시간 업데이트

종단점에 PATCH 요청을 만들고 경로에 예약의 ID를 포함하여 예약 시간을 업데이트할 수 `/config/schedules` 있습니다.

**API 형식**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**요청**

다음 요청에서는 일정에 대한 [cron 표현식을](http://jsonpatch.com/) 업데이트하기 위해 JSON 패치 서식을 [](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 사용합니다. 이 예에서는 일정이 이제 10:15:00 UTC에 트리거됩니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**응답**

업데이트가 성공하면 빈 응답 본문과 HTTP 상태 204(콘텐츠 없음)가 반환됩니다.

## On-Demand 평가

주문형 평가를 통해 필요할 때마다 대상 세그먼트를 생성하기 위해 세그먼트 작업을 만들 수 있습니다. 예약된 평가와 달리, 이 문제는 요청이 있을 때만 발생하며 반복되지 않습니다.

### 세그먼트 작업 만들기

세그먼트 작업은 새 대상 세그먼트를 만드는 비동기 프로세스입니다. 세그먼트 정의뿐만 아니라 실시간 고객 프로파일을 프로필 조각에 겹치는 속성을 병합하는 방법을 제어하는 모든 병합 정책을 참조합니다. 세그먼트 작업이 성공적으로 완료되면 처리 중에 발생한 오류와 대상의 최종 크기 등 세그먼트에 대한 다양한 정보를 수집할 수 있습니다.

실시간 고객 프로필 API에서 `/segment/jobs` 끝점에 대한 POST 요청을 만들어 새 세그먼트 작업을 만들 수 있습니다.

**API 형식**

```http
POST /segment/jobs
```

**요청**

다음 요청은 페이로드에 제공된 두 세그먼트 정의를 기반으로 새 세그먼트 작업을 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `segmentId` | 대상을 빌드할 세그먼트 정의의 식별자입니다. 페이로드 배열에서 하나 이상의 세그먼트 ID를 제공해야 합니다. |

**응답**

성공적인 응답은 이 세그먼트 작업에 고유한 읽기 전용 시스템 생성 값을 포함하여 새로 만든 세그먼트 작업의 세부 사항을 반환합니다. `id`

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 조회 목적으로 사용되는 새 세그먼트 작업의 식별자입니다. |
| `status` | 세그먼트 작업의 현재 상태입니다. 처리가 완료될 때까지 &quot;PROCESSING&quot;이 되며, 이 시점에서 &quot;SUCCESS&quot; 또는 &quot;FAILED&quot;가 됩니다. |

### 세그먼트 작업 상태 조회

특정 세그먼트 작업에 `id` 대한 GET(조회 요청)을 사용하여 작업의 현재 상태를 볼 수 있습니다.

**API 형식**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | 액세스하려는 세그먼트 `id` 작업 |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 세그멘테이션 작업의 세부 사항을 반환하고 작업의 현재 상태에 따라 다른 정보를 제공합니다. &quot;SUCCESS&quot;에 `status` 도달할 때까지 조회 요청을 반복할 수 있습니다. 이 때 세그먼트를 데이터 세트로 내보낼 수 있습니다.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `segmentedProfileCounter` | 세그먼트에 적합한 병합된 프로필의 총 수입니다. |
| `segmentedProfileByNamespaceCounter` | ID 네임스페이스 코드별로 세그먼트를 자격을 규정하는 프로필의 분류입니다. ID 네임스페이스 코드 목록은 [ID 네임스페이스 개요에서](../../identity-service/namespaces.md)찾을 수 있습니다. |

## 세그먼트 결과 해석

세그먼트 작업이 성공적으로 실행되면 세그먼트 내에 포함된 각 프로필에 대해 `segmentMembership` 맵이 업데이트됩니다. `segmentMembership` 또한 Adobe Audience Manager와 같은 다른 솔루션과 통합할 수 있도록 인제스트된 사전 평가 대상 세그먼트를 플랫폼에 저장합니다.

다음 예는 각 개별 프로필 레코드에 대한 `segmentMembership` 속성의 모양을 보여줍니다.

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `lastQualificationTime` | 세그먼트 멤버십의 어설션이 수행되고 프로필이 세그먼트를 입력하거나 종료한 타임스탬프. |
| `status` | 현재 요청의 일부로서 세그먼트 기여도 상태입니다. 다음 알려진 값 중 하나와 같아야 합니다. <ul><li>`existing`:엔티티는 세그먼트에 계속 있습니다.</li><li>`realized`:엔티티가 세그먼트를 입력하고 있습니다.</li><li>`exited`:엔티티가 세그먼트를 종료합니다.</li></ul> |

## 세그먼트 결과 액세스

다음 두 가지 방법 중 하나로 세그먼트 작업의 결과에 액세스할 수 있습니다.개별 프로필에 액세스하거나 전체 대상을 데이터 세트로 내보낼 수 있습니다.

다음 섹션에서는 이러한 옵션에 대해 자세히 설명합니다.

## 프로필 찾기

사용하려는 특정 프로필을 알고 있는 경우 실시간 고객 프로필 API를 사용하여 액세스할 수 있습니다. 개별 프로필에 액세스하는 전체 단계는 프로필 API [자습서를 사용하여 실시간 고객 프로필 데이터에 액세스하십시오](../../profile/api/entities.md) .

## 세그먼트 내보내기

세그멘테이션 작업이 성공적으로 완료된 후( `status` 속성 값이 &quot;성공&quot;됨), 대상을 액세스 및 작동 가능한 데이터 세트로 내보낼 수 있습니다.

대상을 내보내려면 다음 단계가 필요합니다.

- [대상 데이터 집합](#create-a-target-dataset) 만들기 - 대상 구성원을 포함할 데이터 집합을 만듭니다.
- [데이터 세트에서](#generate-profiles-for-audience-members) 고객 프로필 생성 - 세그먼트 작업 결과를 기반으로 XDM 개별 프로필로 데이터 세트를 채웁니다.
- [내보내기 진행](#monitor-export-progress) 모니터링 - 내보내기 프로세스의 현재 진행 상태를 확인합니다.
- [고객 데이터](#next-steps) 읽기 - 대상 구성원을 나타내는 결과 XDM 개별 프로필을 검색합니다.

### 타겟 데이터 세트 만들기

대상을 내보낼 때 타겟 데이터 세트를 먼저 만들어야 합니다. 데이터 세트를 올바르게 구성하여 내보내기가 제대로 수행되도록 해야 합니다.

중요한 고려 사항 중 하나는 데이터 세트가 기반으로 하는 스키마입니다(`schemaRef.id` 아래 API 샘플 요청에서). 세그먼트를 내보내려면 데이터 집합이 XDM 개인 프로필 조합 스키마(`https://ns.adobe.com/xdm/context/profile__union`)를 기반으로 해야 합니다. 공용 스키마는 XDM 개별 프로필 클래스인 동일한 클래스를 공유하는 스키마 필드를 집계하는 시스템 생성 읽기 전용 스키마입니다. 결합 보기 스키마에 대한 자세한 내용은 스키마 레지스트리 [개발자 안내서의](../../xdm/api/getting-started.md)실시간 고객 프로필 섹션을 참조하십시오.

다음 두 가지 방법으로 필요한 데이터 세트를 만들 수 있습니다.

- **API 사용:** 이 튜토리얼의 다음 단계에서는 카탈로그 API를 사용하여 XDM 개별 프로필 조합 스키마를 참조하는 데이터 세트를 만드는 방법에 대해 간략하게 설명합니다.
- **UI 사용:** Adobe Experience Platform 사용자 인터페이스를 사용하여 통합 스키마를 참조하는 데이터 세트를 만들려면 UI 자습서의 [](../ui/overview.md) 단계를 수행한 다음 이 자습서로 돌아가서 대상 프로필을 [생성하는 단계를 계속 진행합니다](#generate-xdm-profiles-for-audience-members).

이미 호환되는 데이터 세트가 있고 ID를 알고 있는 경우 대상 프로필을 [생성하기 위해](#generate-xdm-profiles-for-audience-members)바로 단계를 진행할 수 있습니다.

**API 형식**

```http
POST /dataSets
```

**요청**

다음 요청은 페이로드에 구성 매개 변수를 제공하여 새 데이터 세트를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "aspect": "production"
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 데이터 세트에 대한 설명 이름입니다. |
| `schemaRef.id` | 데이터 집합에 연결할 통합 보기(스키마)의 ID입니다. |
| `fileDescription.persisted` | 로 설정되면 `true`통합 보기에서 데이터 세트가 유지될 수 있도록 하는 부울 값입니다. |

**응답**

성공적인 응답은 새로 만든 데이터 세트에 대한 읽기 전용 시스템 생성 고유 ID가 포함된 배열을 반환합니다. 대상 구성원을 성공적으로 내보내려면 제대로 구성된 데이터 집합 ID가 필요합니다.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 대상 구성원을 위한 프로필 생성

결합 지속 데이터 세트를 만들었으면 실시간 고객 프로필 API의 `/export/jobs` 끝점에 대한 POST 요청을 만들고 내보내려는 세그먼트에 대한 데이터 집합 ID 및 세그먼트 정보를 제공하여 대상 구성원을 데이터 집합으로 유지하는 내보내기 작업을 만들 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
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
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `fields` | *(선택 사항)* 내보내기에 포함할 데이터 필드를 이 매개 변수에 제공된 필드로만 제한합니다. 세그먼트를 만들 때도 동일한 매개 변수를 사용할 수 있으므로 세그먼트의 필드가 이미 필터링되었을 수 있습니다. 이 값을 생략하면 내보낸 데이터에 모든 필드가 포함됩니다. |
| `mergePolicy` | *(선택 사항)* 내보낸 데이터를 제어하는 병합 정책을 지정합니다. 내보낼 세그먼트가 여러 개 있을 경우 이 매개 변수를 포함하십시오. 이 값을 생략하면 Export Service가 세그먼트에서 제공하는 병합 정책을 사용하게 됩니다. |
| `mergePolicy.id` | 병합 정책의 ID |
| `mergePolicy.version` | 사용할 병합 정책의 특정 버전입니다. 이 값을 생략하면 기본적으로 최신 버전이 사용됩니다. |
| `filter` | *(선택 사항)* 내보내기 전에 세그먼트에 적용할 다음 필터 중 하나 이상을 지정합니다. |
| `filter.segments` | *(선택 사항)* 내보낼 세그먼트를 지정합니다. 이 값을 생략하면 모든 프로필의 모든 데이터가 내보내집니다. 다음 필드를 포함하는 세그먼트 개체의 배열을 수락합니다. |
| `filter.segments.segmentId` | **(사용하는 경우 필수`segments`)** 내보낼 프로필의 세그먼트 ID입니다. |
| `filter.segments.segmentNs` | *(선택 사항)* 주어진 세그먼트 `segmentID`네임스페이스입니다. |
| `filter.segments.status` | *(선택 사항)* 에 대한 상태 필터를 제공하는 문자열 `segmentID`배열입니다. 기본적으로 `status` 는 현재 시간에 세그먼트에 속하는 모든 프로파일을 나타내는 값을 `["realized", "existing"]` 가집니다. 가능한 값은 다음과 같습니다. `"realized"`및 `"existing"`를 `"exited"`참조하십시오. |
| `filter.segmentQualificationTime` | *(선택 사항)* 세그먼트 자격 조건 시간을 기반으로 필터링합니다. 시작 시간 및/또는 종료 시간을 제공할 수 있습니다. |
| `filter.segmentQualificationTime.startTime` | *(선택 사항)* 주어진 상태에 대한 세그먼트 ID에 대한 세그먼트 자격 시작 시간입니다. 제공되지 않으며 세그먼트 ID 자격에 대한 시작 시간에 필터가 없습니다. 타임스탬프는 RFC 3339 [형식으로 제공되어야 합니다](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(선택 사항)* 주어진 상태에 대한 세그먼트 ID에 대한 세그먼트 자격 종료 시간입니다. 제공되지 않으며 세그먼트 ID 자격 부여의 종료 시간에 필터가 없습니다. 타임스탬프는 RFC 3339 [형식으로 제공되어야 합니다](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` | *(선택 사항)* 내보낸 프로필을 이 타임스탬프 이후에 업데이트된 프로필만 포함하도록 제한합니다. 타임스탬프는 RFC 3339 [형식으로 제공되어야 합니다](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` for **profiles**, if provided | 병합된 업데이트된 타임스탬프가 지정된 타임스탬프보다 큰 병합된 프로필을 모두 포함합니다. 피연산자를 `greater_than` 지원합니다. |
| `filter.fromTimestamp` 이벤트 | 이 타임스탬프 이후에 인제스트된 모든 이벤트는 결과 프로필 결과에 따라 내보내집니다. 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다. |
| `filter.emptyProfiles` | *(선택 사항)* 부울 값. 프로필에는 프로필 레코드, ExperienceEvent 레코드 또는 둘 다를 포함할 수 있습니다. 프로필 레코드가 없고 ExperienceEvent 레코드만 있는 프로필을 &quot;emptyProfiles&quot;라고 합니다. &quot;emptyProfiles&quot;를 포함하여 프로필 저장소에서 모든 프로필을 내보내려면 `emptyProfiles` 의 값을 `true`로 설정합니다. 로 `emptyProfiles` 설정하면 `false`저장소에 프로필 레코드가 있는 프로필만 내보내집니다. 기본적으로 속성이 포함되지 않은 경우 `emptyProfiles` 프로필 레코드가 포함된 프로파일만 내보내집니다. |
| `additionalFields.eventList` | *(선택 사항)* 다음 설정 중 하나 이상을 제공하여 하위 또는 관련 개체에 대해 내보낸 시계열 이벤트 필드를 제어합니다. |
| `additionalFields.eventList.fields` | 내보낼 필드를 제어합니다. |
| `additionalFields.eventList.filter` | 관련 개체에서 포함된 결과를 제한하는 기준을 지정합니다. 내보내기에 필요한 최소 값(일반적으로 날짜)이 필요합니다. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | 제공된 타임스탬프 이후에 인제스트된 이벤트까지 시간 시리즈 이벤트를 필터링합니다. 이벤트 시간 자체가 아니라 이벤트에 대한 수집 시간입니다. |
| `destination` | **(필수)** 내보낸 데이터의 대상 정보 |
| `destination.datasetId` | **(필수)** 데이터를 내보낼 데이터 집합의 ID입니다. |
| `destination.segmentPerBatch` | *(선택 사항)* 제공되지 않는 경우 기본적으로 `false`설정되는 부울 값입니다. 값이 모든 세그먼트 ID를 단일 배치 ID로 `false` 내보냅니다. 한 세그먼트 ID를 하나의 배치 ID로 `true` 내보내는 값입니다. 값을 설정할 경우 일괄 내보내기 성능에 영향을 줄 `true` 수 있습니다. |
| `schema.name` | **(필수)** 데이터를 내보낼 데이터 세트와 연결된 스키마의 이름입니다. |

**응답**

성공적인 응답은 세그먼트 작업의 마지막 완료된 실행에 대해 자격이 있는 프로필로 채워진 데이터 세트를 반환합니다. 이전에 데이터 세트에 존재했지만 세그먼트 작업의 마지막 완료된 실행 동안 세그먼트에 적합하지 않은 모든 프로필이 제거되었습니다.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

요청에 포함되지 `destination.segmentPerBatch` 않았거나(없을 경우, 기본값이 `false`으로 설정됨), 또는 값이 로 설정된 경우 위의 응답에 있는 `false`개체에 `destination` 배열이 없고, 대신 아래에 표시된 것처럼 하나의 `batches` `batchId`배열만 포함됩니다. 이 단일 배치에는 모든 세그먼트 ID가 포함되는 반면 위의 응답에는 배치 ID당 단일 세그먼트 ID가 표시됩니다.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### 모든 내보내기 작업 나열

특정 IMS에 대한 모든 내보내기 작업 목록을 `export/jobs` 끝점에 GET 요청을 수행하여 반환할 수 있습니다. 또한 요청은 쿼리 매개 변수를 `limit` 지원하며 `offset`아래와 같이 지원합니다.

**API 형식**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| 속성 | 설명 |
| -------- | ----------- |
| `limit` | 반환할 레코드 수를 지정합니다. |
| `offset` | 제공된 번호로 반환할 결과 페이지를 오프셋합니다. |


**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

응답에는 IMS 조직에서 만든 내보내기 작업이 포함된 `records` 개체가 포함됩니다.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
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

### 내보내기 진행 상태 모니터링

내보내기 작업 프로세스에서는 `/export/jobs` 종단점에 GET 요청을 만들고 경로에 내보내기 작업의 `id` 내용을 포함하여 해당 상태를 모니터링할 수 있습니다. 필드가 &quot;SUCCESS&quot; 값을 반환하면 내보내기 작업이 `status` 완료됩니다.

**API 형식**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 액세스하려는 내보내기 `id` 작업 |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
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
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `batchId` | 대상 데이터를 읽을 때 조회 목적으로 사용할 성공적인 내보내기에서 생성된 배치의 식별자입니다. |

## 다음 단계

내보내기가 성공적으로 완료되면 Experience Platform의 Data Lake 내에서 데이터를 사용할 수 있습니다. 그런 다음 데이터 액세스 [API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 사용하여 내보내기와 `batchId` 연결된 데이터를 사용하여 데이터에 액세스할 수 있습니다. 세그먼트 크기에 따라 데이터가 청크 단위일 수 있으며 일괄 처리는 여러 파일로 구성될 수 있습니다.

데이터 액세스 API를 사용하여 배치 파일에 액세스하고 다운로드하는 방법에 대한 단계별 지침을 보려면 데이터 액세스 [자습서를](../../data-access/tutorials/dataset-data.md)따르십시오.

Adobe Experience Platform 쿼리 서비스를 사용하여 성공적으로 내보낸 세그먼트 데이터에 액세스할 수도 있습니다. UI 또는 RESTful API를 사용하여 쿼리 서비스를 사용하여 데이터 레이크 내의 데이터에 대한 쿼리를 작성, 유효성 확인 및 실행할 수 있습니다.

대상 데이터를 쿼리하는 방법에 대한 자세한 내용은 쿼리 서비스 [설명서를](../../query-service/home.md)참조하십시오.
