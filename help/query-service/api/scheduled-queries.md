---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;예약된 쿼리;예약된 쿼리
solution: Experience Platform
title: 예약된 쿼리 API 끝점
description: 다음 섹션에서는 Query Service API를 사용하는 예약된 쿼리에 사용할 수 있는 다양한 API 호출을 안내합니다.
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 2%

---

# 예약된 쿼리 끝점

## 샘플 API 호출

이제 사용할 헤더를 이해하므로 을 호출할 준비가 되었습니다. [!DNL Query Service] API. 다음 섹션에서는 를 사용하여 수행할 수 있는 다양한 API 호출을 살펴봅니다 [!DNL Query Service] API. 각 호출에는 일반 API 형식, 필수 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함되어 있습니다.

### 예약된 쿼리 목록 검색

IMS 조직에 대해 GET 요청을 수행하여 예약된 모든 질의 목록을 검색할 수 있습니다 `/schedules` 엔드포인트.

**API 형식**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*선택 사항입니다*) 응답에서 반환된 결과를 구성하는 요청 경로에 매개 변수가 추가되었습니다. 여러 매개 변수를 앰퍼샌드( )로 구분하여 포함할 수 있습니다`&`). 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 예약된 쿼리를 나열할 수 있는 사용 가능한 쿼리 매개 변수 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 종단점을 호출하면 조직에 사용할 수 있는 예약된 쿼리를 모두 검색합니다.

| 매개 변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬할 필드를 지정합니다. 지원되는 필드는 다음과 같습니다 `created` 및 `updated`. 예, `orderby=created` 은(는) 결과를 오름차순으로 정렬하게 됩니다. 추가 `-` 생성 전(`orderby=-created`)은 내림차순으로 만든 항목을 정렬합니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20년*) |
| `start` | 영(0) 기반 번호 지정을 사용하여 응답 목록을 오프셋합니다. 예, `start=2` 세 번째 나열된 쿼리에서 시작하는 목록을 반환합니다. (*기본값: 0*) |
| `property` | 필드를 기반으로 결과를 필터링합니다. 필터 **반드시** HTML 이스케이프 처리됨. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 다음과 같습니다 `created`, `templateId`, 및 `userId`. 지원되는 연산자 목록은 다음과 같습니다 `>` (보다 큼), `<` (보다 작음), 및 `==` (같음). 예, `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 은 사용자 ID가 지정된 대로 예약된 쿼리를 모두 반환합니다. |

**요청**

다음 요청은 IMS 조직에 대해 만들어진 최신 예약된 쿼리를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 IMS 조직에 대해 예약된 쿼리 목록과 함께 HTTP 상태 200을 반환합니다. 다음 응답은 IMS 조직에 대해 작성된 최신 예약된 쿼리를 반환합니다.

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

에 POST 요청을 만들어 예약된 새 쿼리를 만들 수 있습니다 `/schedules` 엔드포인트. API에서 예약된 쿼리를 만들면 쿼리 편집기에서 볼 수도 있습니다. UI의 예약된 쿼리에 대한 자세한 내용은 [쿼리 편집기 설명서](../ui/user-guide.md#scheduled-queries).

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
| `query.dbName` | 예약된 쿼리를 만들 데이터베이스의 이름입니다. |
| `query.sql` | 만들 SQL 쿼리 |
| `query.name` | 예약된 쿼리의 이름입니다. |
| `schedule.schedule` | 쿼리의 크론 일정입니다. 크론 예약에 대한 자세한 내용은 [cron 식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서. 이 예에서 &quot;30 * * * *&quot;는 쿼리가 30분 표시에서 매시간마다 실행됨을 의미합니다.<br><br>또는 다음 축약식을 사용할 수 있습니다.<ul><li>`@once`: 쿼리는 한 번만 실행됩니다.</li><li>`@hourly`: 쿼리는 매시간 시작 시 실행됩니다. 이는 cron 표현식과 같습니다 `0 * * * *`.</li><li>`@daily`: 쿼리는 하루에 한 번 자정에 실행됩니다. 이는 cron 표현식과 같습니다 `0 0 * * *`.</li><li>`@weekly`: 이 쿼리는 매주 한 번, 일요일, 자정에 실행됩니다. 이는 cron 표현식과 같습니다 `0 0 * * 0`.</li><li>`@monthly`: 쿼리는 한 달에 한 번, 그 달의 첫 번째 날, 자정에 실행됩니다. 이는 cron 표현식과 같습니다 `0 0 1 * *`.</li><li>`@yearly`: 이 쿼리는 1월 1일 자정, 1년에 한 번 실행됩니다. 이는 cron 표현식과 같습니다 `1 0 0 1 1 *`. |
| `schedule.startDate` | UTC 타임스탬프로 작성된 예약된 쿼리의 시작 날짜입니다. |

**응답**

성공적인 응답은 새로 만든 예약된 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 예약된 쿼리 활성화가 끝나면 `state` 이(가) `REGISTERING` to `ENABLED`.

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
>다음 값을 사용할 수 있습니다. `_links.delete` to [만든 예약된 쿼리 삭제](#delete-a-specified-scheduled-query).

### 지정된 예약된 쿼리의 요청 세부 정보

에 GET 요청을 수행하여 특정 예약된 쿼리에 대한 정보를 검색할 수 있습니다 `/schedules` 엔드포인트 및 요청 경로에 해당 ID 제공.

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
>다음 값을 사용할 수 있습니다. `_links.delete` to [만든 예약된 쿼리 삭제](#delete-a-specified-scheduled-query).

### 지정된 예약된 쿼리의 세부 정보 업데이트

에 PATCH 요청을 수행하여 지정된 예약된 쿼리의 세부 사항을 업데이트할 수 있습니다 `/schedules` 엔드포인트 및 요청 경로에 해당 ID를 제공하여 채워집니다.

PATCH 요청은 두 개의 서로 다른 경로를 지원합니다. `/state` 및 `/schedule/schedule`.

### 예약된 쿼리 상태 업데이트

다음을 사용할 수 있습니다 `/state` 선택한 예약된 쿼리의 상태를 업데이트하려면(활성화 또는 비활성화) 상태를 업데이트하려면 값을 `enable` 또는 `disable`.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` PATCH 할 예약된 쿼리의 값입니다. |


