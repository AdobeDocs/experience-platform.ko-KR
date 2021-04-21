---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;스트리밍 세그멘테이션;연속 평가
solution: Experience Platform
title: '스트리밍 세분화를 통해 거의 실시간으로 이벤트 평가 '
topic-legacy: developer guide
description: 이 문서에는 Adobe Experience Platform 세그멘테이션 서비스 API에서 스트리밍 세그멘테이션을 사용하는 방법에 대한 예가 포함되어 있습니다.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 1%

---

# 스트리밍 세분화를 통해 거의 실시간으로 이벤트 평가

>[!NOTE]
>
>다음 문서에서는 API를 사용하여 스트리밍 세그멘테이션을 사용하는 방법을 설명합니다. UI를 사용한 스트리밍 세그멘테이션 사용에 대한 자세한 내용은 [스트리밍 세그멘테이션 UI 안내서](../ui/streaming-segmentation.md)를 참조하십시오.

[!DNL Adobe Experience Platform]의 스트리밍 세그먼테이션을 통해 고객은 데이터 풍부함에 주력하면서 거의 실시간으로 세그먼테이션을 수행할 수 있습니다. 스트리밍 세그먼테이션을 통해 이제 스트리밍 데이터가 [!DNL Platform]에 도달하면 세그먼트 자격이 부여되므로 세그먼테이션 작업을 예약하고 실행할 필요가 없습니다. 이 기능을 사용하면 이제 데이터가 [!DNL Platform]에 전달되므로 대부분의 세그먼트 규칙을 평가할 수 있습니다. 즉, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>스트리밍 세그먼테이션은 플랫폼으로 스트리밍된 데이터를 평가하는 데에만 사용할 수 있습니다. 즉, 일괄 처리를 통해 처리된 데이터는 스트리밍 세그멘테이션을 통해 평가되지 않으며, 야간 세그먼트화된 작업과 함께 평가됩니다.

## 시작하기

이 개발자 가이드는 스트리밍 세그멘테이션과 관련된 다양한 [!DNL Adobe Experience Platform] 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스의 데이터를 집계하여 실시간으로 통합 소비자 프로파일을 제공합니다.
- [[!DNL Segmentation]](../home.md):데이터에서 세그먼트와 대상을 만드는 기능을  [!DNL Real-time Customer Profile] 제공합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크

다음 섹션에서는 [!DNL Platform] API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 개발자 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

특정 요청을 완료하려면 추가 헤더가 필요할 수 있습니다. 이 문서의 각 예제에 올바른 머리글이 표시됩니다. 모든 필수 헤더가 포함되도록 샘플 요청에 특별히 주의하십시오.

### 스트리밍 세그먼테이션 사용 쿼리 유형 {#streaming-segmentation-query-types}

