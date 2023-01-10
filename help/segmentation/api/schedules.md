---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;일정;예약;api;API;
solution: Experience Platform
title: API 엔드포인트 예약
description: 예약은 하루에 한 번 배치 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 3%

---

# 끝점 예약

예약은 하루에 한 번 배치 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. 를 사용할 수 있습니다 `/config/schedules` 종단점은 일정 목록을 검색하거나, 새 일정을 만들거나, 특정 예약의 세부 사항을 검색하거나, 특정 일정을 업데이트하거나, 특정 일정을 삭제하는 것입니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 [시작 안내서](./getting-started.md) 필수 헤더 및 예제 API 호출을 읽는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보입니다.

## 일정 목록 검색 {#retrieve-list}

에 GET 요청을 작성하여 조직의 모든 예약 목록을 검색할 수 있습니다 `/config/schedules` 엔드포인트.

**API 형식**

다음 `/config/schedules` endpoint는 결과를 필터링하는 데 도움이 되는 몇 가지 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만 고가의 오버헤드를 줄이는 데 도움이 되도록 사용하는 것이 좋습니다. 매개 변수 없이 이 종단점을 호출하면 조직에서 사용할 수 있는 모든 일정을 검색합니다. 여러 매개 변수를 앰퍼샌드( )로 구분하여 포함할 수 있습니다`&`).

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{START}` | 오프셋을 시작할 페이지를 지정합니다. 기본적으로 이 값은 0입니다. |
| `{LIMIT}` | 반환된 예약 수를 지정합니다. 기본적으로 이 값은 100입니다. |

**요청**

다음 요청은 조직 내에 게시된 마지막 10개의 일정을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 일정 목록이 HTTP 상태 200을 JSON으로 반환합니다.

>[!NOTE]
>
>다음 응답은 스페이스에 대해 잘렸으며 반환된 첫 번째 예약만 표시합니다.

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
| `_page.totalCount` | 반환된 총 일정 수 |
| `_page.pageSize` | 일정 페이지의 크기입니다. |
| `children.name` | 날짜의 문자열 이름입니다. |
| `children.type` | 문자열로서의 작업 유형입니다. 지원되는 두 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `children.properties` | 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `children.properties.segments` | 사용 `["*"]` 모든 세그먼트가 포함되도록 합니다. |
| `children.schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 두 번 이상 실행하도록 작업을 예약할 수 없습니다. 크론 스케줄에 대한 자세한 내용은 [cron 식 형식](#appendix). 이 예에서 &quot;0 0 1 *&quot;는 이 일정이 매일 오전 1시에 실행됨을 의미합니다. |
| `children.state` | 예약 상태가 포함된 문자열입니다. 지원되는 두 상태는 &quot;활성&quot; 및 &quot;비활성&quot;입니다. 기본적으로 상태는 &quot;비활성&quot;으로 설정됩니다. |

## 새 일정 만들기 {#create}

에 POST 요청을 작성하여 새 일정을 만들 수 있습니다 `/config/schedules` 엔드포인트.

**API 형식**

```http
POST /config/schedules
```

**요청**

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
| `name` | **필수 여부.** 날짜의 문자열 이름입니다. |
| `type` | **필수 여부.** 문자열로서의 작업 유형입니다. 지원되는 두 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `properties` | **필수 여부.** 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `properties.segments` | **필요한 경우 `type` equals &quot;batch_segmentation&quot;입니다.** 사용 `["*"]` 모든 세그먼트가 포함되도록 합니다. |
| `schedule` | *선택 사항입니다.* 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 두 번 이상 실행하도록 작업을 예약할 수 없습니다. 크론 스케줄에 대한 자세한 내용은 [cron 식 형식](#appendix). 이 예에서 &quot;0 0 1 *&quot;는 이 일정이 매일 오전 1시에 실행됨을 의미합니다. <br><br>이 문자열을 제공하지 않으면 시스템에서 생성한 일정이 자동으로 생성됩니다. |
| `state` | *선택 사항입니다.* 예약 상태가 포함된 문자열입니다. 지원되는 두 상태는 &quot;활성&quot; 및 &quot;비활성&quot;입니다. 기본적으로 상태는 &quot;비활성&quot;으로 설정됩니다. |

**응답**

성공적인 응답은 새로 만든 예약의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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

## 특정 일정 검색 {#get}

에 GET 요청을 수행하여 특정 예약에 대한 자세한 정보를 검색할 수 있습니다 `/config/schedules` 엔드포인트 및 요청 경로에서 검색할 예약의 ID를 제공합니다.

**API 형식**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 검색할 예약의 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 일정에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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
| `name` | 날짜의 문자열 이름입니다. |
| `type` | 문자열로서의 작업 유형입니다. 지원되는 두 유형은 다음과 같습니다 `batch_segmentation` 및 `export`. |
| `properties` | 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `properties.segments` | 사용 `["*"]` 모든 세그먼트가 포함되도록 합니다. |
| `schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 기간 동안 두 번 이상 실행하도록 작업을 예약할 수 없습니다. 크론 스케줄에 대한 자세한 내용은 [cron 식 형식](#appendix). 이 예에서 &quot;0 0 1 *&quot;는 이 일정이 매일 오전 1시에 실행됨을 의미합니다. |
| `state` | 예약 상태가 포함된 문자열입니다. 지원되는 두 상태는 다음과 같습니다 `active` 및 `inactive`. 기본적으로 상태는 로 설정되어 있습니다 `inactive`. |

## 특정 일정에 대한 세부 정보 업데이트 {#update}

에 PATCH 요청을 작성하여 특정 일정을 업데이트할 수 있습니다 `/config/schedules` endpoint 및 제공 요청 경로에서 업데이트하려는 예약의 ID

PATCH 요청을 통해 [state](#update-state) 또는 [예약](#update-schedule) 을 참조하십시오.

### 예약 상태 업데이트 {#update-state}

JSON 패치 작업을 사용하여 예약의 상태를 업데이트할 수 있습니다. 상태를 업데이트하려면 `path` property as `/state` 그리고 `value` 다음 중 하나를 수행합니다. `active` 또는 `inactive`. JSON 패치에 대한 자세한 내용은 [JSON 패치](https://datatracker.ietf.org/doc/html/rfc6902) 설명서.

**API 형식**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 업데이트할 예약의 값입니다. |

**요청**

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

| 속성 | 설명 |
| -------- | ----------- |
| `path` | 패치할 값의 경로입니다. 이 경우 예약의 상태를 업데이트하므로 값을 설정해야 합니다 `path` 를 &quot;/state&quot;로 설정합니다. |
| `value` | 일정 상태의 업데이트된 값입니다. 이 값을 &quot;활성&quot; 또는 &quot;비활성&quot;으로 설정하여 일정을 활성화하거나 비활성화할 수 있습니다. 참고 사항 **사용할 수 없음** IMS 조직이 스트리밍을 사용하도록 설정된 경우 예약을 비활성화합니다. |

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음)를 반환합니다.

### 크론 일정 업데이트 {#update-schedule}

JSON 패치 작업을 사용하여 콘 일정을 업데이트할 수 있습니다. 일정을 업데이트하려면 `path` property as `/schedule` 그리고 `value` 올바른 cron 일정에 따라 변경할 수 있습니다. JSON 패치에 대한 자세한 내용은 [JSON 패치](https://datatracker.ietf.org/doc/html/rfc6902) 설명서. 크론 스케줄에 대한 자세한 내용은 [cron 식 형식](#appendix).

**API 형식**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 업데이트할 예약의 값입니다. |

**요청**

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
        "value":"0 0 2 * *"
    }
]'
```

| 속성 | 설명 |
| -------- | ----------- |
| `path` | 업데이트할 값의 경로입니다. 이 경우 cron 일정을 업데이트하므로 값을 설정해야 합니다. `path` to `/schedule`. |
| `value` | 크론 예약의 업데이트된 값입니다. 이 값은 크론 예약의 형식이어야 합니다. 이 예에서는 매월 두 번째로 일정이 실행됩니다. |

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음)를 반환합니다.

## 특정 일정 삭제

에 DELETE 요청을 수행하여 특정 일정을 삭제하도록 요청할 수 있습니다 `/config/schedules` 엔드포인트 및 요청 경로에서 삭제할 예약의 ID를 제공합니다.

**API 형식**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 삭제할 예약의 값입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음)를 반환합니다.

