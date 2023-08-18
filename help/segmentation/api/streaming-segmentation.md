---
solution: Experience Platform
title: 스트리밍 세분화를 통해 실시간에 가까운 이벤트 평가
description: 이 문서에는 Adobe Experience Platform 세그먼테이션 서비스 API와 함께 스트리밍 세그먼테이션을 사용하는 방법에 대한 예제가 포함되어 있습니다.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 23504dd0909488e2ee63bf356fba4c7f0f7320dc
workflow-type: tm+mt
source-wordcount: '1956'
ht-degree: 1%

---

# 스트리밍 세분화를 통해 거의 실시간으로 이벤트 평가

>[!NOTE]
>
>다음 문서에서는 API를 사용하여 스트리밍 세분화를 사용하는 방법을 설명합니다. UI를 사용하여 스트리밍 세분화를 사용하는 방법에 대한 자세한 내용은 [스트리밍 세분화 UI 안내서](../ui/streaming-segmentation.md).

스트리밍 세분화 [!DNL Adobe Experience Platform] 을 사용하면 고객이 데이터 풍부함에 초점을 맞추면서 거의 실시간으로 세분화를 수행할 수 있습니다. 스트리밍 세분화를 통해 이제 스트리밍 데이터가에 도달하면 세그먼트 자격이 발생합니다 [!DNL Platform]을 사용하면 세분화 작업을 예약하고 실행할 필요가 줄어듭니다. 이 기능을 사용하면 이제 데이터가 전달될 때 대부분의 세그먼트 규칙을 평가할 수 있습니다 [!DNL Platform]: 세그먼트 멤버십이 예약된 세그먼테이션 작업을 실행하지 않고 최신 상태로 유지됨을 의미합니다.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>스트리밍 세분화는 스트리밍 소스를 사용하여 수집된 모든 데이터에 대해 작동합니다. 일괄 처리 기반 소스를 사용하여 수집된 세그먼트는 스트리밍 세그멘테이션 자격이 있는 경우에도 매일 밤 평가됩니다.
>
>또한, 스트리밍 세분화로 평가된 세그먼트 정의는 세그먼트 정의가 배치 세분화를 사용하여 평가된 다른 세그먼트 정의에 따라 달라지는 경우 이상적인 멤버십과 실제 멤버십 사이에서 표류할 수 있습니다. 예를 들어 세그먼트 A가 세그먼트 B를 기반으로 하고 세그먼트 B가 배치 세그먼테이션을 사용하여 평가되는 경우 세그먼트 B는 24시간마다 업데이트되므로 세그먼트 A는 세그먼트 B 업데이트와 다시 동기화될 때까지 실제 데이터에서 더 멀리 이동합니다.

## 시작하기

이 개발자 안내서를 사용하려면 여러 가지 사항에 대한 작업 이해가 필요합니다 [!DNL Adobe Experience Platform] 스트리밍 세분화와 관련된 서비스. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 소비자 프로필을 실시간으로 제공합니다.
- [[!DNL Segmentation]](../home.md): 의 세그먼트 정의 및 기타 외부 소스를 사용하여 대상자를 만드는 기능을 제공합니다. [!DNL Real-Time Customer Profile] 데이터.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

다음 섹션에서는 을 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Platform] API.

### 샘플 API 호출 읽기

이 개발자 안내서에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

- 인증: 전달자 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

특정 요청을 완료하려면 추가 헤더가 필요할 수 있습니다. 이 문서 내의 각 예제에 올바른 헤더가 표시됩니다. 모든 필수 헤더가 포함되도록 하려면 샘플 요청에 특별히 주의하십시오.

### 스트리밍 세분화 사용 쿼리 유형 {#query-types}

