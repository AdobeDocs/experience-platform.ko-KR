---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;일정;예약;api;API;
solution: Experience Platform
title: API 엔드포인트 예약
topic-legacy: developer guide
description: 예약은 하루에 한 번 배치 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다.
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---

# 끝점 예약

예약은 하루에 한 번 배치 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. 를 사용할 수 있습니다 `/config/schedules` 종단점은 일정 목록을 검색하거나, 새 일정을 만들거나, 특정 예약의 세부 사항을 검색하거나, 특정 일정을 업데이트하거나, 특정 일정을 삭제하는 것입니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 [!DNL Adobe Experience Platform Segmentation Service] API. 계속하기 전에 [시작 안내서](./getting-started.md) 필수 헤더 및 예제 API 호출을 읽는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보입니다.

## 일정 목록 검색 {#retrieve-list}

IMS 조직에 대한 GET 요청을 수행하여 모든 스케줄 목록을 검색할 수 있습니다 `/config/schedules` 엔드포인트.

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

다음 요청은 IMS 조직 내에 게시된 마지막 10개의 일정을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `_page.totalCount` | 반환된 총 일정 수 |
| `_page.pageSize` | 일정 페이지의 크기입니다. |
| `children.name` | 날짜의 문자열 이름입니다. |
| `children.type` | 문자열로서의 작업 유형입니다. 지원되는 두 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `children.properties` | 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `children.properties.segments` | 사용 `["*"]` 모든 세그먼트가 포함되도록 합니다. |
| `children.schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 두 번 이상 실행하도록 작업을 예약할 수 없습니다. 크론 예약에 대한 자세한 내용은 [cron 식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서. 이 예에서 &quot;0 0 1 *&quot;는 이 일정이 매월 1일 자정에 실행됨을 의미합니다. |
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
| `name` | **필수 여부.** 날짜의 문자열 이름입니다. |
| `type` | **필수 여부.** 문자열로서의 작업 유형입니다. 지원되는 두 유형은 &quot;batch_segmentation&quot; 및 &quot;export&quot;입니다. |
| `properties` | **필수 여부.** 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `properties.segments` | **필요한 경우 `type` equals &quot;batch_segmentation&quot;입니다.** 사용 `["*"]` 모든 세그먼트가 포함되도록 합니다. |
| `schedule` | *선택 사항입니다.* 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 동안 두 번 이상 실행하도록 작업을 예약할 수 없습니다. 크론 예약에 대한 자세한 내용은 [cron 식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서. 이 예에서 &quot;0 0 1 *&quot;는 이 일정이 매월 1일 자정에 실행됨을 의미합니다. <br><br>이 문자열을 제공하지 않으면 시스템에서 생성한 일정이 자동으로 생성됩니다. |
| `state` | *선택 사항입니다.* 예약 상태가 포함된 문자열입니다. 지원되는 두 상태는 &quot;활성&quot; 및 &quot;비활성&quot;입니다. 기본적으로 상태는 &quot;비활성&quot;으로 설정됩니다. |

**응답**

성공적인 응답은 새로 만든 예약의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 일정에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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
| `name` | 날짜의 문자열 이름입니다. |
| `type` | 문자열로서의 작업 유형입니다. 지원되는 두 유형은 다음과 같습니다 `batch_segmentation` 및 `export`. |
| `properties` | 예약과 관련된 추가 속성이 포함된 객체입니다. |
| `properties.segments` | 사용 `["*"]` 모든 세그먼트가 포함되도록 합니다. |
| `schedule` | 작업 일정을 포함하는 문자열입니다. 작업은 하루에 한 번만 실행되도록 예약할 수 있습니다. 즉, 24시간 기간 동안 두 번 이상 실행하도록 작업을 예약할 수 없습니다. 크론 예약에 대한 자세한 내용은 [cron 식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서. 이 예에서 &quot;0 0 1 *&quot;는 이 일정이 매월 1일 자정에 실행됨을 의미합니다. |
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
| `path` | 패치할 값의 경로입니다. 이 경우 예약의 상태를 업데이트하므로 값을 설정해야 합니다 `path` 를 &quot;/state&quot;로 설정합니다. |
| `value` | 일정 상태의 업데이트된 값입니다. 이 값을 &quot;활성&quot; 또는 &quot;비활성&quot;으로 설정하여 일정을 활성화하거나 비활성화할 수 있습니다. |

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음)를 반환합니다.

### 크론 일정 업데이트 {#update-schedule}

JSON 패치 작업을 사용하여 콘 일정을 업데이트할 수 있습니다. 일정을 업데이트하려면 `path` property as `/schedule` 그리고 `value` 올바른 cron 일정에 따라 변경할 수 있습니다. JSON 패치에 대한 자세한 내용은 [JSON 패치](https://datatracker.ietf.org/doc/html/rfc6902) 설명서. 크론 예약에 대한 자세한 내용은 [cron 식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음)를 반환합니다.

## 다음 단계

이 안내서를 읽은 후에는 일정이 어떻게 작동하는지 더 잘 알 수 있습니다.