## 다음 단계

이 안내서를 읽은 후에는 일정이 어떻게 작동하는지 더 잘 알 수 있습니다.

## 부록 {#appendix}

다음 부록에서는 예약에 사용되는 크론 표현식의 형식을 설명합니다.

### 형식

크론 표현식은 6 또는 7 필드로 구성된 문자열입니다. 표현식은 다음과 비슷합니다.

`0 0 12 * * ?`

cron 표현식 문자열에서 첫 번째 필드는 초를 나타내고, 두 번째 필드는 분을 나타냅니다. 두 번째 필드는 시간을 나타내고, 세 번째 필드는 시간을 나타내고, 네 번째 필드는 월의 일을 나타내고, 다섯 번째 필드는 월을 나타내고, 여섯 번째 필드는 요일을 나타냅니다. 연도를 나타내는 7번째 필드를 선택적으로 포함할 수도 있습니다.

| 필드 이름 | 필수 여부 | 가능한 값 | 허용되는 특수 문자 |
| ---------- | -------- | --------------- | -------------------------- |
| 초 | 예 | 0-59 | `, - * /` |
| 분 | 예 | 0-59 | `, - * /` |
| 시간 | 예 | 0-23 | `, - * /` |
| 날짜(월 기준) | 예 | 1-31 | `, - * ? / L W` |
| 월 | 예 | 1-12, 1월 12일 | `, - * /` |
| 요일 | 예 | 1-7, SUN-SAT | `, - * ? / L #` |
| 년 | 아니요 | 비어 있음, 1970-2099 | `, - * /` |

