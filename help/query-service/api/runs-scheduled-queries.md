---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;예약된 쿼리 실행;예약된 쿼리 실행;쿼리 서비스;예약된 쿼리;예약된 쿼리;
solution: Experience Platform
title: 예약된 쿼리가 API 끝점을 실행합니다.
description: 다음 섹션에서는 쿼리 서비스 API로 예약된 쿼리를 실행하기 위해 수행할 수 있는 다양한 API 호출을 안내합니다.
role: Developer
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---

# 예약된 쿼리 실행 엔드포인트

## 샘플 API 호출

사용할 헤더를 이해했으므로 [!DNL Query Service] API를 호출할 준비가 되었습니다. 다음 섹션에서는 [!DNL Query Service] API를 사용하여 수행할 수 있는 다양한 API 호출을 살펴봅니다. 각 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

### 지정된 예약된 쿼리에 대한 모든 실행 목록을 검색합니다.

현재 실행 중인지 또는 이미 완료되었는지에 관계없이 특정 예약된 쿼리에 대해 모든 실행 목록을 검색할 수 있습니다. 이 작업은 `/schedules/{SCHEDULE_ID}/runs` 끝점에 대한 GET 요청을 통해 수행됩니다. 여기서 `{SCHEDULE_ID}`은(는) 검색하려는 실행이 예약된 쿼리의 `id` 값입니다.

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 예약된 쿼리의 `id` 값입니다. |
| `{QUERY_PARAMETERS}` | (*선택 사항*) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다. 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 지정된 예약된 쿼리에 대한 실행을 나열하기 위해 사용할 수 있는 쿼리 매개 변수의 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 지정된 예약된 쿼리에 사용할 수 있는 모든 실행을 검색합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬하는 데 사용할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어 `orderby=created`은(는) 만들어진 항목별로 오름차순으로 결과를 정렬합니다. 만들기 전에 `-`을(를) 추가하면(`orderby=-created`) 내림차순으로 만들어진 항목별로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20*) |
| `start` | ISO 형식 타임스탬프를 지정하여 결과 순서를 지정합니다. 시작 날짜가 지정되지 않은 경우, API 호출이 가장 오래된 실행을 먼저 반환한 다음 더 최근의 결과를 계속 나열합니다.<br> ISO 타임스탬프를 사용하면 날짜 및 시간에 따라 서로 다른 수준의 세부기간을 사용할 수 있습니다. 기본 ISO 타임스탬프는 `2020-09-07` 형식을 사용하여 2020년 9월 7일의 날짜를 나타냅니다. 보다 복잡한 예제는 `2022-11-05T08:15:30-05:00`(으)로 작성되며 2022년 11월 5일 오전 8:15:30(미국 동부 표준시)에 해당합니다. 시간대는 UTC 오프셋을 사용하여 제공될 수 있으며 접미사 &quot;Z&quot;(`2020-01-01T01:01:01Z`)로 표시됩니다. 시간대가 제공되지 않으면 기본값은 0입니다. |
| `property` | 필드를 기반으로 결과를 필터링합니다. **must** 필터는 HTML 이스케이프해야 합니다. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `created`, `state` 및 `externalTrigger`입니다. 지원되는 연산자 목록은 `>`(보다 큼), `<`(보다 작음), `==`(과 같음) 및 `!=`(과 같지 않음)입니다. 예를 들어 `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z`은(는) 2019년 4월 20일 이후에 수동으로 만들고 성공하고 만든 모든 실행을 반환합니다. |

**요청**

다음 요청은 지정된 예약된 쿼리에 대한 마지막 네 번의 실행을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 JSON으로 지정된 예약된 쿼리에 대한 실행 목록과 함께 HTTP 상태 200을 반환합니다. 다음 응답은 지정된 예약된 쿼리에 대해 마지막 네 번의 실행을 반환합니다.

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>`_links.cancel`의 값을 사용하여 [지정된 예약된 쿼리에 대한 실행을 중지](#immediately-stop-a-run-for-a-specific-scheduled-query)할 수 있습니다.

### 특정 예약된 쿼리에 대한 실행을 즉시 트리거

`/schedules/{SCHEDULE_ID}/runs` 끝점에 대한 POST 요청을 수행하여 지정된 예약된 쿼리에 대한 실행을 즉시 트리거할 수 있습니다. 여기서 `{SCHEDULE_ID}`은(는) 트리거하려는 예약된 쿼리의 `id` 값입니다.

**API 형식**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### 특정 예약된 쿼리에 대한 실행 세부 정보 검색

`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 끝점에 GET 요청을 하고 예약된 쿼리의 ID와 요청 경로에 실행을 모두 제공하여 특정 예약된 쿼리의 실행에 대한 세부 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 세부 정보를 검색하려는 예약된 쿼리의 `id` 값입니다. |
| `{RUN_ID}` | 검색할 실행의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 실행에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### 특정 예약된 쿼리에 대한 실행을 즉시 중지합니다.

`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 끝점에 PATCH 요청을 하고 예약된 쿼리의 ID와 요청 경로에 실행을 모두 제공하여 특정 예약된 쿼리에 대한 실행을 즉시 중지할 수 있습니다.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 세부 정보를 검색하려는 예약된 쿼리의 `id` 값입니다. |
| `{RUN_ID}` | 검색할 실행의 `id` 값입니다. |

**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```
