---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 스트리밍 세분화
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 스트리밍 세그멘테이션(베타)을 통해 실시간으로 이벤트 평가

>[!NOTE] 스트리밍 세그멘테이션은 베타 기능이며 요청 시 사용할 수 있습니다.

스트리밍 세그멘테이션(연속 쿼리 평가라고도 함)은 이벤트가 특정 세그먼트 그룹에 들어오면 즉시 고객을 평가할 수 있는 기능입니다. 이 기능을 사용하면 이제 데이터가 Adobe Experience Platform으로 전달되므로 대부분의 세그먼트 규칙을 평가할 수 있습니다. 즉, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.

![](../images/api/streaming-segment-evaluation.png)

## 시작하기

이 개발자 가이드는 스트리밍 세그멘테이션과 관련된 다양한 Adobe Experience Platform 서비스에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [실시간 고객 프로필](../../profile/home.md):다양한 소스의 데이터를 집계하여 실시간으로 통합된 고객 프로파일을 제공합니다.
- [세그멘테이션](../home.md):실시간 고객 프로필 데이터를 통해 세그먼트와 대상을 만들 수 있는 기능을 제공합니다.
- [XDM(Experience Data Model)](../../xdm/home.md):플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 개발자 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

- 인증:베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

경험 플랫폼의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 플랫폼의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서를](../../sandboxes/home.md)참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

특정 요청을 완료하려면 추가 헤더가 필요할 수 있습니다. 이 문서 내의 각 예에서 올바른 헤더가 표시됩니다. 모든 필수 헤더가 포함되도록 샘플 요청에 특별히 주의하십시오.

### 스트리밍 세그멘테이션 활성화 쿼리 유형

다음 표에는 서로 다른 유형의 세그멘테이션 쿼리 및 스트리밍 세그멘테이션을 지원하는지 여부가 나와 있습니다.

| 쿼리 유형 | 샘플 쿼리 | 스트리밍 세분화 지원 |
| ---------- | ------------ | --------------------------------- |
| 간단한 인구 통계 | &quot;캐나다에 있는 집 주소를 가진 모든 사람들에게 주세요.&quot; | 지원됨 |
| 시계열 이벤트 | &quot;Lightroom을 다운로드한 모든 사용자를 제공합니다.&quot; | 지원됨 |
| 인구 통계 및 시간 시리즈 | &quot;캐나다에 살고 있고 지난 30일 동안 주문을 한 모든 사람들을 저에게 주세요.&quot; | 지원됨 |
| 이벤트 부재 | &quot;이틀 안에 두 대의 카트를 모두 포기하신 분들께만 주십시오.&quot; | 지원됨 |
| 다중 엔티티 | &quot;자격 유형이 &quot;경험&quot;인 모든 사용자를 제공합니다.&quot; | 지원되지 않음 |
| 고급 PQL 함수 | &quot;지난 주에 주문한 모든 프로파일을 제공하고 구매한 모든 제품에 대한 SKU 및 이름을 포함합니다.&quot; | 지원되지 않음 |

## 모든 스트리밍 세그먼테이션 지원 세그먼트 검색

스트리밍이 가능한 새 세그먼트를 만들거나 기존 세그먼트를 업데이트하여 스트리밍이 가능하도록 하려면 먼저 스트리밍이 활성화된 모든 세그먼트 목록을 검색하여 정보를 복제하지 않아야 합니다.

**API 형식**

스트리밍이 활성화된 세그먼트를 검색하려면 쿼리 매개 변수를 요청 `evaluationInfo.continuous.enabled=true` 경로에 포함해야 합니다.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME'
```

**응답**

성공적인 응답은 IMS 조직에서 스트리밍 세그멘테이션을 사용할 수 있는 세그먼트 배열을 반환합니다.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## 스트리밍 가능 세그먼트 만들기

만들려는 세그먼트가 아직 존재하지 않음을 확인한 후 스트리밍 세그먼테이션을 사용할 수 있는 새 세그먼트를 만들 수 있습니다.

**API 형식**

```http
POST /segment/definitions
```

**요청**

다음 요청은 스트리밍 세그먼테이션이 활성화된 새 세그먼트를 만듭니다. Note that the `continuous` section is set to `enabled: true`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

>[!NOTE] 이것은 `continuous` 섹션의 추가된 매개 변수가 설정된 표준 &quot;세그먼트 만들기&quot; 요청입니다 `enabled: true`. 세그먼트 정의 만들기에 대한 자세한 내용은 [세그먼트 만들기에](../tutorials/create-a-segment.md)대한 설명서를 참조하십시오.

**응답**

성공적인 응답은 새로 만든 스트리밍 지원 세그먼트 정의의 세부 사항을 반환합니다.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## 스트리밍 세분화를 위한 기존 세그먼트 활성화

PATCH 요청 경로에 세그먼트 정의 ID를 제공하여 기존 세그먼트를 스트리밍 세그먼테이션에 사용할 수 있습니다. 또한 이 PATCH 요청의 페이로드에 기존 세그먼트 정의의 전체 세부 사항이 포함되어야 하며, 이 세부 사항은 해당 세그먼트 정의에 GET 요청을 하여 액세스할 수 있습니다.

### 기존 세그먼트 정의 찾기

기존 세그먼트 정의를 찾으려면 GET 요청의 경로에 해당 ID를 제공해야 합니다.

**API 형식**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 조회할 세그먼트 정의의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답이 성공하면 요청한 세그먼트 정의의 세부 정보가 반환됩니다.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] 다음 요청의 경우 이 응답에서 반환되는 세그먼트 정의의 전체 세부 정보가 필요합니다. 다음 요청의 본문에 사용할 이 응답의 세부 사항을 복사하십시오.

### 스트리밍 세그먼테이션을 위해 기존 세그먼트 활성화

업데이트하려는 세그먼트의 세부 사항을 알고 있으므로 PATCH 요청을 수행하여 세그먼트를 업데이트하여 스트리밍 세그먼테이션을 활성화할 수 있습니다.

**API 형식**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**요청**

다음 요청의 페이로드는 [이전 단계에서](#look-up-an-existing-segment-definition)얻은 세그먼트 정의의 세부 사항을 제공하고, 해당 `continuous.enabled` 속성을 `true`로 변경하여 업데이트합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    }
}'
```

**응답**

성공적인 응답은 새로 업데이트된 세그먼트 정의의 세부 사항을 반환합니다.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## 예약된 평가 사용

스트리밍 평가가 활성화되면 베이스라인을 만들어야 합니다(그 이후는 항상 최신 상태로 유지됨). 이 작업은 시스템에 의해 자동으로 수행되지만, 먼저 예약된 평가(예약된 세그멘테이션이라고도 함)가 활성화되어야 기본 설정이 적용됩니다.

IMS 조직에서 예약된 세그먼테이션을 사용하여 반복 일정을 만들어 세그먼트를 평가하는 내보내기 작업을 자동으로 실행할 수 있습니다.

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

## 다음 단계

이제 스트리밍 세그먼테이션을 위해 새 세그먼트와 기존 세그먼트를 모두 활성화하고 기준 개발 및 반복 평가를 수행하기 위해 예약된 세그멘테이션을 활성화했으므로 조직의 세그먼트를 만들 수 있습니다.

유사한 작업을 수행하고 Adobe Experience Platform 사용자 인터페이스를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 세그먼트 빌더 [사용 안내서를](../ui/overview.md)참조하십시오.