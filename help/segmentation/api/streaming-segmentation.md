---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;streaming segmentation;Streaming segmentation;Continuous evaluation;
solution: Experience Platform
title: 스트리밍 세분화
topic: developer guide
description: 이 문서에는 스트리밍 세그멘테이션 API와 함께 스트리밍 세그멘테이션을 사용하는 방법에 대한 예가 나와 있습니다.
translation-type: tm+mt
source-git-commit: 2bd4b773f7763ca408b55e3b0e2d0bbe9e7b66ba
workflow-type: tm+mt
source-wordcount: '1310'
ht-degree: 1%

---


# 스트리밍 세분화를 통해 거의 실시간으로 이벤트 평가

>[!NOTE]
>
>다음 문서에서는 API를 사용하여 스트리밍 세그멘테이션을 사용하는 방법을 설명합니다. UI를 사용한 스트리밍 세그멘테이션 사용에 대한 자세한 내용은 [스트리밍 세그멘테이션 UI 안내서를 참조하십시오](../ui/streaming-segmentation.md).

스트리밍 세그먼테이션을 통해 [!DNL Adobe Experience Platform] 고객은 데이터 풍부함에 주력하면서 거의 실시간으로 세분화할 수 있습니다. 스트리밍 세분화를 통해 이제 데이터가 스트리밍되는 즉시 세그먼트 자격 조건 [!DNL Platform]이 충족되므로 세분화 작업을 예약하고 실행할 필요가 없습니다. 이 기능을 사용하면 이제 데이터가 전달될 때 대부분의 세그먼트 규칙을 평가할 수 [!DNL Platform]있으므로, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>스트리밍 세그먼테이션은 플랫폼으로 스트리밍되는 데이터를 평가하는 데에만 사용할 수 있습니다. 즉, 일괄 처리를 통해 수집되는 데이터는 스트리밍 세그멘테이션을 통해 평가되지 않으며, 야간 세그먼트화된 작업과 함께 평가됩니다.

## 시작하기

이 개발자 가이드는 스트리밍 세그멘테이션과 관련된 다양한 [!DNL Adobe Experience Platform] 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 한 통합 소비자 프로필을 실시간으로 제공합니다.
- [[!DNL Segmentation]](../home.md):데이터에서 세그먼트 및 대상을 만들 수 있는 기능을 [!DNL Real-time Customer Profile] 제공합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 [!DNL Platform] 제공합니다.

### 샘플 API 호출 읽기

이 개발자 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

특정 요청을 완료하려면 추가 헤더가 필요할 수 있습니다. 이 문서 내의 각 예에서 정확한 헤더가 표시됩니다. 모든 필수 헤더가 포함되도록 샘플 요청에 특별히 주의하십시오.

### 스트리밍 세그멘테이션 사용 쿼리 유형 {#streaming-segmentation-query-types}