>[!NOTE]
>
>월의 이름과 요일 이름은 다음과 같습니다 **not** 대/소문자를 구분합니다. 따라서, `SUN` 는 를 사용하는 것과 같습니다 `sun`.

허용되는 특수 문자는 다음 의미를 나타냅니다.

| 특수 문자 | 설명 |
| ----------------- | ----------- |
| `*` | 이 값은 을 선택하는 데 사용됩니다 **모두** 값을 지정한 경우 이해할 수 있도록 해줍니다. 예를 들어, pting `*` 시간 필드는 **매** 시간 |
| `?` | 이 값은 특정 값이 필요하지 않음을 의미합니다. 일반적으로 한 필드에서 문자를 사용할 수 있는 항목을 지정하는 데 사용되지만 다른 필드에서는 지정하지 않습니다. 예를 들어 그 달의 3일마다 트리거되는 이벤트가 있지만 그 요일이 무엇인지에 대해서는 신경 쓰지 않으면 `3` 월 필드 및 `?` 요일 필드. |
| `-` | 이 값은 **포함** 필드의 범위. 예를 들어, `9-15` 시간 필드에서 이는 시간이 9, 10, 11, 12, 13, 14 및 15를 포함함을 의미합니다. |
| `,` | 이 값은 추가 값을 지정하는 데 사용됩니다. 예를 들어, `MON, FRI, SAT` 요일 필드에서 요일은 월요일, 금요일, 토요일이 포함됨을 의미합니다. |
| `/` | 이 값은 증분을 지정하는 데 사용됩니다. 다음 항목 앞에 배치된 값 `/` 값이 다음에 배치되는 반면, 다음에서 증가되는 위치를 결정합니다 `/` 증분을 결정합니다. 예를 들어, `1/7` 분 필드에서 이는 분이 1, 8, 15, 22, 29, 36, 43, 50 및 57을 포함함을 의미합니다. |
| `L` | 이 값은 `Last`에는 사용하는 필드에 따라 다른 의미가 있습니다. 월 일 필드에 사용하는 경우 해당 월의 마지막 날을 나타냅니다. 요일 필드와 함께 사용하는 경우 요일(토요일)을 나타냅니다`SAT`). 요일 필드에서 다른 값과 함께 사용하는 경우 해당 월의 해당 유형의 마지막 날을 나타냅니다. 예를 들어, `5L` 요일 필드에서 **전용** 그 달의 마지막 금요일을 포함시킵니다. |
| `W` | 이 값은 주어진 날짜에 가장 가까운 요일을 지정하는 데 사용됩니다. 예를 들어, `18W` 월 필드에서, 그 달의 18일은 토요일이었는데, 그것은 가장 가까운 금요일과 17일에 트리거될 것입니다. 그 달의 18일이 일요일이었다면 그것은 가장 가까운 월요일과 19일에 트리거될 것입니다. 만약 당신이 `1W` 월 필드에서 가장 가까운 요일이 이전 달에 있고 이벤트는 여전히 가장 가까운 요일에서 트리거됩니다 **현재** 월</br></br>또한 결합할 수 있습니다 `L` 및 `W` 만들기 `LW`: 월의 마지막 요일을 지정합니다. |
| `#` | 이 값은 한 달에 주의 n번째 요일을 지정하는 데 사용됩니다. 다음 항목 앞에 배치된 값 `#` 는 요일을 나타내는 반면 값은 다음에 옵니다 `#` 해당 월의 발생 항목을 나타냅니다. 예를 들어, `1#3`이 경우 해당 달 3일 이벤트가 시작될 것이다. 만약 당신이 `X#5` 그 달에 해당 요일의 다섯 번째 발생 횟수가 없습니다. 이벤트가 발생할 것입니다 **not** 트리거됩니다. 예를 들어, `1#5`그리고 그 달에 다섯 번째 일요일이 없는데, 그 행사가 있을 것입니다 **not** 트리거됩니다. |

### 예시

다음 표는 샘플 cron 표현식 문자열을 보여 주고 그 의미를 설명합니다.

| 표현식 | 설명 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 이벤트는 매일 오후 1시에 실행됩니다. |
| `0 30 9 * * ? 2022` | 이 행사는 2022년에 매일 오전 9시 30분에 시작될 것입니다. |
| `0 * 18 * * ?` | 이 행사는 매일 오후 6시부터 오후 6시 59분까지 열립니다. |
| `0 0/10 17 * * ?` | 이 이벤트는 10분마다, 오후 5시부터 시작하여 오후 6시까지, 매일 시작됩니다. |
| `0 13,38 5 ? 6 WED` | 그 행사는 6월에 매주 수요일 오전 5시 13분 그리고 5시 38분에 시작될 것이다. |
| `0 30 12 ? * 4#3` | 이 행사는 매달 세 번째 수요일 오후 12시 30분에 시작될 것이다. |
| `0 30 12 ? * 6L` | 이 행사는 매달 마지막 주 금요일 오후 12시 30분에 시작될 것이다. |
| `0 45 11 ? * MON-THU` | 이 대회는 월요일, 화요일, 수요일, 그리고 목요일에 오전 11시 45분에 시작됩니다. |