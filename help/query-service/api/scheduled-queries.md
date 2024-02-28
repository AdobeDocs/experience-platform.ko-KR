---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;예약된 쿼리;예약된 쿼리;
solution: Experience Platform
title: 일정 끝점
description: 다음 섹션에서는 쿼리 서비스 API를 사용하여 예약된 쿼리에 대해 수행할 수 있는 다양한 API 호출을 안내합니다.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---

# 일정 끝점

## 샘플 API 호출

사용할 헤더를 이해했으므로 이제 [!DNL Query Service] API. 다음 섹션에서는 를 사용하여 수행할 수 있는 다양한 API 호출을 살펴봅니다 [!DNL Query Service] API. 각 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

### 예약된 쿼리 목록 검색

에 GET 요청을 하여 조직에 대해 모든 예약된 쿼리 목록을 검색할 수 있습니다. `/schedules` 엔드포인트.

**API 형식**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*선택 사항*) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`). 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 예약된 쿼리를 나열하기 위해 사용할 수 있는 쿼리 매개 변수의 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 예약된 쿼리를 검색합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬하는 데 사용할 필드를 지정합니다. 지원되는 필드는 다음과 같습니다. `created` 및 `updated`. 예를 들어, `orderby=created` 생성된 항목별로 오름차순으로 결과를 정렬합니다. 추가 `-` 만들기 전(`orderby=-created`)은 만들어진 항목별로 내림차순으로 정렬합니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20*) |
| `start` | ISO 형식 타임스탬프를 지정하여 결과 순서를 지정합니다. 시작 날짜가 지정되지 않은 경우 API 호출은 가장 오래 전에 생성된 예약 쿼리를 먼저 반환한 다음 더 최근 결과를 계속 나열합니다.<br> ISO 타임스탬프를 사용하면 날짜 및 시간에 따라 다양한 세부 기간 수준을 사용할 수 있습니다. 기본 ISO 타임스탬프는 다음 형식을 사용합니다. `2020-09-07` 날짜를 2020년 9월 7일로 표현합니다. 보다 복잡한 예제는 다음과 같이 작성됩니다. `2022-11-05T08:15:30-05:00` 2022년 11월 5일 8에 해당합니다.:15:오전 30시, 미국 동부 표준시. 시간대는 UTC 오프셋으로 제공될 수 있으며 접미사 &quot;Z&quot;(`2020-01-01T01:01:01Z`). 시간대가 제공되지 않으면 기본값은 0입니다. |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **필수** HTML 이스케이프 처리. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 다음과 같습니다. `created`, `templateId`, 및 `userId`. 지원되는 연산자 목록은 다음과 같습니다 `>` (보다 큼), `<` (보다 작음) 및 `==` (와 같음). 예를 들어, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 은 사용자 ID가 지정된 대로 모든 예약된 쿼리를 반환합니다. |

**요청**

다음 요청은 조직에 대해 생성된 가장 최근의 예약된 쿼리를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 조직에 대해 예약된 쿼리 목록과 함께 HTTP 상태 200을 반환합니다. 다음 응답은 조직에 대해 생성된 가장 최근의 예약된 쿼리를 반환합니다.

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### 새 예약된 쿼리 만들기

에 POST 요청을 하여 새 예약된 쿼리를 만들 수 있습니다. `/schedules` 엔드포인트. API에서 예약된 쿼리를 만들면 쿼리 편집기에서도 볼 수 있습니다. UI의 예약된 쿼리에 대한 자세한 내용은 [쿼리 편집기 설명서](../ui/user-guide.md#scheduled-queries).

**API 형식**

```http
POST /schedules
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| 속성 | 설명 |
| -------- | ----------- |
| `query.dbName` | 예약된 쿼리를 만드는 데이터베이스의 이름입니다. |
| `query.sql` | 만들려는 SQL 쿼리입니다. |
| `query.name` | 예약된 쿼리의 이름입니다. |
| `schedule.schedule` | 쿼리에 대한 cron 일정. cron 일정에 대한 자세한 내용은 [cron 표현식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. 이 예에서 &quot;30 * * * *&quot;는 쿼리가 매 시간마다 30분 표시에 실행됨을 의미합니다.<br><br>또는 다음과 같은 축약 표현식을 사용할 수 있습니다.<ul><li>`@once`: 쿼리가 한 번만 실행됩니다.</li><li>`@hourly`: 쿼리가 매시간 시작 시간에 실행됩니다. 이는 cron 표현식과 같습니다 `0 * * * *`.</li><li>`@daily`: 쿼리가 매일 자정에 한 번 실행됩니다. 이는 cron 표현식과 같습니다 `0 0 * * *`.</li><li>`@weekly`: 쿼리가 일주일에 한 번, 일요일 자정에 실행됩니다. 이는 cron 표현식과 같습니다 `0 0 * * 0`.</li><li>`@monthly`: 쿼리가 한 달에 한 번, 그 달의 첫날 자정에 실행됩니다. 이는 cron 표현식과 같습니다 `0 0 1 * *`.</li><li>`@yearly`: 쿼리가 1년에 한 번, 1월 1일 자정에 실행됩니다. 이는 cron 표현식과 같습니다 `1 0 0 1 1 *`. |
| `schedule.startDate` | UTC 타임스탬프로 작성된 예약된 쿼리의 시작 날짜입니다. |

**응답**

성공적인 응답은 새로 생성된 예약된 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 예약된 쿼리의 활성화가 완료되면 `state` 다음에서 변경됨: `REGISTERING` 끝 `ENABLED`.

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.delete` 끝 [생성된 예약된 쿼리 삭제](#delete-a-specified-scheduled-query).

### 지정된 예약된 쿼리의 세부 정보 요청

에 GET 요청을 하여 특정 예약된 쿼리에 대한 정보를 검색할 수 있습니다. `/schedules` 엔드포인트 및 요청 경로에 해당 ID 제공

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` 검색할 예약된 쿼리의 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 예약된 쿼리의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE]
>
>다음 값을 사용할 수 있습니다. `_links.delete` 끝 [생성된 예약된 쿼리 삭제](#delete-a-specified-scheduled-query).

### 지정된 예약된 쿼리의 세부 정보 업데이트

에 PATCH 요청을 하여 지정된 예약된 쿼리에 대한 세부 정보를 업데이트할 수 있습니다. `/schedules` 엔드포인트 및 요청 경로에 해당 ID를 제공

PATCH 요청은 두 개의 서로 다른 경로를 지원합니다. `/state` 및 `/schedule/schedule`.

### 예약된 쿼리 상태 업데이트

다음을 설정하여 선택한 예약된 쿼리의 상태를 업데이트할 수 있습니다. `path` 다음으로 속성: `/state` 및 `value` 다음 중 하나의 속성 `enable` 또는 `disable`.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` PATCH 할 예약된 쿼리의 값입니다. |


**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 쿼리 일정에 대해 수행할 작업입니다. 허용되는 값은 입니다. `replace`. |
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 상태를 업데이트하므로 값을 설정해야 합니다. `path` 끝 `/state`. |
| `value` | 의 업데이트된 값 `/state`. 이 값은 다음으로 설정할 수 있습니다. `enable` 또는 `disable` 예약된 쿼리를 활성화하거나 비활성화합니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 예약된 쿼리 일정 업데이트

다음을 설정하여 예약된 쿼리의 cron 일정을 업데이트할 수 있습니다. `path` 다음으로 속성: `/schedule/schedule` 를 입력합니다. cron 일정에 대한 자세한 내용은 [cron 표현식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` PATCH 할 예약된 쿼리의 값입니다. |

**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 쿼리 일정에 대해 수행할 작업입니다. 허용되는 값은 입니다. `replace`. |
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 일정을 업데이트하므로 값을 설정해야 합니다. `path` 끝 `/schedule/schedule`. |
| `value` | 의 업데이트된 값 `/schedule`. 이 값은 cron schedule 형식이어야 합니다. 따라서 이 예에서는 예약된 쿼리가 매 시간 45분 표시에 실행됩니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 지정된 예약된 쿼리 삭제

에 DELETE 요청을 하여 지정된 예약된 쿼리를 삭제할 수 있습니다. `/schedules` 엔드포인트 및 요청 경로에서 삭제하려는 예약된 쿼리의 ID 제공

>[!NOTE]
>
>일정 **필수** 삭제하기 전에 비활성화하십시오.

**API 형식**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` DELETE 할 예약된 쿼리의 값입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```
