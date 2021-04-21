---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;일정;일정;api;Segmentation;home;popular topmentation;segmentation;service;schedule;api;API
solution: Experience Platform
title: API 끝점 예약
topic-legacy: developer guide
description: 예약은 하루에 한 번 일괄 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 3%

---

# 일정 끝점

예약은 하루에 한 번 일괄 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. `/config/schedules` 끝점을 사용하여 일정 목록을 검색하고, 새 일정을 만들고, 특정 일정의 세부 정보를 검색하고, 특정 일정을 업데이트하거나, 특정 일정을 삭제할 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 계속하기 전에 필수 헤더 및 예제 API 호출 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보가 필요하면 [시작 안내서](./getting-started.md)를 검토하십시오.

## 일정 목록 검색 {#retrieve-list}

`/config/schedules` 종단점에 GET 요청을 함으로써 IMS 조직에 대한 모든 일정 목록을 가져올 수 있습니다.

**API 형식**

`/config/schedules` 끝점은 결과를 필터링하는 데 도움이 되는 여러 쿼리 매개 변수를 지원합니다. 이러한 매개 변수는 선택 사항이지만, 비싼 오버헤드를 줄이려면 매개 변수를 사용하는 것이 좋습니다. 매개 변수 없이 이 끝점을 호출하면 조직에 사용할 수 있는 모든 일정을 검색합니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다.

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

다음 요청은 IMS 조직 내에 게시된 최근 10개의 일정을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 일정 목록이 포함된 HTTP 상태 200을 JSON으로 반환합니다.

