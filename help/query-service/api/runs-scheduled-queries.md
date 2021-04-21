---
keywords: Experience Platform;home;popular topics;query service;run scheduled queries;run scheduled query service;scheduled queries;scheduled queries
solution: Experience Platform
title: 예약된 쿼리 실행 API 끝점
topic-legacy: runs for scheduled queries
description: 다음 섹션에서는 쿼리 서비스 API를 사용하여 예약된 쿼리를 실행하기 위해 수행할 수 있는 다양한 API 호출을 안내합니다.
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 2%

---

# 예약된 쿼리 실행 끝점

## 샘플 API 호출

이제 사용할 헤더를 이해했으므로 [!DNL Query Service] API에 대한 호출을 시작할 준비가 되었습니다. 다음 섹션에서는 [!DNL Query Service] API를 사용하여 수행할 수 있는 다양한 API 호출을 안내합니다. 각 호출에는 일반 API 형식, 필수 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

### 지정된 예약 쿼리에 대한 모든 실행 목록 검색

현재 실행 중인지 또는 이미 완료되었는지에 관계없이 특정 예약 쿼리에 대한 모든 실행 목록을 검색할 수 있습니다. 이 작업은 검색하려는 실행이 예약된 쿼리의 `{SCHEDULE_ID}` 값인 `/schedules/{SCHEDULE_ID}/runs` 끝점에 GET 요청을 함으로써 수행됩니다.`id`

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 예약된 쿼리의 `id` 값입니다. |
| `{QUERY_PARAMETERS}` | (*선택적*) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다. |

**쿼리 매개 변수**

다음은 지정된 예약 쿼리에 대한 실행 목록을 나열할 수 있는 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 지정된 예약 쿼리에 사용할 수 있는 모든 실행이 검색됩니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어 `orderby=created`은(는) 결과를 오름차순으로 정렬합니다. 만들기 전에 `-`(`orderby=-created`)을 추가하면 작성된 항목이 내림차순으로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어하기 위해 페이지 크기 제한을 지정합니다. (*기본값:20*) |
| `start` | 0부터 시작하는 번호 매기기를 사용하여 응답 목록을 오프셋합니다. 예를 들어 `start=2`은 세 번째 나열된 쿼리에서 시작하는 목록을 반환합니다. (*기본값:0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **은(는) HTML을 escape해야 합니다.** 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `created`, `state` 및 `externalTrigger`입니다. 지원되는 연산자 목록은 `>`(보다 큼), `<`(보다 작음) 및 `==`(같음) 및 `!=`(같지 않음)입니다. 예를 들어 `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z`은 2019년 4월 20일 이후에 수동으로 만들고, 성공하고, 만든 모든 실행을 반환합니다. |

**요청**

다음 요청은 지정된 예약 쿼리에 대해 마지막 4개의 실행을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 예약된 쿼리에 대한 실행 목록이 있는 HTTP 상태 200을 JSON으로 반환합니다. 다음 응답은 지정된 예약 쿼리에 대한 마지막 4개의 실행을 반환합니다.

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
>`_links.cancel` 값을 사용하여 지정된 예약된 쿼리](#immediately-stop-a-run-for-a-specific-scheduled-query)에 대한 실행을 [중지할 수 있습니다.

### 특정 예약된 쿼리에 대해 실행을 즉시 트리거합니다.

`/schedules/{SCHEDULE_ID}/runs` 끝점에 POST 요청을 하여 지정된 예약된 쿼리에 대한 실행을 즉시 트리거할 수 있습니다. 여기서 `{SCHEDULE_ID}`은(는) 실행을 트리거하려는 예약된 쿼리의 `id` 값입니다.

**API 형식**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 끝점에 GET 요청을 하고 예약된 쿼리의 ID와 요청 경로에서 실행을 모두 제공하여 특정 예약된 쿼리에 대한 실행에 대한 세부 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 세부 정보를 검색할 실행이 있는 예약된 쿼리의 `id` 값. |
| `{RUN_ID}` | 검색할 실행의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 실행에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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

`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 끝점에 PATCH 요청을 하고 예약된 쿼리의 ID와 요청 경로에서 실행을 모두 제공하여 특정 예약된 쿼리에 대한 실행을 즉시 중지할 수 있습니다.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 세부 정보를 검색할 실행이 있는 예약된 쿼리의 `id` 값. |
| `{RUN_ID}` | 검색할 실행의 `id` 값입니다. |

**요청**

이 API 요청에서는 페이로드에 대한 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