>[!NOTE]
>
>스트리밍 세그멘테이션이 작동하려면 조직에 대해 예약된 세그멘테이션을 활성화해야 합니다. 예약된 세그멘테이션 활성화에 대한 정보는 [예약 세그멘테이션 활성화 섹션에서 찾을 수 있습니다](#enable-scheduled-segmentation)

스트리밍 세그먼테이션을 사용하여 세그먼트를 평가하려면 쿼리는 다음 지침을 따라야 합니다.

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 들어오는 히트 | 시간 제한 없이 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의 |
| 상대 시간 창 내의 들어오는 히트 | 단일 들어오는 이벤트를 참조하는 세그먼트 정의입니다. |
| 프로필 전용 | 프로필 속성만 참조하는 모든 세그먼트 정의 |
| 프로필을 참조하는 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하는 세그먼트 정의 및 하나 이상의 프로필 속성. |
| 상대 시간 창 내의 프로파일을 참조하는 들어오는 히트 | 단일 들어오는 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의입니다. |
| 프로파일을 참조하는 여러 이벤트 | 지난 24시간 **** 이내에 여러 이벤트를 참조하고 (선택 사항) 하나 이상의 프로필 속성을 포함하는 세그먼트 정의입니다. |

다음 시나리오에서는 세그먼트 정의를 스트리밍 세그먼테이션에 사용할 수 **없습니다** .

- 세그먼트 정의에는 Adobe Audience Manager(AAM) 세그먼트 또는 트레이트가 포함됩니다.
- 세그먼트 정의에는 여러 엔티티(다중 엔티티 쿼리)가 포함됩니다.

또한 스트리밍 세그먼테이션을 수행할 때 다음과 같은 지침이 적용됩니다.

| 쿼리 유형 | 지침 |
| ---------- | -------- |
| 단일 이벤트 쿼리 | 룩백 창에는 제한이 없습니다. |
| 이벤트 내역이 있는 쿼리 | <ul><li>룩백 창은 **하루로 제한됩니다**.</li><li>이벤트 간에 엄격한 시간 순서 조건이 **있어야** 합니다.</li><li>하나 이상의 부정 이벤트가 있는 쿼리가 지원됩니다. 하지만 전체 이벤트는 부정일 **수** 없습니다.</li></ul> |

## 스트리밍 세그멘테이션에 대해 활성화된 모든 세그먼트 검색

IMS 조직 내에서 세그먼테이션을 스트리밍하도록 활성화된 모든 세그먼트 목록을 검색하여 종단점에 GET 요청을 `/segment/definitions` 할 수 있습니다.

**API 형식**

스트리밍이 활성화된 세그먼트를 검색하려면 요청 경로 `evaluationInfo.continuous.enabled=true` 에 쿼리 매개 변수를 포함해야 합니다.

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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답으로 IMS 조직의 세그먼트 배열을 반환합니다. 이 경우 스트리밍 세그멘테이션이 활성화됩니다.

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

세그먼트는 위에 나열된 [스트리밍 세그멘테이션 유형 중 하나와 일치하는 경우 자동으로 스트리밍이 활성화됩니다](#streaming-segmentation-query-types).

**API 형식**

```http
POST /segment/definitions
```

**요청**

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
    }
}'
```

>[!NOTE]
>
>표준 &quot;세그먼트 만들기&quot; 요청입니다. 세그먼트 정의를 만드는 방법에 대한 자세한 내용은 세그먼트 [만들기에 대한 자습서를 참조하십시오](../tutorials/create-a-segment.md).

**응답**

성공적인 응답은 새로 만든 스트리밍 가능 세그먼트 정의에 대한 세부 사항을 반환합니다.

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

## 예약된 평가 사용 {#enable-scheduled-segmentation}

스트리밍 평가가 활성화되면 베이스라인을 만들어야 합니다(그 이후는 항상 최신 상태로 유지됨). 시스템에서 자동으로 기준 지정을 수행하려면 먼저 예약된 평가(예약된 세그멘테이션이라고도 함)를 활성화해야 합니다. IMS 조직에서는 예약된 세그먼테이션을 통해 반복되는 일정을 준수하여 세그먼트를 평가하는 내보내기 작업을 자동으로 실행할 수 있습니다.

>[!NOTE]
>
>최대 5개의 병합 정책을 포함하는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다 [!DNL XDM Individual Profile]. 조직에서 단일 샌드박스 환경 [!DNL XDM Individual Profile] 에 대해 5개 이상의 병합 정책을 보유하고 있는 경우 예약된 평가를 사용할 수 없습니다.

### 일정 만들기

종단점에 POST 요청을 함으로써 일정을 만들고 일정을 트리거해야 하는 특정 시간을 포함할 수 `/config/schedules` 있습니다.

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
| `properties.segments` | **( `type` 등호 시 `batch_segmentation`필수)** 을 사용하면 `["*"]` 모든 세그먼트가 포함됩니다. |
| `schedule` | **(필수)** 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약하면 됩니다. 즉, 24시간 동안 두 번 이상 작업이 실행되도록 예약할 수 없습니다. 표시된 예(`0 0 1 * * ?`)는 작업이 매일 1:00:00 UTC에 트리거됨을 의미합니다. 자세한 내용은 [cron 식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. |
| `state` | *(선택 사항)* 예약 상태를 포함하는 문자열. 사용 가능한 값: `active` 및 `inactive`. 기본값은 `inactive`입니다. IMS 조직은 하나의 예약만 만들 수 있습니다. 일정을 업데이트하는 단계는 이 자습서의 후반부에서 확인할 수 있습니다. |

**응답**

성공적인 응답은 새로 만든 일정의 세부 사항을 반환합니다.

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

기본적으로, 속성이 만들기(POST) 요청 본문에 로 설정되어 있지 않은 이상 `state` 만들어진 경우 일정 `active` 은 비활성화됩니다. 종단점에 PATCH 요청을 만들고 경로에 있는 일정 `state` 의 ID를 포함하여 일정(설정 `active``/config/schedules` )을 활성화할 수 있습니다.

**API 형식**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**요청**

다음 요청에서는 [JSON 패치 서식](http://jsonpatch.com/) 을 사용하여 일정 `state` 을 다음으로 업데이트합니다 `active`.

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

이제 스트리밍 세그먼테이션을 위해 새 세그먼트와 기존 세그먼트를 모두 활성화하고, 기준 요소를 개발하고 반복적인 평가를 수행하는 예약된 세그먼테이션을 활성화했으므로 조직의 세그먼트를 만들기 시작할 수 있습니다.

유사한 작업을 수행하고 Adobe Experience Platform 사용자 인터페이스를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 [세그먼트 빌더 사용자 안내서를 참조하십시오](../ui/segment-builder.md).