>[!NOTE]
>
>다음 응답은 공간에 대해 잘렸고 반환된 첫 번째 예약만 표시합니다.

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
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
| `_page.totalCount` | 반환된 총 예약 수입니다. |
| `_page.pageSize` | 일정 페이지의 크기입니다. |
| `children.name` | 예약의 이름(문자열). |
| `children.type` | 문자열 작업 유형입니다. 지원되는 두 가지 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `children.properties` | 예약과 관련된 추가 속성을 포함하는 객체입니다. |
| `children.properties.segments` | `["*"]`을 사용하면 모든 세그먼트가 포함됩니다. |
| `children.schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있으므로 24시간 동안 두 번 이상 실행되도록 작업을 예약할 수 없습니다. cron 예약에 대한 자세한 내용은 [cron 식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. 이 예에서 &quot;0 0 1 * *&quot;는 이 일정이 매달 첫째 자정에 실행됨을 의미합니다. |
| `children.state` | 예약 상태를 포함하는 문자열입니다. 지원되는 두 가지 상태는 &quot;활성&quot; 및 &quot;비활성&quot;입니다. 기본적으로 상태는 &quot;비활성&quot;으로 설정됩니다. |

## 새 일정 {#create} 만들기

`/config/schedules` 끝점에 POST 요청을 하여 새 일정을 만들 수 있습니다.

**API 형식**

```http
POST /config/schedules
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | **필수 여부.** 예약의 이름(문자열). |
| `type` | **필수 여부.** 문자열 작업 유형입니다. 지원되는 두 가지 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `properties` | **필수 여부.** 예약과 관련된 추가 속성을 포함하는 객체입니다. |
| `properties.segments` | **&quot; `type` batch_segmentation&quot;이 될 때 필요합니다.** 을  `["*"]` 사용하면 모든 세그먼트가 포함됩니다. |
| `schedule` | *선택 사항.* 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있으므로 24시간 동안 두 번 이상 실행되도록 작업을 예약할 수 없습니다. cron 예약에 대한 자세한 내용은 [cron 식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. 이 예에서 &quot;0 0 1 * *&quot;는 이 일정이 매달 첫째 자정에 실행됨을 의미합니다. <br><br>이 문자열을 제공하지 않으면 시스템 생성 일정이 자동으로 생성됩니다. |
| `state` | *선택 사항.* 예약 상태를 포함하는 문자열입니다. 지원되는 두 가지 상태는 &quot;활성&quot; 및 &quot;비활성&quot;입니다. 기본적으로 상태는 &quot;비활성&quot;으로 설정됩니다. |

**응답**

성공적인 응답은 새로 만든 일정에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
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

## 특정 일정 {#get} 검색

`/config/schedules` 종단점에 GET 요청을 하고 요청 경로에서 검색할 예약의 ID를 제공하여 특정 일정에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 스케줄의 `id` 값. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 일정에 대한 자세한 정보가 있는 HTTP 상태 200을 반환합니다.

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
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

| 속성 | 설명 |
| -------- | ------------ |
| `name` | 예약의 이름(문자열). |
| `type` | 문자열 작업 유형입니다. 지원되는 두 유형은 `batch_segmentation` 및 `export`입니다. |
| `properties` | 예약과 관련된 추가 속성을 포함하는 객체입니다. |
| `properties.segments` | `["*"]`을 사용하면 모든 세그먼트가 포함됩니다. |
| `schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있으므로 24시간 동안 두 번 이상 실행되도록 작업을 예약할 수 없습니다. cron 예약에 대한 자세한 내용은 [cron 식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. 이 예에서 &quot;0 0 1 * *&quot;는 이 일정이 매달 첫째 자정에 실행됨을 의미합니다. |
| `state` | 예약 상태를 포함하는 문자열입니다. 지원되는 두 상태는 `active` 및 `inactive`입니다. 기본적으로 상태는 `inactive`으로 설정됩니다. |

## 특정 일정 {#update} 업데이트 세부 정보

PATCH 요청을 `/config/schedules` 끝점에 만들고 요청 경로에서 업데이트하려는 예약의 ID를 제공하여 특정 일정을 업데이트할 수 있습니다.

PATCH 요청을 통해 개별 일정에 대해 [state](#update-state) 또는 [cron 일정](#update-schedule)을 업데이트할 수 있습니다.

### 업데이트 일정 상태 {#update-state}

JSON 패치 작업을 사용하여 일정 상태를 업데이트할 수 있습니다. 상태를 업데이트하려면 `path` 속성을 `/state`으로 선언하고 `value`를 `active` 또는 `inactive` 중 하나로 설정합니다. JSON 패치에 대한 자세한 내용은 [JSON 패치](http://jsonpatch.com/) 설명서를 참조하십시오.

**API 형식**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 업데이트할 예약의 `id` 값입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `path` | 패치할 값의 경로입니다. 이 경우 일정 상태를 업데이트하므로 `path` 값을 &quot;/state&quot;로 설정해야 합니다. |
| `value` | 예약 상태의 업데이트된 값입니다. 이 값을 &quot;활성&quot; 또는 &quot;비활성&quot;으로 설정하여 일정을 활성화하거나 비활성화할 수 있습니다. |

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

### 업데이트 cron 일정 {#update-schedule}

JSON 패치 작업을 사용하여 충돌 일정을 업데이트할 수 있습니다. 일정을 업데이트하려면 `path` 속성을 `/schedule`(으)로 선언하고 `value`을(를) 유효한 cron 일정으로 설정합니다. JSON 패치에 대한 자세한 내용은 [JSON 패치](http://jsonpatch.com/) 설명서를 참조하십시오. cron 예약에 대한 자세한 내용은 [cron 식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오.

**API 형식**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 업데이트할 예약의 `id` 값입니다. |

**요청**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `path` | 업데이트할 값의 경로입니다. 이 경우 cron 일정을 업데이트하므로 `path` 값을 `/schedule`으로 설정해야 합니다. |
| `value` | cron 예약의 업데이트된 값입니다. 이 값은 cron 일정 형식이어야 합니다. 이 예에서는 매월 둘째 달에 일정이 실행됩니다. |

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

## 특정 일정 삭제

`/config/schedules` 끝점에 DELETE 요청을 하고 요청 경로에서 삭제할 일정의 ID를 제공하여 특정 일정을 삭제하도록 요청할 수 있습니다.

**API 형식**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 삭제할 일정의 `id` 값입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

## 다음 단계

이 안내서를 읽고 나면 이제 일정이 어떻게 진행되는지 더 잘 알 수 있다.
