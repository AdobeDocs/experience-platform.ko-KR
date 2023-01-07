---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;예약된 쿼리 실행;예약된 쿼리 실행;쿼리 서비스;예약된 쿼리;예약된 쿼리;예약된 쿼리
solution: Experience Platform
title: 예약된 쿼리 실행 API 끝점
description: 다음 섹션에서는 Query Service API를 사용하여 예약된 쿼리를 실행하기 위해 수행할 수 있는 다양한 API 호출을 안내합니다.
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 2%

---

# 예약된 쿼리 실행 끝점

## 샘플 API 호출

이제 사용할 헤더를 이해하므로 을 호출할 준비가 되었습니다. [!DNL Query Service] API. 다음 섹션에서는 를 사용하여 수행할 수 있는 다양한 API 호출을 살펴봅니다 [!DNL Query Service] API. 각 호출에는 일반 API 형식, 필수 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함되어 있습니다.

### 지정된 예약된 쿼리에 대한 모든 실행 목록을 검색합니다

현재 실행 중인지 또는 이미 완료되었는지에 관계없이 특정 예약된 쿼리에 대해 모든 실행 목록을 검색할 수 있습니다. 이 작업은 GET 요청을 `/schedules/{SCHEDULE_ID}/runs` 엔드포인트, 위치 `{SCHEDULE_ID}` 은 `id` 검색할 실행의 예약된 쿼리의 값입니다.

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 검색할 예약된 쿼리의 값입니다. |
| `{QUERY_PARAMETERS}` | (*선택 사항입니다*) 응답에서 반환된 결과를 구성하는 요청 경로에 매개 변수가 추가되었습니다. 여러 매개 변수를 앰퍼샌드( )로 구분하여 포함할 수 있습니다`&`). 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 지정된 예약된 쿼리에 대한 실행을 나열하기 위해 사용할 수 있는 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 지정된 예약된 쿼리에 사용할 수 있는 모든 실행이 검색됩니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬할 필드를 지정합니다. 지원되는 필드는 다음과 같습니다 `created` 및 `updated`. 예, `orderby=created` 은(는) 결과를 오름차순으로 정렬하게 됩니다. 추가 `-` 생성 전(`orderby=-created`)은 내림차순으로 만든 항목을 정렬합니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20년*) |
| `start` | 영(0) 기반 번호 지정을 사용하여 응답 목록을 오프셋합니다. 예, `start=2` 세 번째 나열된 쿼리에서 시작하는 목록을 반환합니다. (*기본값: 0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **반드시** HTML 이스케이프 처리됨. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 다음과 같습니다 `created`, `state`, 및 `externalTrigger`. 지원되는 연산자 목록은 다음과 같습니다 `>` (보다 큼), `<` (보다 작음), 및  `==` (같음), 및 `!=` (같지 않음). 예, `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` 은 2019년 4월 20일 이후에 수동으로 만들고, 성공하고, 만든 모든 실행을 반환합니다. |

**요청**

다음 요청은 지정된 예약된 쿼리에 대해 최근 4개의 실행을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 예약된 쿼리에 대한 실행 목록이 있는 HTTP 상태 200을 JSON으로 반환합니다. 다음 응답은 지정된 예약된 쿼리에 대해 마지막 4개의 실행을 반환합니다.

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
>다음 값을 사용할 수 있습니다. `_links.cancel` to [지정된 예약된 쿼리에 대한 실행 중지](#immediately-stop-a-run-for-a-specific-scheduled-query).

### 특정 예약된 쿼리에 대해 실행을 즉시 트리거합니다

에 POST 요청을 작성하여 지정된 예약된 쿼리에 대한 실행을 즉시 트리거할 수 있습니다 `/schedules/{SCHEDULE_ID}/runs` 엔드포인트, 위치 `{SCHEDULE_ID}` 은 `id` 실행할 예약된 쿼리의 값입니다.

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

### 특정 예약된 쿼리에 대한 실행 세부 정보를 검색합니다

에 GET 요청을 수행하여 특정 예약된 쿼리에 대한 실행 세부 사항을 검색할 수 있습니다 `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 엔드포인트 및 예약된 쿼리의 ID와 요청 경로에서 실행을 모두 제공합니다.

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 세부 정보를 검색하려는 실행 예약된 쿼리의 값입니다. |
| `{RUN_ID}` | 다음 `id` 검색할 실행의 값입니다. |

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

### 특정 예약된 쿼리에 대한 실행을 즉시 중지합니다

에 PATCH 요청을 수행하여 특정 예약된 쿼리에 대한 실행을 즉시 중지할 수 있습니다 `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 엔드포인트 및 예약된 쿼리의 ID와 요청 경로에서 실행을 모두 제공합니다.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 세부 정보를 검색하려는 실행 예약된 쿼리의 값입니다. |
| `{RUN_ID}` | 다음 `id` 검색할 실행의 값입니다. |

**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

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
