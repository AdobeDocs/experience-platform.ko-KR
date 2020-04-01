---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 쿼리 서비스 개발자 가이드
topic: scheduled queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 예약된 쿼리

## 샘플 API 호출

이제 사용할 헤더를 이해했으므로 쿼리 서비스 API에 대한 호출을 시작할 수 있습니다. 다음 섹션에서는 Query Service API를 사용하여 수행할 수 있는 다양한 API 호출을 살펴봅니다. 각 호출에는 일반 API 형식, 필요한 헤더를 표시하는 샘플 요청 및 샘플 응답이 포함됩니다.

### 예약된 쿼리 목록 검색

IMS 조직에 대해 GET 요청을 `/schedules` 끝점에 만들어 예약된 모든 쿼리 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*선택*&#x200B;사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다. 사용 가능한 매개 변수는 아래에 나열되어 있습니다. |

**쿼리 매개 변수**

다음은 예약된 쿼리를 나열하기 위한 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 예약된 쿼리를 모두 검색합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 주문할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어, `orderby=created` 결과를 오름차순으로 정렬합니다. 만들기 `-` 전(`orderby=-created`)을 추가하면 항목이 내림차순으로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어하기 위해 페이지 크기 제한을 지정합니다. (*Default value: 20*) |
| `start` | 0부터 시작하는 번호 매기기를 사용하여 응답 목록을 오프셋합니다. 예를 들어 세 번째 나열된 쿼리에서 시작하는 목록을 `start=2` 반환합니다. (*Default value: 0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터는 HTML에서 **escape되어야 합니다** . 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `created`, `templateId`및 `userId`입니다. 지원되는 연산자 목록은 `>` (보다 큼), `<` (보다 작음) 및 `==` (같음)입니다. 예를 들어 사용자 ID가 지정된 모든 예약된 쿼리를 `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 반환합니다. |

**요청**

다음 요청은 IMS 조직에 대해 작성된 최신 예약 쿼리를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대한 예약된 쿼리 목록과 함께 HTTP 상태 200을 반환합니다. 다음 응답은 IMS 조직에 대해 작성된 최신 예약 쿼리를 반환합니다.

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

### 예약된 새 쿼리 만들기

종단점에 대한 POST 요청을 만들어 새 예약된 쿼리를 만들 수 `/schedules` 있습니다.

**API 형식**

```http
POST /schedules
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `query.dbName` | 예약된 쿼리를 만들 데이터베이스의 이름입니다. |
| `query.sql` | 만들려는 SQL 쿼리입니다. |
| `query.name` | 예약된 쿼리의 이름입니다. |
| `schedule.schedule` | 쿼리의 cron 일정. cron 예약에 대한 자세한 내용은 cron [식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오. 이 예에서 &quot;30 * * * * * *&quot;는 쿼리가 30분 표시에서 매 시간마다 실행됨을 의미합니다. |
| `schedule.startDate` | UTC 타임스탬프로 작성된 예약된 쿼리의 시작 날짜입니다. |

**응답**

성공적인 응답은 새로 만든 예약된 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 예약된 쿼리가 활성화되면 `state` 에서 `REGISTERING` 로 `ENABLED`변경됩니다.

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

>[!NOTE] 의 값을 `_links.delete` 사용하여 만든 예약된 쿼리를 [삭제할 수 있습니다](#delete-a-specified-scheduled-query).

### 지정된 예약된 쿼리의 요청 세부 사항

종단점에 GET 요청을 만들고 요청 경로에서 해당 ID를 제공하여 특정 예약된 쿼리에 대한 정보를 검색할 수 `/schedules` 있습니다.

**API 형식**

```http
GET /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 예약된 쿼리의 `id` 값입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 예약된 쿼리의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

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

>[!NOTE] 의 값을 `_links.delete` 사용하여 만든 예약된 쿼리를 [삭제할 수 있습니다](#delete-a-specified-scheduled-query).

### 지정된 예약된 쿼리의 세부 정보 업데이트

PATCH 요청을 끝점에 수행하고 요청 경로에서 해당 ID를 제공하여 지정된 예약된 쿼리에 대한 세부 정보를 업데이트할 수 `/schedules` 있습니다.

PATCH 요청은 두 가지 경로를 지원합니다. `/state` 및 `/schedule/schedule`Adobe

### 예약된 쿼리 상태 업데이트

를 사용하여 선택한 예약된 쿼리의 상태(ENABLED 또는 DISABLED)를 업데이트할 `/state` 수 있습니다. 상태를 업데이트하려면 값을 `enable` 또는 으로 설정해야 `disable`합니다.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 예약된 쿼리의 `id` 값입니다. |


**요청**

이 API 요청은 페이로드에 대한 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 상태를 업데이트하므로 의 값을 `path` 다음으로 설정해야 `/state`합니다. |
| `value` | 의 업데이트된 값입니다 `/state`. 이 값은 예약된 쿼리를 활성화하거나 비활성화하도록 `enable` 설정하거나 해제할 `disable` 수 있습니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 예약된 쿼리 일정 업데이트

을 `/schedule/schedule` 사용하여 예약된 쿼리의 cron 예약을 업데이트할 수 있습니다. cron 예약에 대한 자세한 내용은 cron [식 형식](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 예약된 쿼리의 `id` 값입니다. |

**요청**

이 API 요청은 페이로드에 대한 JSON 패치 구문을 사용합니다. JSON 패치의 작동 방식에 대한 자세한 내용은 API 기본 문서를 참조하십시오.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 일정을 업데이트하므로 의 값을 `path` 다음으로 설정해야 합니다 `/schedule/schedule`. |
| `value` | 의 업데이트된 값입니다 `/schedule`. 이 값은 cron 일정 형식이어야 합니다. 따라서 이 예에서 예약된 쿼리는 매 시간마다 45분 표시에서 실행됩니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 지정된 예약된 쿼리 삭제

끝점에 DELETE 요청을 만들고 요청 경로에서 삭제하려는 예약된 쿼리의 ID를 제공하여 지정된 예약된 쿼리를 삭제할 수 있습니다. `/schedules`

>[!NOTE] 삭제하기 전에 예약을 비활성화해야 **합니다** .

**API 형식**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 검색할 예약된 쿼리의 `id` 값입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
