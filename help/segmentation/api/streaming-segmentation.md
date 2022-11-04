---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;스트리밍 세그먼테이션;스트리밍 세그먼테이션;연속 평가;
solution: Experience Platform
title: 스트리밍 세그먼테이션을 사용하여 거의 실시간으로 이벤트 평가
topic-legacy: developer guide
description: 이 문서에는 Adobe Experience Platform 세그멘테이션 서비스 API에서 스트리밍 세그멘테이션을 사용하는 방법에 대한 예가 나와 있습니다.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 30a12fee487609b4c85ba342963bb915e8152195
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 1%

---

# 스트리밍 세그먼테이션을 통해 거의 실시간으로 이벤트 평가

>[!NOTE]
>
>다음 문서에서는 API를 사용하여 스트리밍 세그멘테이션을 사용하는 방법을 설명합니다. UI를 사용하여 스트리밍 세그멘테이션을 사용하는 방법에 대한 자세한 내용은 [스트리밍 세그멘테이션 UI 안내서](../ui/streaming-segmentation.md).

스트리밍 세그먼테이션 [!DNL Adobe Experience Platform] 을 사용하면 데이터 풍요에 주력하면서 거의 실시간으로 세분화를 수행할 수 있습니다. 스트리밍 세그먼테이션을 사용하면 이제 스트리밍 데이터가 . [!DNL Platform], 세그먼테이션 작업을 예약하고 실행할 필요성을 완화합니다. 이 기능을 사용하면 이제 데이터가 . [!DNL Platform]: 세그먼트 멤버십이 예약된 세그먼테이션 작업을 실행하지 않고 최신 상태로 유지됩니다.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>스트리밍 세그먼테이션은 스트리밍 소스를 사용하여 수집된 모든 데이터에서 작동합니다. 일괄 처리 기반 소스를 사용하여 수집된 세그먼트는 스트리밍 세그멘테이션의 자격이 있는 경우에도 매일 평가됩니다.
>
>또한 스트리밍 세그먼테이션으로 평가된 세그먼트는 세그먼트가 배치 세그먼테이션을 사용하여 평가되는 다른 세그먼트를 기반으로 하는 경우 이상과 실제 멤버십 간에 이동될 수 있습니다. 예를 들어 세그먼트 A가 세그먼트 B를 기반으로 하고 세그먼트 B가 배치 세그먼테이션을 사용하여 평가되는 경우 세그먼트 B는 24시간마다 업데이트되므로 세그먼트 B 업데이트와 다시 동기화될 때까지 실제 데이터에서 더 멀리 이동합니다.

## 시작하기

이 개발자 안내서를 사용하려면 다양한 [!DNL Adobe Experience Platform] 스트리밍 세그먼테이션과 관련된 서비스. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 실시간으로 통합 소비자 프로필을 제공합니다.
- [[!DNL Segmentation]](../home.md): 에서 세그먼트와 대상을 만들 수 있는 기능을 제공합니다. [!DNL Real-time Customer Profile] 데이터.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

다음 섹션에서는 를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다 [!DNL Platform] API.

### 샘플 API 호출 읽기

이 개발자 가이드는 요청의 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- 권한 부여: 베어러 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형: application/json

특정 요청을 완료하려면 추가 헤더가 필요할 수 있습니다. 이 문서 내의 각 예제에 올바른 헤더가 표시됩니다. 모든 필수 헤더가 포함되도록 샘플 요청에 특별히 주의하십시오.

### 스트리밍 세그먼테이션이 활성화된 쿼리 유형 {#query-types}