>[!NOTE]
>
>스트리밍 세분화를 사용하려면 조직에 대해 예약된 세분화를 활성화해야 합니다. 예약된 세분화 활성화에 대한 정보는 [예약된 세분화 섹션 활성화](#enable-scheduled-segmentation)

스트리밍 세분화를 사용하여 세그먼트 정의를 평가하려면 쿼리가 다음 지침을 준수해야 합니다.

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 단일 이벤트 | 시간 제한 없이 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의. |
| 상대 기간 내의 단일 이벤트 | 단일 수신 이벤트를 참조하는 모든 세그먼트 정의. |
| 시간 창이 있는 단일 이벤트 | 시간 창이 있는 단일 수신 이벤트를 참조하는 모든 세그먼트 정의. |
| 프로필만 | 프로필 속성만 참조하는 모든 세그먼트 정의. |
| 24시간 미만의 상대 시간 창 내에 프로필 속성이 있는 단일 이벤트 | 하나 이상의 프로필 속성을 가진 단일 수신 이벤트를 참조하고 24시간 미만의 상대 시간 창 내에서 발생하는 모든 세그먼트 정의입니다. |
| 세그먼트 | 하나 이상의 일괄 처리 또는 스트리밍 세그먼트를 포함하는 모든 세그먼트 정의입니다. **참고:** 세그먼트 세그먼트를 사용하는 경우 프로필 결격이 발생합니다 **24시간마다**. |
| 프로필 속성이 있는 여러 이벤트 | 여러 이벤트를 참조하는 모든 세그먼트 정의 **지난 24시간 이내** 및 (선택 사항)에는 하나 이상의 프로필 속성이 있습니다. |

세그먼트 정의는 **아님** 다음과 같은 시나리오에서 스트리밍 세분화를 사용할 수 있습니다.

- 세그먼트 정의에는 Adobe Audience Manager(AAM) 세그먼트 또는 트레이트가 포함됩니다.
- 세그먼트 정의에는 여러 엔티티(다중 엔티티 쿼리)가 포함됩니다.
- 세그먼트 정의는 단일 이벤트와 `inSegment` 이벤트.
   - 그러나 세그먼트에 포함된 경우 `inSegment` 이벤트는 프로필 전용이며, 세그먼트 정의는 입니다. **의지** 스트리밍 세분화를 활성화하십시오.

스트리밍 세분화를 수행할 때 다음 지침이 적용됩니다.

| 쿼리 유형 | 지침 |
| ---------- | -------- |
| 단일 이벤트 쿼리 | 전환 확인 기간에는 제한이 없습니다. |
| 이벤트 기록이 있는 쿼리 | <ul><li>전환 확인 기간은 다음으로 제한됩니다. **1일**.</li><li>엄격한 시간 순서 조건 **필수** 이벤트 사이에 존재합니다.</li><li>적어도 한 개의 무효화된 이벤트가 있는 쿼리가 지원됩니다. 그러나 전체 이벤트는 **할 수 없음** 부정적이 되라.</li></ul> |

스트리밍 세분화 기준을 더 이상 충족하지 않도록 세그먼트 정의를 수정하면 세그먼트 정의가 자동으로 &quot;스트리밍&quot;에서 &quot;일괄 처리&quot;로 전환됩니다.

또한 세그먼트 자격과 마찬가지로 세그먼트 비자격은 실시간으로 발생합니다. 따라서 프로필이 더 이상 세그먼트 정의에 적합하지 않으면 즉시 부적격 프로필이 됩니다. 예를 들어 세그먼트 정의가 &quot;지난 3시간 동안 빨간 신발을 구매한 모든 사용자&quot;를 묻는 경우 3시간 후에 세그먼트 정의에 대해 처음에 자격을 부여한 모든 프로필은 부적격합니다.

## 스트리밍 세분화에 대해 활성화된 모든 세그먼트 정의 검색

에 GET 요청을 하여 조직 내에서 스트리밍 세분화에 대해 활성화된 모든 세그먼트 정의 목록을 검색할 수 있습니다. `/segment/definitions` 엔드포인트.

**API 형식**

스트리밍 지원 세그먼트 정의를 검색하려면 쿼리 매개 변수를 포함해야 합니다 `evaluationInfo.continuous.enabled=true` 요청 경로에서.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 스트리밍 세분화에 대해 활성화된 조직의 세그먼트 정의 배열을 반환합니다.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

## 스트리밍 사용 세그먼트 정의 만들기

세그먼트 정의가 다음 중 하나와 일치하는 경우 자동으로 스트리밍이 활성화됩니다. [위에 나열된 스트리밍 세분화 유형](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

>[!NOTE]
>
>표준 &quot;세그먼트 정의 만들기&quot; 요청입니다. 세그먼트 정의 만들기에 대한 자세한 내용은 다음 자습서를 참조하십시오. [세그먼트 정의 만들기](../tutorials/create-a-segment.md).

**응답**

성공한 응답은 새로 만든 스트리밍 활성화 세그먼트 정의의 세부 정보를 반환합니다.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
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

## 예약된 평가 활성화 {#enable-scheduled-segmentation}

스트리밍 평가가 활성화되면 기준선을 만들어야 합니다. 그 후 세그먼트 정의는 항상 최신 상태가 됩니다. 시스템에서 베이스라인을 자동으로 수행하려면 먼저 예약된 평가(예약된 세그먼테이션이라고도 함)를 활성화해야 합니다. 예약된 세그먼테이션을 사용하면 조직에서 반복 일정을 준수하여 세그먼트 정의를 평가하기 위해 내보내기 작업을 자동으로 실행할 수 있습니다.

>[!NOTE]
>
>최대 5개의 병합 정책이 있는 샌드박스에 대해 예약된 평가를 활성화할 수 있습니다. [!DNL XDM Individual Profile]. 조직에 5개 이상의 병합 정책이 있는 경우 [!DNL XDM Individual Profile] 단일 샌드박스 환경 내에서는 예약된 평가를 사용할 수 없습니다.

### 일정 만들기

에 POST 요청 수행 `/config/schedules` 엔드포인트에서는 일정을 만들고 일정이 트리거되어야 하는 특정 시간을 포함할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | **(필수)** 문자열 형식의 작업 유형입니다. 지원되는 유형은 다음과 같습니다 `batch_segmentation` 및 `export`. |
| `properties` | **(필수)** 일정과 관련된 추가 등록 정보가 포함된 객체입니다. |
| `properties.segments` | **(필요한 경우) `type` 다음과 같음 `batch_segmentation`)** 사용 `["*"]` 는 모든 세그먼트 정의를 포함합니다. |
| `schedule` | **(필수)** 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 작업을 두 번 이상 실행하도록 예약할 수 없습니다. 표시된 예 (`0 0 1 * * ?`)은 작업이 매일 1시에 트리거됨을 의미합니다:00:00 UTC. 자세한 내용은 다음 문서의 부록을 참조하십시오. [cron 표현식 형식](./schedules.md#appendix) 세분화 내 일정에 대한 설명서 내에서. |
| `state` | *(선택 사항)* 일정 상태를 포함하는 문자열입니다. 사용 가능한 값: `active` 및 `inactive`. 기본값은 `inactive`입니다. 조직은 하나의 스케줄만 생성할 수 있습니다. 일정을 업데이트하는 단계는 이 자습서의 뒷부분에서 확인할 수 있습니다. |

**응답**

성공한 응답은 새로 생성된 일정의 세부 정보를 반환합니다.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{ORG_ID}",
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

기본적으로 스케줄은 다음 경우를 제외하고 생성 시 비활성화됩니다. `state` 속성이 로 설정되어 있습니다. `active` (POST) 만들기 요청 본문에서 확인할 수 있습니다. 예약을 활성화할 수 있습니다(다음을 설정하십시오.) `state` 끝 `active`)에 PATCH 요청을 하여 `/config/schedules` 엔드포인트 및 경로에 일정 ID 포함.

**API 형식**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**요청**

다음 요청은 을 사용합니다 [JSON 패치 형식 지정](https://datatracker.ietf.org/doc/html/rfc6902) 를 업데이트하려면 `state` 일정: 까지 `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

성공한 업데이트는 빈 응답 본문과 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

동일한 작업을 사용하여 이전 요청의 &quot;value&quot;를 &quot;inactive&quot;로 대체하여 일정을 비활성화할 수 있습니다.

## 다음 단계

스트리밍 세분화에 대한 새 세그먼트 정의와 기존 세그먼트 정의를 모두 활성화하고, 기준선 개발과 반복 평가를 수행하기 위해 예약된 세분화를 활성화했으므로 이제 조직에 대해 스트리밍 지원 세그먼트 정의를 만들 수 있습니다.

Adobe Experience Platform 사용자 인터페이스를 사용하여 유사한 작업을 수행하고 세그먼트 정의를 사용하는 방법을 알아보려면 다음을 방문하십시오. [세그먼트 빌더 사용 안내서](../ui/segment-builder.md).

## 부록

다음 섹션에서는 스트리밍 세분화에 대해 자주 묻는 질문에 대해 설명합니다.

### 스트리밍 세분화 &quot;비자격&quot;도 실시간으로 발생합니까?

대부분의 경우 스트리밍 세분화 비자격이 실시간으로 발생합니다. 그러나 세그먼트의 세그먼트를 사용하는 스트리밍 세그먼트 정의는 다음과 같습니다 **아님** 실시간으로 부적격 처리, 대신 24시간 후 부적격 처리.

### 스트리밍 세분화는 어떤 데이터에 작동합니까?

스트리밍 세분화는 스트리밍 소스를 사용하여 수집된 모든 데이터에 대해 작동합니다. 일괄 처리 기반 소스를 사용하여 수집된 세그먼트는 스트리밍 세그멘테이션 자격이 있는 경우에도 매일 밤 평가됩니다. 타임스탬프가 24시간 이상인 시스템으로 스트리밍되는 이벤트는 후속 일괄 처리 작업에서 처리됩니다.

### 세그먼트 정의는 배치 또는 스트리밍 세그먼테이션으로 어떻게 정의됩니까?

세그먼트 정의는 쿼리 유형과 이벤트 내역 기간의 조합을 기반으로 하는 일괄 처리 또는 스트리밍 세그먼테이션으로 정의됩니다. 스트리밍 세그먼트로 평가될 세그먼트 정의의 목록은 [스트리밍 세분화 쿼리 유형 섹션](#query-types).

세그먼트에 포함된 경우 참고 사항 **모두** an `inSegment` 표현식 및 직접적인 단일 이벤트 체인이므로 스트리밍 세분화에 적합하지 않습니다. 이 세그먼트 정의가 스트리밍 세분화에 적합하도록 하려면 직접 단일 이벤트 체인을 고유한 세그먼트 정의로 만들어야 합니다.

### 세그먼트 정의 세부 사항 섹션 내에서 &quot;최근 X일&quot;에 있는 숫자가 0으로 유지되는 동안 &quot;총 적격&quot; 세그먼트 정의의 수가 계속 증가하는 이유는 무엇입니까?

총 적격 세그먼트 정의 수는 일괄 처리와 스트리밍 세그먼트 정의를 모두 사용할 수 있는 대상을 포함하는 일별 세그먼테이션 작업에서 가져옵니다. 이 값은 배치 및 스트리밍 세그먼트 정의에 모두 표시됩니다.

&quot;최근 X일&quot; 아래의 숫자 **전용** 스트리밍 세분화에서 자격을 갖춘 대상자를 포함합니다. **전용** 데이터를 시스템으로 스트리밍하고 해당 스트리밍 정의로 카운트하면 증가합니다. 이 값은 **전용** 스트리밍 세그먼트 정의에 대해 표시됩니다. 따라서 이 값은 **5월** 배치 세그먼트 정의에 대해 0으로 표시합니다.

따라서 &quot;최근 X일&quot; 아래의 숫자가 0이고 선 그래프가 0을 보고하는 것을 보면 다음을 가질 수 있습니다. **아님** 해당 세그먼트 정의에 적합한 프로필을 시스템으로 스트리밍했습니다.

### 세그먼트 정의를 사용하려면 얼마나 걸립니까?

세그먼트 정의를 사용할 수 있는 데 최대 1시간이 소요됩니다.
