---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;예약된 쿼리;예약된 쿼리;
solution: Experience Platform
title: 일정 끝점
description: 다음 섹션에서는 쿼리 서비스 API를 사용하여 예약된 쿼리에 대해 수행할 수 있는 다양한 API 호출을 안내합니다.
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 10c0c5c639226879b1ca25391fc4a1006cf40003
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 2%

---

# 일정 끝점

자세한 정보 및 예제를 사용하여 쿼리 서비스 예약 API를 사용하여 프로그래밍 방식으로 예약된 쿼리를 만들고, 관리하고, 모니터링하는 방법에 대해 알아봅니다.

## 요구 사항 및 사전 요구 사항

기술 계정(OAuth 서버 간 자격 증명을 통해 인증됨) 또는 개인 사용자 계정(사용자 토큰)을 사용하여 예약된 쿼리를 만들 수 있습니다. 그러나 Adobe에서는 특히 장기 또는 프로덕션 워크로드에 대해 예약된 쿼리를 중단 없이 안전하게 실행할 수 있도록 기술 계정을 사용하는 것이 좋습니다.

개인 사용자 계정으로 만든 쿼리는 해당 사용자의 액세스가 취소되거나 계정이 비활성화된 경우 실패합니다. 기술 계정은 개별 사용자의 고용 상태나 액세스 권한에 연결되지 않으므로 보다 큰 안정성을 제공합니다.

>[!IMPORTANT]
>
>예약된 쿼리를 관리할 때 고려해야 할 중요한 사항:<ul><li>예약된 쿼리를 만드는 데 사용된 계정(기술 또는 사용자)에 액세스나 권한이 없으면 예약된 쿼리가 실패합니다.</li><li>API 또는 UI를 통해 삭제하기 전에 예약된 쿼리를 비활성화해야 합니다.</li><li>종료 날짜 없이 무기한 예약은 지원되지 않습니다. 종료 날짜는 항상 지정해야 합니다.</li></ul>

계정 요구 사항, 권한 설정 및 예약된 쿼리 관리에 대한 자세한 지침은 [쿼리 일정 설명서](../ui/query-schedules.md#technical-account-user-requirements)를 참조하세요. 기술 계정 만들기 및 구성에 대한 단계별 지침은 [Developer Console 설정](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman) 및 [전체 기술 계정 설정](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup)을 참조하세요.

## 샘플 API 호출

필요한 인증 헤더를 구성했으면([API 인증 안내서](../../landing/api-authentication.md) 참조) [!DNL Query Service] API를 호출할 수 있습니다. 다음 섹션에서는 일반 형식, 필수 헤더를 포함한 요청 예 및 샘플 응답을 사용하는 다양한 API 호출을 보여줍니다.

### 예약된 쿼리 목록 검색

`/schedules` 끝점에 대한 GET 요청을 통해 조직에 대해 예약된 모든 쿼리 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*선택 사항*) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(`&`)로 구분됩니다. 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 예약된 쿼리를 나열하기 위해 사용할 수 있는 쿼리 매개 변수의 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 예약된 쿼리를 검색합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과를 정렬하는 데 사용할 필드를 지정합니다. 지원되는 필드는 `created` 및 `updated`입니다. 예를 들어 `orderby=created`은(는) 만들어진 항목별로 오름차순으로 결과를 정렬합니다. 만들기 전에 `-`을(를) 추가하면(`orderby=-created`) 내림차순으로 만들어진 항목별로 정렬됩니다. |
| `limit` | 페이지에 포함된 결과 수를 제어할 페이지 크기 제한을 지정합니다. (*기본값: 20*) |
| `start` | ISO 형식 타임스탬프를 지정하여 결과 순서를 지정합니다. 시작 날짜가 지정되지 않은 경우 API 호출은 가장 오래 전에 생성된 예약 쿼리를 먼저 반환한 다음 더 최근 결과를 계속 나열합니다.<br> ISO 타임스탬프를 사용하면 날짜 및 시간에 서로 다른 수준의 세부기간을 사용할 수 있습니다. 기본 ISO 타임스탬프는 `2020-09-07` 형식을 사용하여 2020년 9월 7일의 날짜를 나타냅니다. 보다 복잡한 예제는 `2022-11-05T08:15:30-05:00`(으)로 작성되며 2022년 11월 5일 오전 8:15:30(미국 동부 표준시)에 해당합니다. 시간대는 UTC 오프셋을 사용하여 제공될 수 있으며 접미사 &quot;Z&quot;(`2020-01-01T01:01:01Z`)로 표시됩니다. 시간대가 제공되지 않으면 기본값은 0입니다. |
| `property` | 필드를 기반으로 결과를 필터링합니다. **must** 필터는 HTML 이스케이프되어야 합니다. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 지원되는 필드는 `created`, `templateId` 및 `userId`입니다. 지원되는 연산자 목록은 `>`(보다 큼), `<`(보다 작음) 및 `==`(과 같음)입니다. 예를 들어 `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec`은(는) 사용자 ID가 지정된 대로 지정된 모든 예약된 쿼리를 반환합니다. |

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