>[!NOTE]
>
>스트리밍 세그먼테이션이 작동하려면 조직에 대해 예약된 세그먼테이션을 활성화해야 합니다. 예약된 세그먼테이션을 활성화하는 방법은 [예약된 세그멘테이션 섹션 활성화](#enable-scheduled-segmentation)

스트리밍 세그먼테이션을 사용하여 세그먼트를 평가하려면 다음 지침을 따라야 합니다.

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 단일 이벤트 | 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. |
| 상대 시간 창 내의 단일 이벤트 | 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. |
| 시간 창이 있는 단일 이벤트 | 시간 창이 있는 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. |
| 프로필만 | 프로필 속성만 참조하는 모든 세그먼트 정의. |
| 프로필 속성이 있는 단일 이벤트 | 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의와 하나 이상의 프로필 속성을 참조합니다. **참고:** 이벤트가 발생하면 쿼리가 즉시 평가됩니다. 그러나 프로필 이벤트의 경우 통합하려면 24시간을 기다려야 합니다. |
| 상대 시간 창 내에 프로필 속성이 있는 단일 이벤트 | 단일 수신 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의입니다. |
| 세그먼트 | 하나 이상의 일괄 처리 또는 스트리밍 세그먼트를 포함하는 모든 세그먼트 정의. **참고:** 세그먼트 세그먼트가 사용되는 경우 프로필 결격률이 발생합니다 **24시간마다**. |
| 프로필 속성이 있는 여러 이벤트 | 여러 이벤트를 참조하는 모든 세그먼트 정의 **지난 24시간 내에** 및 (선택적)에는 하나 이상의 프로필 속성이 있습니다. |

세그먼트 정의는 **not** 다음 시나리오에서 스트리밍 세그멘테이션에 대해 활성화되어 있습니다.

- 세그먼트 정의에는 Adobe Audience Manager(AAM) 세그먼트 또는 트레이트가 포함됩니다.
- 세그먼트 정의에는 여러 엔티티(다중 엔티티 쿼리)가 포함되어 있습니다.

스트리밍 세그멘테이션을 수행할 때 다음 지침이 적용됩니다.

| 쿼리 유형 | 지침 |
| ---------- | -------- |
| 단일 이벤트 쿼리 | 전환 확인 기간에는 제한이 없습니다. |
| 이벤트 내역이 있는 쿼리 | <ul><li>전환 확인 기간은 로 제한됩니다 **하루**.</li><li>엄격한 시간 순서 조건 **반드시** 이벤트 사이에 존재해야 합니다.</li><li>하나 이상의 부정 이벤트가 있는 쿼리가 지원됩니다. 하지만 전체 이벤트는 **사용할 수 없음** 부정이다.</li></ul> |

세그먼트 정의가 수정되어 더 이상 스트리밍 세그먼테이션의 기준을 충족하지 않는 경우 세그먼트 정의는 자동으로 &quot;스트리밍&quot;에서 &quot;일괄 처리&quot;로 전환됩니다.

또한 세그먼트 자격 증명과 유사한 세그먼트 자격 해제가 실시간으로 발생합니다. 따라서 대상이 더 이상 세그먼트 자격이 없는 경우 즉시 자격이 없습니다. 예를 들어 세그먼트 정의에 &quot;최근 3시간 내에 빨간색 신발을 구매한 모든 사용자&quot;를 묻는 경우 3시간 후 세그먼트 정의에 처음에 자격을 부여한 모든 프로필은 자격을 갖추지 못합니다.

## 스트리밍 세그먼테이션을 위해 활성화된 모든 세그먼트 검색

IMS 조직 내에서 세그먼테이션 스트리밍을 위해 활성화된 모든 세그먼트 목록을 IMS에 GET 요청을 수행하여 검색할 수 있습니다 `/segment/definitions` 엔드포인트.

**API 형식**

스트리밍이 활성화된 세그먼트를 검색하려면 쿼리 매개 변수를 포함해야 합니다 `evaluationInfo.continuous.enabled=true` 를 입력합니다.

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

성공적인 응답은 스트리밍 세그멘테이션을 위해 활성화된 IMS 조직의 세그먼트 배열을 반환합니다.

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

## 스트리밍 사용 세그먼트 만들기

세그먼트가 다음 중 하나와 일치하는 경우 자동으로 스트리밍이 활성화됩니다 [위에 나열된 스트리밍 세분화 유형](#query-types).

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
    }
}'
```

>[!NOTE]
>
>표준 &quot;세그먼트 만들기&quot; 요청입니다. 세그먼트 정의 만들기에 대한 자세한 내용은 [세그먼트 만들기](../tutorials/create-a-segment.md).

**응답**

성공적인 응답은 새로 만든 스트리밍 사용 세그먼트 정의의 세부 사항을 반환합니다.

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

스트리밍 평가가 활성화되면 베이스라인을 만들어야 합니다(그 이후에는 세그먼트가 항상 최신 상태로 유지됨). 시스템에서 자동으로 기본 설정을 수행하려면 먼저 예약된 평가(예약된 세그먼테이션이라고도 함)를 활성화해야 합니다. 예약된 세그멘테이션을 사용하면 IMS 조직은 반복 일정을 준수하여 세그먼트를 평가하기 위해 내보내기 작업을 자동으로 실행할 수 있습니다.

>[!NOTE]
>
>샌드박스에 대해 예약된 평가를 사용하도록 설정할 수 있으며 최대 5개의 병합 정책이 있습니다 [!DNL XDM Individual Profile]. 조직에 5개 이상의 병합 정책이 있는 경우 [!DNL XDM Individual Profile] 단일 샌드박스 환경 내에서 예약된 평가를 사용할 수 없습니다.

### 예약 만들기

에 POST 요청을 함으로써 `/config/schedules` 종단점을 위해 일정을 만들고 일정을 트리거해야 하는 특정 시간을 포함할 수 있습니다.

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
| `properties` | **(필수)** 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `properties.segments` | **(필요한 경우) `type` 다음과 같음 `batch_segmentation`)** 사용 `["*"]` 모든 세그먼트가 포함되도록 합니다. |
| `schedule` | **(필수)** 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 기간 동안 두 번 이상 실행하도록 작업을 예약할 수 없습니다. 이 예는 와(과) 같습니다.`0 0 1 * * ?`)은 작업이 매일 1에 트리거됨을 의미합니다:00:00 UTC입니다. 자세한 내용은 [cron 식 형식](./schedules.md#appendix) 를 클릭하여 제품에서 사용할 수 있습니다. |
| `state` | *(선택 사항)* 예약 상태가 포함된 문자열입니다. 사용 가능한 값: `active` 및 `inactive`. 기본값은 `inactive`입니다. IMS 조직은 하나의 일정만 만들 수 있습니다. 일정을 업데이트하는 단계는 이 자습서의 뒷부분에 있습니다. |

**응답**

성공적으로 응답하면 새로 만든 예약의 세부 정보가 반환됩니다.

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

### 예약 활성화

기본적으로 예약은 `state` 속성이 `active` 만들기(POST) 요청 본문에서 일정을 활성화( `state` to `active`)에 PATCH 요청을 함으로써 `/config/schedules` 엔드포인트 및 경로에 예약의 ID를 포함합니다.

**API 형식**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**요청**

다음 요청에서는 을 사용합니다 [JSON 패치 형식](https://datatracker.ietf.org/doc/html/rfc6902) 업데이트하기 위해 `state` 일정 기준 `active`.

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

성공적으로 업데이트되면 빈 응답 본문과 HTTP 상태 204(콘텐츠 없음)가 반환됩니다.

동일한 작업을 사용하여 이전 요청의 &quot;값&quot;을 &quot;비활성&quot;으로 대체하여 일정을 비활성화할 수 있습니다.

## 다음 단계

이제 스트리밍 세그먼테이션을 위해 새 세그먼트와 기존 세그먼트를 모두 활성화하고 기준선을 개발하고 반복 평가를 수행하도록 예약된 세그먼테이션을 활성화했으므로 조직에 대해 스트리밍 지원 세그먼트를 만들 수 있습니다.

Adobe Experience Platform 사용자 인터페이스를 사용하여 유사한 작업을 수행하고 세그먼트를 작업하는 방법을 배우려면 [세그먼트 빌더 사용 안내서](../ui/segment-builder.md).

## 부록

다음 섹션에는 스트리밍 세그먼테이션과 관련된 FAQ가 나열되어 있습니다.

### 스트리밍 세그먼테이션 &quot;자격 없음&quot;도 실시간으로 발생합니까?

대부분의 경우 스트리밍 세그멘테이션 무자격 은 실시간으로 발생합니다. 하지만 세그먼트의 세그먼트를 사용하는 스트리밍 세그먼트는 **not** 24시간 후에 자격 증명을 받지 못하는 대신 실시간으로 자격 조건을 충족하지 못합니다.

### 스트리밍 세그먼테이션은 어떤 데이터에서 작동합니까?

스트리밍 세그먼테이션은 스트리밍 소스를 사용하여 수집된 모든 데이터에서 작동합니다. 일괄 처리 기반 소스를 사용하여 수집된 세그먼트는 스트리밍 세그멘테이션의 자격이 있는 경우에도 매일 평가됩니다. 24시간 이전의 타임스탬프와 함께 시스템으로 스트리밍되는 이벤트는 후속 배치 작업에서 처리됩니다.

### 세그먼트는 어떻게 일괄 처리 또는 스트리밍 세그먼테이션으로 정의됩니까?

세그먼트는 쿼리 유형 및 이벤트 내역 기간의 조합을 기반으로 일괄 처리 또는 스트리밍 세그먼테이션으로 정의됩니다. 스트리밍 세그먼트로 평가될 세그먼트 목록은 [세그먼테이션 쿼리 유형 섹션](#query-types).

세그먼트에 **둘 다** an `inSegment` 표현식 및 직접적인 단일 이벤트 체인은 스트리밍 세그먼테이션의 자격이 없습니다. 이 세그먼트가 스트리밍 세그먼테이션에 대한 자격이 되게 하려면 직접 단일 이벤트 체인을 자체 세그먼트로 만들어야 합니다.

### 최근 X일 아래의 수가 세그먼트 세부 사항 섹션 내에 0으로 남아 있는 동안 &quot;총 적격한&quot; 세그먼트 수는 왜 계속 증가합니까?

일별 세그먼테이션 작업에서 정규화된 총 세그먼트 수가 도출되며 여기에는 일괄 처리 및 스트리밍 세그먼트 모두에 대한 자격이 있는 대상이 포함됩니다. 이 값은 일괄 처리 및 스트리밍 세그먼트 모두에 대해 표시됩니다.

마지막 X일 아래의 숫자 **전용** 스트리밍 세그멘테이션의 자격이 있는 대상을 포함하며, **전용** 시스템에 데이터를 스트리밍한 경우 해당 스트리밍 정의로 카운트되면 증가합니다. 이 값은 **전용** 스트리밍 세그먼트에 대해 표시됩니다. 따라서 이 값은 **5월** 배치 세그먼트에 대해 0으로 표시합니다.

따라서 &quot;최근 X일&quot; 아래의 숫자가 0이고 선 그래프도 0을 보고하는 경우, **not** 해당 세그먼트에 대한 자격이 되는 시스템에 모든 프로필을 스트리밍했습니다.

### 세그먼트를 사용할 수 있는 데 시간이 얼마나 걸립니까?

세그먼트를 사용할 수 있으려면 최대 1시간이 걸립니다.