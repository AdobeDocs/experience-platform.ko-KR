---
solution: Experience Platform
title: 예약 API 끝점
description: 예약은 하루에 한 번 배치 세분화 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다.
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: bf90e478b38463ec8219276efe71fcc1aab6b2aa
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# 일정 끝점

예약은 하루에 한 번 배치 세분화 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. `/config/schedules` 끝점을 사용하여 일정 목록을 검색하거나 새 일정을 만들거나 특정 일정의 세부 정보를 검색하거나 특정 일정을 업데이트하거나 특정 일정을 삭제할 수 있습니다.

## 시작하기

이 가이드에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 일정 목록 검색 {#retrieve-list}

`/config/schedules` 끝점에 대한 GET 요청을 통해 조직의 모든 일정 목록을 검색할 수 있습니다.

**API 형식**

`/config/schedules` 끝점은 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 값비싼 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 일정을 검색합니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다.

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**쿼리 매개 변수**

+++ 사용 가능한 쿼리 매개 변수 목록입니다.

| 매개변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `start` | 오프셋을 시작할 페이지를 지정합니다. 기본적으로 이 값은 0이 됩니다. | `start=5` |
| `limit` | 반환되는 일정 수를 지정합니다. 기본적으로 이 값은 100이 됩니다. | `limit=20` |

+++

**요청**

다음 요청은 조직 내에 게시된 마지막 10개의 일정을 검색합니다.

+++ 일정 목록을 검색하는 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 지정된 조직에 대한 일정 목록이 JSON인 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>다음 응답은 공간에 대해 잘렸으며, 반환된 첫 번째 예약만 표시합니다.

+++ 일정 목록을 검색할 때의 샘플 응답입니다.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 속성 | 설명 |
| -------- | ------------ |
| `_page.totalCount` | 반환된 총 일정 수입니다. |
| `_page.pageSize` | 일정 페이지의 크기입니다. |
| `children.name` | 문자열로 표시되는 예약의 이름입니다. |
| `children.type` | 문자열로서의 작업 유형입니다. 지원되는 두 가지 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `children.properties` | 일정과 관련된 추가 등록 정보가 포함된 객체입니다. |
| `children.properties.segments` | `["*"]`을(를) 사용하면 모든 세그먼트가 포함됩니다. |
| `children.schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 작업을 두 번 이상 실행하도록 예약할 수 없습니다. cron 일정에 대한 자세한 내용은 [cron 식 형식](#appendix)의 부록을 참조하십시오. 이 예에서 &quot;0 0 1 * *&quot;는 이 일정이 매일 오전 1시에 실행됨을 의미합니다. |
| `children.state` | 일정 상태를 포함하는 문자열입니다. 지원되는 두 가지 상태는 &quot;활성&quot; 및 &quot;비활성&quot;입니다. 기본적으로 상태는 &quot;비활성&quot;으로 설정됩니다. |

+++

## 새 일정 만들기 {#create}

`/config/schedules` 끝점에 대한 POST 요청을 수행하여 새 일정을 만들 수 있습니다.

**API 형식**

```http
POST /config/schedules
```

**요청**

+++ 일정 만들기에 대한 샘플 요청입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| 속성 | 설명 |
| -------- | ------------ |
| `name` | **필수.** 일정 이름(문자열)입니다. |
| `type` | **필수.** 작업 유형(문자열)입니다. 지원되는 두 가지 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `properties` | **필수.** 일정과 관련된 추가 속성을 포함하는 개체입니다. |
| `properties.segments` | **`type`이(가) &quot;batch_segmentation&quot;인 경우 필요합니다.** `["*"]`을(를) 사용하면 모든 세그먼트가 포함됩니다. |
| `schedule` | *선택 사항입니다.* 작업 일정이 포함된 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 작업을 두 번 이상 실행하도록 예약할 수 없습니다. cron 일정에 대한 자세한 내용은 [cron 식 형식](#appendix)의 부록을 참조하십시오. 이 예에서 &quot;0 0 1 * *&quot;는 이 일정이 매일 오전 1시에 실행됨을 의미합니다. <br><br>이 문자열을 제공하지 않으면 시스템에서 생성한 일정이 자동으로 생성됩니다. |
| `state` | *선택 사항입니다.* 일정 상태를 포함하는 문자열입니다. 지원되는 두 가지 상태는 &quot;활성&quot; 및 &quot;비활성&quot;입니다. 기본적으로 상태는 &quot;비활성&quot;으로 설정됩니다. |

+++

**응답**

성공한 응답은 새로 만든 일정의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 일정을 만들 때 샘플 응답.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
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

+++

## 특정 일정 검색 {#get}

`/config/schedules` 끝점에 대한 GET 요청을 만들고 요청 경로에서 검색하려는 일정의 ID를 제공하여 특정 일정에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 일정의 `id` 값입니다. |

**요청**

+++ 일정을 검색하기 위한 샘플 요청입니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공한 응답은 지정된 일정에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

+++ 일정을 검색할 때의 샘플 응답입니다.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
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

| 속성 | 설명 |
| -------- | ------------ |
| `name` | 문자열로 표시되는 예약의 이름입니다. |
| `type` | 문자열로서의 작업 유형입니다. 지원되는 두 형식은 `batch_segmentation` 및 `export`입니다. |
| `properties` | 일정과 관련된 추가 등록 정보가 포함된 객체입니다. |
| `properties.segments` | `["*"]`을(를) 사용하면 모든 세그먼트가 포함됩니다. |
| `schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 작업을 두 번 이상 실행하도록 예약할 수 없습니다. cron 일정에 대한 자세한 내용은 [cron 식 형식](#appendix)의 부록을 참조하십시오. 이 예에서 &quot;0 0 1 * *&quot;는 이 일정이 매일 오전 1시에 실행됨을 의미합니다. |
| `state` | 일정 상태를 포함하는 문자열입니다. 지원되는 두 가지 상태는 `active` 및 `inactive`입니다. 기본적으로 상태는 `inactive`(으)로 설정됩니다. |

+++

## 특정 일정에 대한 세부 정보 업데이트 {#update}

`/config/schedules` 끝점에 대한 PATCH 요청을 수행하고 업데이트하려는 일정의 ID를 요청 경로에 제공하여 특정 일정을 업데이트할 수 있습니다.

PATCH 요청을 사용하면 개별 일정에 대해 [상태](#update-state) 또는 [cron 일정](#update-schedule)을 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 업데이트할 일정의 `id` 값입니다. |

>[!BEGINTABS]

>[!TAB 일정 상태 업데이트]

JSON 패치 작업을 사용하여 스케줄의 상태를 업데이트할 수 있습니다. 상태를 업데이트하려면 `path` 속성을 `/state`(으)로 선언하고 `value`을(를) `active` 또는 `inactive`(으)로 설정합니다. JSON 패치에 대한 자세한 내용은 [JSON 패치](https://datatracker.ietf.org/doc/html/rfc6902) 설명서를 참조하십시오.

**요청**

+++ 일정 상태를 업데이트하기 위한 샘플 요청입니다.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op": "add",
        "path": "/state",
        "value": "active"
    }
]'
```

+++

| 속성 | 설명 |
| -------- | ----------- |
| `path` | 패치할 값의 경로입니다. 이 경우 일정의 상태를 업데이트하는 중이므로 `path`의 값을 &quot;/state&quot;로 설정해야 합니다. |
| `value` | 일정 상태의 업데이트된 값. 이 값은 일정을 활성화하거나 비활성화하기 위해 &quot;활성&quot; 또는 &quot;비활성&quot;으로 설정할 수 있습니다. 조직이 스트리밍을 사용하도록 설정된 경우 **일정을 사용하지 않도록**&#x200B;할 수 없습니다. |

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

>[!TAB cron 일정 업데이트]

JSON 패치 작업을 사용하여 cron 일정을 업데이트할 수 있습니다. 일정을 업데이트하려면 `path` 속성을 `/schedule`(으)로 선언하고 `value`을(를) 올바른 크론 일정으로 설정합니다. JSON 패치에 대한 자세한 내용은 [JSON 패치](https://datatracker.ietf.org/doc/html/rfc6902) 설명서를 참조하십시오. cron 일정에 대한 자세한 내용은 [cron 식 형식](#appendix)의 부록을 참조하십시오.

>[!ENDTABS]

**요청**

+++ 일정을 업데이트하기 위한 샘플 요청입니다.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `path` | 업데이트할 값의 경로입니다. 이 경우 cron 일정을 업데이트하고 있으므로 `path`의 값을 `/schedule`(으)로 설정해야 합니다. |
| `value` | cron schedule의 업데이트된 값. 이 값은 cron schedule 형식이어야 합니다. 이 예에서는 일정이 매월 2일에 실행됩니다. |

+++

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

## 특정 일정 삭제

`/config/schedules` 끝점에 DELETE 요청을 하고 요청 경로에 삭제하려는 일정의 ID를 제공하여 특정 일정의 삭제를 요청할 수 있습니다.

**API 형식**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 삭제할 일정의 `id` 값입니다. |

**요청**

+++ 일정 삭제에 대한 샘플 요청입니다.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

## 다음 단계

이 안내서를 읽고 나면 이제 일정이 어떻게 돌아가는지에 대해 더 잘 이해할 수 있습니다.

## 부록 {#appendix}

다음 부록에서는 일정에 사용되는 cron 표현식의 형식을 설명합니다.

### 형식

cron 표현식은 6개 또는 7개의 필드로 구성된 문자열입니다. 표현식은 다음과 유사합니다.

`0 0 12 * * ?`

cron 표현식 문자열에서 첫 번째 필드는 초를 나타내고, 두 번째 필드는 분을 나타내고, 세 번째 필드는 시간을 나타내고, 네 번째 필드는 요일을 나타내고, 다섯 번째 필드는 월을 나타내고, 여섯 번째 필드는 요일을 나타냅니다. 연도를 나타내는 일곱 번째 필드를 선택적으로 포함할 수도 있습니다.

| 필드 이름 | 필수 여부 | 가능한 값 | 허용되는 특수 문자 |
| ---------- | -------- | --------------- | -------------------------- |
| 초 | 예 | 0-59 | `, - * /` |
| 분 | 예 | 0-59 | `, - * /` |
| 시간 | 예 | 0-23 | `, - * /` |
| 날짜(월 기준) | 예 | 1-31 | `, - * ? / L W` |
| 월 | 예 | 1-12, 1-12 | `, - * /` |
| 요일 | 예 | 1-7, 순토 | `, - * ? / L #` |
| 년 | 아니요 | 비어 있음, 1970-2099 | `, - * /` |

>[!NOTE]
>
>월 이름과 요일 이름은 대소문자를 구분합니다. **not**. 따라서 `SUN`은(는) `sun`을(를) 사용하는 것과 같습니다.

허용되는 특수 문자는 다음 의미를 나타냅니다.

| 특수 문자 | 설명 |
| ----------------- | ----------- |
| `*` | 이 값은 필드에서 **모두**&#x200B;개의 값을 선택하는 데 사용됩니다. 예를 들어, 시간 필드에 `*`을(를) 넣으면 **간격**&#x200B;시간을 의미합니다. |
| `?` | 이 값은 특정 값이 필요하지 않음을 의미합니다. 일반적으로 한 필드에 문자가 허용되는 항목을 지정하고 다른 필드에는 지정하지 않는 데 사용됩니다. 예를 들어, 매월 3일에 이벤트가 트리거되도록 하고 싶지만, 어떤 요일에 대해서는 신경 쓰지 않는 경우, `3`을(를) 요일 필드에 지정하고 `?`을(를) 요일 필드에 지정합니다. |
| `-` | 이 값은 필드에 대한 **포함** 범위를 지정하는 데 사용됩니다. 예를 들어 시간 필드에 `9-15`을(를) 입력하면 시간에 9, 10, 11, 12, 13, 14 및 15가 포함됩니다. |
| `,` | 이 값은 추가 값을 지정하는 데 사용됩니다. 예를 들어 요일 필드에 `MON, FRI, SAT`을(를) 입력하면 요일에 월요일, 금요일 및 토요일이 포함됩니다. |
| `/` | 이 값은 증분을 지정하는 데 사용됩니다. `/` 앞에 배치된 값은 증가하는 위치를 결정하지만, `/` 뒤에 배치된 값은 증가하는 양을 결정합니다. 예를 들어, 분 필드에 `1/7`을(를) 입력하면 분에 1, 8, 15, 22, 29, 36, 43, 50 및 57이 포함됩니다. |
| `L` | 이 값은 `Last`을(를) 지정하는 데 사용되며 사용하는 필드에 따라 의미가 다릅니다. 날짜 필드와 함께 사용하는 경우 해당 월의 마지막 날을 나타냅니다. 요일 필드와 함께 단독으로 사용하는 경우 요일의 마지막 요일인 토요일(`SAT`)을 나타냅니다. 다른 값과 함께 요일 필드를 사용하는 경우 해당 월의 해당 유형의 마지막 날을 나타냅니다. 예를 들어 요일 필드에 `5L`을(를) 입력하면 **해당 월의 마지막 금요일만**&#x200B;됩니다. |
| `W` | 이 값은 지정된 날짜와 가장 가까운 요일을 지정하는 데 사용됩니다. 예를 들어, `18W`을(를) 월 중 일 필드에 넣고 해당 월의 18일이 토요일인 경우 가장 가까운 평일인 17일 금요일에 트리거됩니다. 만약 그달 18일이 일요일이었다면 월요일과 평일이 가장 가까운 19일에 트리거됩니다. `1W`을(를) 월의 일 필드에 넣고 가장 가까운 평일이 이전 달에 있는 경우 이벤트는 여전히 **현재** 월의 가장 가까운 평일에 트리거됩니다.</br></br>또한 `L`과(와) `W`을(를) 결합하여 해당 월의 마지막 주말을 지정하는 `LW`을(를) 만들 수 있습니다. |
| `#` | 이 값은 한 달에 n번째 요일을 지정하는 데 사용됩니다. `#` 앞에 배치된 값은 요일을 나타내고 `#` 뒤에 배치된 값은 해당 월의 발생 횟수를 나타냅니다. 예를 들어 `1#3`을(를) 입력하면 이벤트가 그 달의 세 번째 일요일에 트리거됩니다. `X#5`을(를) 입력했으며 해당 월에 해당 요일의 다섯 번째 항목이 없는 경우 이벤트가 **트리거되지 않습니다**. 예를 들어, `1#5`을(를) 넣었지만 해당 월의 다섯 번째 일요일이 없는 경우 이벤트가 **not** 트리거됩니다. |

### 예시

다음 표에서는 샘플 cron 표현식 문자열을 보여 주고 그 의미를 설명합니다.

| 표현식 | 설명 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 그 행사는 매일 오후 1시에 시작될 것이다. |
| `0 30 9 * * ? 2022` | 이 행사는 2022년에 매일 오전 9시 30분에 시작될 예정입니다. |
| `0 * 18 * * ?` | 행사는 매일 오후 6시부터 시작해 오후 6시 59분에 종료되는 등 매 분마다 불이 붙는다. |
| `0 0/10 17 * * ?` | 이 행사는 매일 오후 5시부터 오후 6시까지 10분 간격으로 시작됩니다. |
| `0 13,38 5 ? 6 WED` | 이 행사는 6월 매주 수요일 오전 5시 13분과 5시 38분에 발사된다. |
| `0 30 12 ? * 4#3` | 행사는 매월 셋째 주 수요일 낮 12시 30분에 발사가 진행된다. |
| `0 30 12 ? * 6L` | 행사는 매월 마지막 주 금요일 낮 12시 30분에 발사가 진행된다. |
| `0 45 11 ? * MON-THU` | 이벤트는 매주 월, 화, 수, 목요일 오전 11시 45분에 발사됩니다. |