---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 일정
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# 개발자 가이드 예약

intro

- 예약 목록 검색
- 새 일정 만들기
- 특정 일정 검색
- 특정 일정 업데이트
- 특정 일정 삭제

## 시작하기

이 안내서에서 사용되는 API 끝점은 세그멘테이션 API의 일부입니다. 계속하기 전에 세그멘테이션 개발자 [안내서를](./getting-started.md)검토하십시오.

특히 세그멘테이션 개발자 안내서의 [시작 섹션은](./getting-started.md#getting-started) 관련 항목에 대한 링크, 문서에서 샘플 API 호출 읽기에 대한 안내, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 포함합니다.

## 예약 목록 검색

IMS 조직에 대한 모든 일정 목록을 `/config/schedules` 끝점에 GET 요청을 수행하여 검색할 수 있습니다.

**API 형식**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*선택*&#x200B;사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다.

**쿼리 매개 변수**

다음은 예약을 나열하기 위한 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 일정을 검색합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `start` | 오프셋을 시작할 페이지를 지정합니다. 기본적으로 이 값은 0입니다. |
| `limit` | 반환된 예약 수를 지정합니다. 기본적으로 이 값은 100입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 일정 목록이 있는 HTTP 상태 200을 JSON으로 반환합니다.

```json
{
    "_page": {
        "totalCount": 1,
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

## 새 일정 만들기

종단점에 POST 요청을 만들어 새 일정을 만들 수 `/config/schedules` 있습니다.

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
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| 매개 변수 | 설명 |
| --------- | ------------ |
| `name` | **필수 여부.** 예약의 이름입니다. |
| `type` | **필수 여부.** 문자열로서의 작업 유형입니다. 지원되는 두 가지 유형은 `batch_segmentation` 및 `export`입니다. |
| `properties` | **필수 여부.** 예약과 관련된 추가 속성이 포함된 개체. |
| `properties.segments` | **Required when`type`equals`batch_segmentation`.** 를 `["*"]` 사용하면 모든 세그먼트가 포함됩니다. |
| `schedule` | **필수 여부.** 작업 일정을 포함하는 문자열. cron 예약에 대한 자세한 내용은 cron [식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. 이 예에서 &quot;0 0 1 * *&quot;는 이 일정이 매월 1일에 자정에 실행됨을 의미합니다. |
| `state` | *선택 사항입니다.* 예약 상태를 포함하는 문자열입니다. 지원되는 두 상태는 `active` 및 `inactive`입니다. 기본적으로 상태는 로 `inactive`설정됩니다. |

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

## 특정 일정 검색

GET 요청을 `/config/schedules` 끝점에 만들고 요청 경로에서 예약의 `id` 값을 제공하여 특정 일정에 대한 자세한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:검색할 스케줄의 `id` 값입니다.

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
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
```

## 특정 일정에 대한 세부 정보 업데이트

PATCH 요청을 `/config/schedules` 끝점에 만들고 요청 경로에서 예약의 `id` 값을 제공하여 지정된 일정을 업데이트할 수 있습니다.

PATCH 요청은 두 가지 경로를 지원합니다. `/state` 및 `/schedule`Adobe

### 업데이트 일정 상태

을 `/state` 사용하여 스케줄 상태(활성 또는 비활성)를 업데이트할 수 있습니다. 상태를 업데이트하려면 값을 `active` 또는 으로 설정해야 `inactive`합니다.

**API 형식**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:업데이트할 예약의 `id` 값.

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
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
]
'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `path` | 패치할 값의 경로입니다. 이 경우 예약 상태를 업데이트하므로 의 값을 `path` 로 설정해야 `/state`합니다. |
| `value` | 의 업데이트된 값입니다 `/state`. 이 값은 예약 활성화 또는 비활성화로 `active` 설정하거나 `inactive` 비활성화할 수 있습니다. |

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

### 예약 cron 일정 업데이트

를 `schedule` 사용하여 cron 일정을 업데이트할 수 있습니다. cron 예약에 대한 자세한 내용은 cron [식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오.

**API 형식**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:업데이트할 예약의 `id` 값.

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `path` | 패치할 값의 경로입니다. 이 경우 일정의 cron 일정을 업데이트하므로 의 값을 `path` 로 설정해야 합니다 `/schedule`. |
| `value` | 의 업데이트된 값입니다 `/state`. 이 값은 cron 일정 형식이어야 합니다. 이 예에서는 매월 둘째 달에 일정이 실행됩니다. |

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

## 특정 일정 삭제

DELETE 요청을 에 `/config/schedules` 만들고 요청 경로에 예약 `id` 값을 제공하여 지정된 일정을 삭제하도록 요청할 수 있습니다.

**API 형식**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:삭제할 예약의 `id` 값.

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 204(콘텐츠 없음)를 반환합니다.

```json
(No Content) Schedule deleted successfully
```

## 다음 단계