`/schedules` 끝점에 대한 POST 요청을 수행하여 새 예약된 쿼리를 만들 수 있습니다. API에서 예약된 쿼리를 만들면 쿼리 편집기에서도 볼 수 있습니다. UI의 예약된 쿼리에 대한 자세한 내용은 [쿼리 편집기 설명서](../ui/user-guide.md#scheduled-queries)를 참조하십시오.

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
| `query.dbName` | 예약된 쿼리가 실행될 데이터베이스의 이름입니다. |
| `query.sql` | 정의된 일정에 따라 실행할 SQL 쿼리입니다. |
| `query.name` | 예약된 쿼리의 이름입니다. |
| `query.description` | 예약된 쿼리에 대한 선택적 설명입니다. |
| `schedule.schedule` | 쿼리에 대한 cron 일정. cron 표현식을 만들고, 확인하고, 이해하는 대화형 방법은 [Crontab.guru](https://crontab.guru/)을 참조하세요. 이 예에서 &quot;30 * * * *&quot;는 쿼리가 매 시간마다 30분 표시에 실행됨을 의미합니다.<br><br>또는 다음 축약 표현식을 사용할 수 있습니다.<ul><li>`@once`: 쿼리가 한 번만 실행됩니다.</li><li>`@hourly`: 쿼리가 매시간 시작 시간에 실행됩니다. 크론 식 `0 * * * *`과(와) 같습니다.</li><li>`@daily`: 쿼리가 매일 자정에 한 번 실행됩니다. 크론 식 `0 0 * * *`과(와) 같습니다.</li><li>`@weekly`: 쿼리가 일주일에 한 번, 일요일 자정에 실행됩니다. 크론 식 `0 0 * * 0`과(와) 같습니다.</li><li>`@monthly`: 쿼리가 한 달에 한 번, 그 달의 첫째 날 자정에 실행됩니다. 크론 식 `0 0 1 * *`과(와) 같습니다.</li><li>`@yearly`: 쿼리가 1년에 한 번 1월 1일 자정에 실행됩니다. 크론 식 `0 0 1 1 *`과(와) 같습니다. |
| `schedule.startDate` | UTC 타임스탬프로 작성된 예약된 쿼리의 시작 날짜입니다. |

**응답**

성공적인 응답은 새로 생성된 예약된 쿼리의 세부 정보와 함께 HTTP 상태 202(허용됨)를 반환합니다. 예약된 쿼리가 활성화되면 `state`이(가) `REGISTERING`에서 `ENABLED`(으)로 변경됩니다.

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
>`_links.delete`의 값을 사용하여 [만들어진 예약된 쿼리를 삭제](#delete-a-specified-scheduled-query)할 수 있습니다.

### 지정된 예약된 쿼리의 세부 정보 요청

`/schedules` 끝점에 대한 GET 요청을 만들고 요청 경로에 해당 ID를 제공하여 특정 예약된 쿼리에 대한 정보를 검색할 수 있습니다.

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
>`_links.delete`의 값을 사용하여 [만들어진 예약된 쿼리를 삭제](#delete-a-specified-scheduled-query)할 수 있습니다.

### 지정된 예약된 쿼리의 세부 정보 업데이트

`/schedules` 끝점에 대한 PATCH 요청을 만들고 요청 경로에 해당 ID를 제공하여 지정된 예약된 쿼리에 대한 세부 정보를 업데이트할 수 있습니다.

PATCH 요청은 두 개의 다른 경로(`/state` 및 `/schedule/schedule`)를 지원합니다.

### 예약된 쿼리 상태 업데이트

`path` 속성을 `/state`(으)로 설정하고 `value` 속성을 `enable` 또는 `disable`(으)로 설정하여 선택한 예약된 쿼리의 상태를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | PATCH에 추가할 예약된 쿼리의 `id` 값입니다. |


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
| `op` | 쿼리 일정에 대해 수행할 작업입니다. 허용되는 값은 `replace`입니다. |
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 상태를 업데이트하는 중이므로 `path`의 값을 `/state`(으)로 설정해야 합니다. |
| `value` | `/state`의 업데이트된 값. 이 값은 `enable` 또는 `disable`(으)로 설정하여 예약된 쿼리를 활성화하거나 비활성화할 수 있습니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 예약된 쿼리 일정 업데이트

요청 본문에서 `path` 속성을 `/schedule/schedule`(으)로 설정하여 예약된 쿼리의 cron 일정을 업데이트할 수 있습니다. cron 일정에 대한 자세한 내용은 [cron 식 형식](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 설명서를 참조하십시오.

**API 형식**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | PATCH에 추가할 예약된 쿼리의 `id` 값입니다. |

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
| `op` | 쿼리 일정에 대해 수행할 작업입니다. 허용되는 값은 `replace`입니다. |
| `path` | 패치할 값의 경로입니다. 이 경우 예약된 쿼리의 일정을 업데이트하고 있으므로 `path`의 값을 `/schedule/schedule`(으)로 설정해야 합니다. |
| `value` | `/schedule`의 업데이트된 값. 이 값은 cron schedule 형식이어야 합니다. 따라서 이 예에서는 예약된 쿼리가 매 시간 45분 표시에 실행됩니다. |

**응답**

성공적인 응답은 다음 메시지와 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 지정된 예약된 쿼리 삭제

`/schedules` 끝점에 DELETE을 요청하고 요청 경로에 삭제할 예약된 쿼리의 ID를 제공하여 지정된 예약된 쿼리를 삭제할 수 있습니다.

>[!NOTE]
>
>삭제하기 전에 일정 **must**&#x200B;을(를) 사용하지 않도록 설정해야 합니다.

**API 형식**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | DELETE에 추가할 예약된 쿼리의 `id` 값입니다. |

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