>[!NOTE]
>
>스트리밍 세그먼테이션이 작동하려면 조직에 대해 예약된 세그먼테이션을 활성화해야 합니다. 예약된 세그멘테이션 활성화에 대한 정보는 [예약된 세그멘테이션 활성화 섹션](#enable-scheduled-segmentation)에서 확인할 수 있습니다.

스트리밍 세그먼테이션을 사용하여 세그먼트를 평가하려면 쿼리는 다음 지침을 따라야 합니다.

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하는 모든 세그먼트 정의 |
| 상대 시간 창 내에서 들어오는 히트 | 단일 들어오는 이벤트를 참조하는 모든 세그먼트 정의 |
| 시간 창으로 들어오는 히트 | 시간 창이 있는 단일 들어오는 이벤트를 참조하는 세그먼트 정의입니다. |
| 프로필 전용 | 프로필 속성만 참조하는 모든 세그먼트 정의 |
| 프로필을 참조하는 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하고 하나 이상의 프로필 속성을 참조하는 세그먼트 정의입니다. |
| 상대 시간 창 내의 프로파일을 참조하는 들어오는 히트 | 단일 들어오는 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의입니다. |
| 세그먼트 | 하나 이상의 일괄 처리 또는 스트리밍 세그먼트를 포함하는 모든 세그먼트 정의 |
| 프로파일을 참조하는 여러 이벤트 | 지난 24시간 이내에 여러 이벤트 **을 참조하고 (선택 사항) 하나 이상의 프로필 특성이 있는 세그먼트 정의입니다.** |

세그먼트 정의는 다음 시나리오에서 스트리밍 세그먼테이션에 대해 **활성화되지 않습니다.**.

- 세그먼트 정의에는 Adobe Audience Manager(AAM) 세그먼트 또는 트레이트가 포함됩니다.
- 세그먼트 정의에는 여러 엔티티(다중 엔티티 쿼리)가 포함됩니다.

또한 스트리밍 세분화를 수행할 때 다음과 같은 지침이 적용됩니다.

| 쿼리 유형 | 지침 |
| ---------- | -------- |
| 단일 이벤트 쿼리 | 전환 확인 창에는 제한이 없습니다. |
| 이벤트 내역이 있는 쿼리 | <ul><li>조회 창은 **1일**&#x200B;로 제한됩니다.</li><li>이벤트 사이에 엄격한 시간 순서 조건 **이 있어야 합니다**.</li><li>하나 이상의 부정 이벤트가 있는 쿼리가 지원됩니다. 그러나 전체 이벤트 **는 부정일 수 없습니다.**</li></ul> |

## 스트리밍 세그멘테이션에 대해 활성화된 모든 세그먼트 검색

`/segment/definitions` 종단점에 GET 요청을 함으로써 IMS 내에서 세그먼테이션을 스트리밍하도록 활성화된 모든 세그먼트 목록을 검색할 수 있습니다.

**API 형식**

스트리밍이 활성화된 세그먼트를 검색하려면 요청 경로에 쿼리 매개 변수 `evaluationInfo.continuous.enabled=true`을(를) 포함해야 합니다.

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

성공적인 응답은 스트리밍 세그멘테이션에 사용할 수 있는 IMS 조직의 세그먼트 배열을 반환합니다.

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

세그먼트가](#streaming-segmentation-query-types) 위에 나열된 [스트리밍 세그먼트 유형 중 하나와 일치하면 자동으로 스트리밍이 활성화됩니다.

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
>표준 &quot;세그먼트 만들기&quot; 요청입니다. 세그먼트 정의 만들기에 대한 자세한 내용은 [세그먼트 만들기](../tutorials/create-a-segment.md)의 자습서를 참조하십시오.

**응답**

성공적으로 응답하면 새로 만든 스트리밍 가능 세그먼트 정의의 세부 사항이 반환됩니다.

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

스트리밍 평가가 활성화되면 베이스라인을 만들어야 합니다(그 이후는 항상 최신 상태로 유지됨). 시스템에서 자동으로 기본 설정을 수행하려면 먼저 예약된 평가(예약된 세그먼테이션이라고도 함)를 활성화해야 합니다. IMS 조직에서는 예약된 세그먼테이션을 사용하여 반복되는 일정을 따르면서 세그먼트를 평가하는 내보내기 작업을 자동으로 실행할 수 있습니다.

>[!NOTE]
>
>[!DNL XDM Individual Profile]에 대해 최대 5개의 병합 정책이 있는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다. 조직에서 단일 샌드박스 환경 내에서 [!DNL XDM Individual Profile]에 대한 병합 정책이 5개 이상 있는 경우 예약된 평가를 사용할 수 없습니다.

### 일정 만들기

`/config/schedules` 끝점에 POST 요청을 함으로써 일정을 만들고 일정을 트리거해야 하는 특정 시간을 포함할 수 있습니다.

**API 형식**

```http
POST /config/schedules
```

**요청**

다음 요청은 페이로드에 제공된 사양을 기반으로 새 일정을 만듭니다.

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
| `properties` | **(필수)** 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `properties.segments` | **( `type` 등호 시  `batch_segmentation`필수)** 를 사용하면  `["*"]` 모든 세그먼트가 포함됩니다. |
| `schedule` | **(필수)** 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있으므로 24시간 동안 두 번 이상 실행되도록 작업을 예약할 수 없습니다. 표시된 예제(`0 0 1 * * ?`)는 작업이 1:00:00 UTC에 매일 트리거됨을 의미합니다. 자세한 내용은 [cron 표현식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. |
| `state` | *(선택 사항)* 예약 상태를 포함하는 문자열입니다. 사용 가능한 값:`active` 및 `inactive`. 기본값은 `inactive`입니다. IMS 조직은 하나의 스케줄만 생성할 수 있습니다. 일정을 업데이트하는 단계는 이 자습서의 후반부에서 확인할 수 있습니다. |

**응답**

성공적인 응답은 새로 만든 일정의 세부 정보를 반환합니다.

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

### 예약 활성화

만들기(POST) 요청 본문에 `state` 속성이 `active`으로 설정되어 있지 않으면 기본적으로 일정이 만들어지면 비활성화됩니다. `/config/schedules` 종단점에 PATCH 요청을 하고 경로에 있는 예약의 ID를 포함하여 일정(`state` 을 `active` 로 설정)을 활성화할 수 있습니다.

**API 형식**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**요청**

다음 요청에서는 [JSON 패치 서식](http://jsonpatch.com/)을 사용하여 일정의 `state`를 `active`으로 업데이트합니다.

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

이전 요청의 &quot;value&quot;를 &quot;inactive&quot;로 대체하여 일정을 비활성화하는 데 동일한 작업을 사용할 수 있습니다.

## 다음 단계

스트리밍 세그먼테이션을 위해 새 세그먼트와 기존 세그먼트를 모두 활성화했고 기준선을 개발하고 반복 평가를 수행하는 예약된 세그먼테이션을 활성화했으므로 이제 조직에 대해 스트리밍이 가능한 세그먼트를 만들기 시작할 수 있습니다.

유사한 작업을 수행하고 Adobe Experience Platform 사용자 인터페이스를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 [세그먼트 빌더 사용자 안내서](../ui/segment-builder.md)를 방문하십시오.