**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

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
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 상태를 업데이트하므로 값을 설정해야 합니다 `path` to `/state`. |
| `value` | 의 업데이트된 값 `/state`. 이 값은 로 설정할 수 있습니다. `enable` 또는 `disable` 예약된 쿼리를 활성화하거나 비활성화합니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 예약된 쿼리 일정 업데이트

다음을 사용할 수 있습니다 `/schedule/schedule` 예약된 쿼리의 cron 일정을 업데이트하려면 크론 예약에 대한 자세한 내용은 [cron 식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 다음 `id` PATCH 할 예약된 쿼리의 값입니다. |

**요청**

이 API 요청은 페이로드에 JSON 패치 구문을 사용합니다. JSON 패치 작동 방식에 대한 자세한 내용은 API 기본 사항 문서를 참조하십시오.

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
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 일정을 업데이트하므로 값을 설정해야 합니다 `path` to `/schedule/schedule`. |
| `value` | 의 업데이트된 값 `/schedule`. 이 값은 크론 예약의 형식이어야 합니다. 따라서 이 예제에서 예약된 쿼리는 45분 표시에서 매시간마다 실행됩니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 지정된 예약된 쿼리 삭제

에 DELETE 요청을 수행하여 지정된 예약된 쿼리를 삭제할 수 있습니다 `/schedules` 끝점을 제공하고 요청 경로에서 삭제할 예약된 쿼리의 ID를 제공합니다.

>[!NOTE]
>
>예약 **반드시** 삭제하기 전에 비활성화하십시오.

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
