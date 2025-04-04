---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;경고;
title: 경고 구독 끝점
description: 이 안내서는 쿼리 서비스 API를 사용하여 경고 구독 끝점에 대해 수행할 수 있는 다양한 API 호출에 대한 샘플 HTTP 요청 및 응답을 제공합니다.
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3217'
ht-degree: 1%

---

# 경고 구독 끝점

Adobe Experience Platform 쿼리 서비스를 사용하면 애드혹 및 예약된 쿼리 모두에 대한 경고를 구독할 수 있습니다. 경고는 이메일로 받거나 Experience Platform UI 내에서 또는 두 가지 모두로 받을 수 있습니다. 알림 콘텐츠는 Experience Platform 내 경고 및 이메일 경고에 대해 동일합니다.

## 시작하기

이 안내서에 사용된 끝점은 Adobe Experience Platform [쿼리 서비스 API](https://developer.adobe.com/experience-platform-apis/references/query-service/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 필수 헤더와 예제 API 호출을 읽는 방법 등 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

>[!IMPORTANT]
>
>이메일 경고를 수신하려면 먼저 UI 내에서 이 설정을 활성화해야 합니다. [전자 메일 알림을 사용하도록 설정하는 방법에 대한 지침](../../observability/alerts/ui.md#enable-email-alerts)에 대해서는 설명서를 참조하세요.

## 경고 유형 {#alert-types}

아래 표에서는 지원되는 쿼리 경고 유형에 대해 설명합니다.

>[!IMPORTANT]
>
>`delay` 또는 [!UICONTROL 쿼리 실행 지연] 경고 유형은 현재 쿼리 서비스 API에서 지원되지 않습니다. 이 경고는 예약된 쿼리 실행의 결과가 지정된 임계값을 초과하는 지연이 있는 경우 이를 알려줍니다. 이 경고를 사용하려면 해당 기간 동안 쿼리가 완료되거나 실패하지 않고 실행될 때 경고를 트리거하는 사용자 지정 시간을 설정해야 합니다. UI에서 이 경고를 설정하는 방법에 대해 알아보려면 [쿼리 일정](../ui/query-schedules.md#alerts-for-query-status) 설명서 또는 [인라인 쿼리 작업에 대한 안내서](../ui/monitor-queries.md#query-run-delay)를 참조하세요.

| 경고 유형 | 설명 |
|---|---|
| `start` | 이 경고는 예약된 쿼리 실행이 시작되거나 처리를 시작할 때 알려줍니다. |
| `success` | 이 경고는 예약된 쿼리 실행이 성공적으로 완료되면 사용자에게 알려 주며 이는 쿼리가 오류 없이 실행되었음을 나타냅니다. |
| `failed` | 이 경고는 예약된 쿼리 실행에 오류가 발생하거나 성공적으로 실행되지 않을 때 트리거됩니다. 문제를 신속하게 식별하고 해결하는 데 도움이 됩니다. |
| `quarantine` | 이 경고는 예약된 쿼리 실행이 격리된 상태로 전환되면 활성화됩니다. 쿼리가 격리 기능에 등록되면 10번의 연속 실행에 실패한 모든 예약된 쿼리는 자동으로 [!UICONTROL 격리됨] 상태가 됩니다. 그런 다음 추가 실행이 수행되기 전에 사용자의 개입이 필요합니다. |

>[!NOTE]
>
>모든 SELECT가 아닌 쿼리는 경고 구독을 지원하며, 경고를 구독하기 위해 쿼리 작성자가 될 필요가 없습니다. 다른 사용자는 자신이 만들지 않은 쿼리에 대한 경고를 등록할 수도 있습니다.

다음 경고는 경고 구독 없이 적용됩니다.

* 일괄 처리 쿼리 작업이 완료되면 사용자에게 알림이 전송됩니다.
* 일괄 처리 쿼리 작업의 기간이 임계값을 초과하면 쿼리를 예약한 사용자에게 경고가 트리거됩니다.

>[!NOTE]
>
>테스트에 사용되는 쿼리는 적절하게 구성된 경우 이러한 경고에서 제외할 수 있습니다.

## 샘플 API 호출

다음 섹션에서는 쿼리 서비스 API를 사용하여 수행할 수 있는 다양한 API 호출을 살펴봅니다. 각 호출에는 일반 API 형식, 필요한 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함됩니다.

## 조직 및 샌드박스에 대한 모든 경고 목록 검색 {#get-list-of-org-alert-subs}

`/alert-subscriptions` 끝점에 대한 GET 요청을 만들어 조직 샌드박스에 대한 모든 경고 목록을 검색합니다.

**API 형식**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| 속성 | 설명 |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | (선택 사항) 응답에서 반환된 결과를 구성하는 요청 경로에 추가된 매개 변수입니다. 여러 매개 변수를 포함할 수 있으며 앰퍼샌드(&amp;)로 구분합니다. 사용 가능한 매개 변수는 아래에 나와 있습니다. |

**쿼리 매개 변수**

다음은 쿼리를 나열하는 데 사용할 수 있는 쿼리 매개 변수의 목록입니다. 이러한 매개 변수는 모두 선택 사항입니다. 매개 변수 없이 이 끝점을 호출하면 조직에서 사용할 수 있는 모든 쿼리를 검색합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `orderby` | 결과 순서를 지정하는 필드입니다. 지원되는 필드는 `created` 및 `updated`입니다. 속성 이름 앞에 오름차순 `+`, 내림차순 `-`을(를) 추가합니다. 기본값은 `-created`입니다. 더하기 기호(`+`)는 `%2B`(으)로 이스케이프해야 합니다. 예를 들어 `%2Bcreated`은(는) 오름차순 생성 순서에 대한 값입니다. |
| `pagesize` | 이 매개 변수를 사용하여 페이지당 API 호출에서 가져올 레코드 수를 제어합니다. 기본 제한은 페이지당 최대 50개의 레코드 수로 설정됩니다. |
| `page` | 레코드를 보려는 반환된 결과의 페이지 번호를 나타냅니다. |
| `property` | 선택한 필드를 기반으로 결과를 필터링합니다. **must** 필터는 HTML 이스케이프되어야 합니다. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 다음 속성을 사용하여 필터링할 수 있습니다. <ul><li>ID</li><li>assetId</li><li>상태</li><li>alertType</li></ul> 지원되는 연산자는 `==`(과 같음)입니다. 예를 들어 `id==6ebd9c2d-494d-425a-aa91-24033f3abeec`은(는) ID가 일치하는 경고를 반환합니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**응답**

성공적인 응답은 페이지 매김 및 버전 정보가 있는 HTTP 200 상태 및 `alerts` 배열을 반환합니다. `alerts` 배열에는 조직 및 특정 샌드박스에 대한 모든 경고에 대한 세부 정보가 포함되어 있습니다. 응답당 최대 3개의 경고를 사용할 수 있으며 각 경고 유형당 하나의 경고가 응답 본문에 포함됩니다.

>[!NOTE]
>
>간결성을 위해 `alerts` 배열의 `alerts._links` 개체가 잘렸습니다. `alerts._links` 개체의 전체 예제는 POST 요청의 [응답](#subscribe-users)에서 찾을 수 있습니다.

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `alerts.assetId` | 경고를 특정 쿼리와 연결한 쿼리 ID입니다. |
| `alerts.id` | 경고의 이름입니다. 이 이름은 경고 서비스에서 생성되며 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType` 및 흐름 ID로 구성됩니다. 사용 가능한 경고에 대한 정보는 [Experience Platform 경고 대시보드 설명서](../../observability/alerts/ui.md)에서 찾을 수 있습니다. |
| `alerts.status` | 경고에는 `enabled`, `enabling`, `disabled` 및 `disabling`의 네 가지 상태 값이 있습니다. 경고는 관련 모든 구독자 및 설정을 유지하면서 나중에 사용할 수 있도록 일시 중지되었거나, 이러한 상태 간에 전환되면서 이벤트를 적극적으로 수신하고 있습니다. |
| `alerts.alertType` | 경고 유형. 임시 쿼리에 사용할 수 있는 경고 상태는 4개이지만 예약된 쿼리에 사용할 수 있는 경고 상태는 5개입니다. `quarantine` 경고는 예약된 쿼리에만 사용할 수 있습니다. 또한 Experience Platform UI에서는 `delay` 경고만 설정할 수 있습니다. 이러한 이유로 `delay`은(는) 여기에 설명되어 있지 않습니다. 사용 가능한 경고는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li><li>`quarantine`: 예약된 쿼리 실행이 격리된 상태가 되면 활성화됩니다.</li></ul> |
| `alerts._links` | 이 경고 ID와 관련된 정보를 검색, 업데이트, 편집 또는 삭제하는 데 사용할 수 있는 사용 가능한 메서드 및 끝점에 대한 정보를 제공합니다. |
| `_page` | 개체에는 순서, 크기, 총 페이지 수 및 현재 페이지를 설명하는 속성이 포함되어 있습니다. |
| `_links` | 개체에는 리소스의 다음 또는 이전 페이지를 가져오는 데 사용할 수 있는 URI 참조가 포함되어 있습니다. |

## 특정 쿼리 또는 예약 ID에 대한 경고 구독 정보를 검색합니다 {#retrieve-all-alert-subscriptions-by-id}

`/alert-subscriptions/{QUERY_ID}` 또는 `/alert-subscriptions/{SCHEDULE_ID}` 끝점에 대한 GET 요청을 수행하여 특정 쿼리 ID 또는 일정 ID에 대한 경고 구독 정보를 검색합니다.

**API 형식**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 구독 정보를 반환하려는 쿼리의 ID입니다. |
| `{SCHEDULE_ID}` | 구독 정보를 반환하려는 예약된 쿼리의 ID입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**응답**

성공한 응답은 제공된 쿼리 또는 일정 ID에 대한 구독 정보를 포함하는 `alerts` 배열 및 200의 HTTP 상태를 반환합니다.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `assetId` | 경고는 이 ID와 연결됩니다. ID는 쿼리 ID 또는 예약 ID일 수 있습니다. |
| `id` | 경고의 이름입니다. 이 이름은 경고 서비스에서 생성되며 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType` 및 흐름 ID로 구성됩니다. 사용 가능한 경고에 대한 정보는 [Experience Platform 경고 대시보드 설명서](../../observability/alerts/ui.md)에서 찾을 수 있습니다. |
| `status` | 경고에는 `enabled`, `enabling`, `disabled` 및 `disabling`의 네 가지 상태 값이 있습니다. 경고는 관련 모든 구독자 및 설정을 유지하면서 나중에 사용할 수 있도록 일시 중지되었거나, 이러한 상태 간에 전환되면서 이벤트를 적극적으로 수신하고 있습니다. |
| `alertType` | 각 경고에는 세 가지 서로 다른 경고 유형이 있을 수 있습니다. 이는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `subscriptions.emailNotifications` | 경고에 대한 이메일을 수신하도록 구독한 사용자를 위해 Adobe에 등록된 이메일 주소 배열입니다. |
| `subscriptions.inContextNotifications` | 경고에 대한 UI 알림을 구독한 사용자를 위한 Adobe 등록 이메일 주소 배열입니다. |

## 특정 쿼리 또는 일정 ID 및 경고 유형에 대한 경고 구독 정보를 검색합니다 {#get-alert-info-by-id-and-alert-type}

`/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 끝점에 대한 GET 요청을 수행하여 특정 ID 및 경고 유형에 대한 경고 구독 정보를 검색합니다. 이는 쿼리 또는 예약된 쿼리 ID 모두에 적용할 수 있습니다.

**API 형식**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `ALERT_TYPE` | 이 속성은 경고를 트리거하는 쿼리 실행 상태를 설명합니다. 응답에는 이 유형의 경고에 대한 경고 구독 정보만 포함됩니다. 각 경고에는 세 가지 서로 다른 경고 유형이 있을 수 있습니다. 이는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `QUERY_ID` | 업데이트할 쿼리의 고유 식별자입니다. |
| `SCHEDULE_ID` | 업데이트할 예약된 쿼리의 고유 식별자입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**응답**

성공적인 응답은 HTTP 상태 200과 구독한 모든 경고를 반환합니다. 여기에는 경고 ID, 경고 유형, 구독자의 Adobe 등록 이메일 ID 및 기본 알림 채널이 포함됩니다.

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `assetId` | 경고를 특정 쿼리와 연결한 쿼리 ID입니다. |
| `alertType` | 경고 유형. 임시 쿼리에 사용할 수 있는 경고 상태는 4개이지만 예약된 쿼리에 사용할 수 있는 경고 상태는 5개입니다. `quarantine` 경고는 예약된 쿼리에만 사용할 수 있습니다. 또한 Experience Platform UI에서는 `delay` 경고만 설정할 수 있습니다. 이러한 이유로 `delay`은(는) 여기에 설명되어 있지 않습니다. 사용 가능한 경고는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li><li>`quarantine`: 예약된 쿼리 실행이 격리된 상태가 되면 활성화됩니다.</li></ul> |
| `subscriptions` | 경고와 연관된 Adobe 등록 이메일 ID 및 사용자가 경고를 수신할 채널을 전달하는 데 사용되는 객체입니다. |
| `subscriptions.inContextNotifications` | 경고에 대한 UI 알림을 구독한 사용자를 위한 Adobe 등록 이메일 주소 배열입니다. |
| `subscriptions.emailNotifications` | 경고에 대한 이메일을 수신하도록 구독한 사용자를 위해 Adobe에 등록된 이메일 주소 배열입니다. |

## 사용자가 구독 중인 모든 경고 목록 검색 {#get-alert-subscription-list}

`/alert-subscriptions/user-subscriptions/{EMAIL_ID}` 끝점에 대한 GET 요청을 통해 사용자가 구독하는 모든 경고 목록을 검색합니다. 응답에는 경고 이름, ID, 상태, 경고 유형 및 알림 채널이 포함됩니다.

**API 형식**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{EMAIL_ID}` | Adobe 계정에 등록된 이메일 주소는 경고에 구독한 사용자를 식별하는 데 사용됩니다. |
| `orderby` | 결과 순서를 지정하는 필드입니다. 지원되는 필드는 `created` 및 `updated`입니다. 속성 이름 앞에 오름차순 `+`, 내림차순 `-`을(를) 추가합니다. 기본값은 `-created`입니다. 더하기 기호(`+`)는 `%2B`(으)로 이스케이프해야 합니다. 예를 들어 `%2Bcreated`은(는) 오름차순 생성 순서에 대한 값입니다. |
| `pagesize` | 이 매개 변수를 사용하여 페이지당 API 호출에서 가져올 레코드 수를 제어합니다. 기본 제한은 페이지당 최대 50개의 레코드 수로 설정됩니다. |
| `page` | 레코드를 보려는 반환된 결과의 페이지 번호를 나타냅니다. |
| `property` | 선택한 필드를 기반으로 결과를 필터링합니다. **must** 필터는 HTML 이스케이프되어야 합니다. 쉼표는 여러 필터 세트를 결합하는 데 사용됩니다. 다음 속성을 사용하여 필터링할 수 있습니다. <ul><li>ID</li><li>assetId</li><li>상태</li><li>alertType</li></ul> 지원되는 연산자는 `==`(과 같음)입니다. 예를 들어 `id==6ebd9c2d-494d-425a-aa91-24033f3abeec`은(는) ID가 일치하는 경고를 반환합니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**응답**

성공한 응답은 제공된 `emailId`이(가) 구독한 경고의 세부 정보와 함께 HTTP 상태 200 및 `items` 배열을 반환합니다.

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 경고의 이름입니다. 이 이름은 경고 서비스에서 생성되며 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType` 및 흐름 ID로 구성됩니다. 사용 가능한 경고에 대한 정보는 [Experience Platform 경고 대시보드 설명서](../../observability/alerts/ui.md)에서 찾을 수 있습니다. |
| `assetId` | 경고를 특정 쿼리와 연결한 쿼리 ID입니다. |
| `status` | 경고에는 `enabled`, `enabling`, `disabled` 및 `disabling`의 네 가지 상태 값이 있습니다. 경고는 관련 모든 구독자 및 설정을 유지하면서 나중에 사용할 수 있도록 일시 중지되었거나, 이러한 상태 간에 전환되면서 이벤트를 적극적으로 수신하고 있습니다. |
| `alertType` | 경고 유형. 임시 쿼리에 사용할 수 있는 경고 상태는 4개이지만 예약된 쿼리에 사용할 수 있는 경고 상태는 5개입니다. `quarantine` 경고는 예약된 쿼리에만 사용할 수 있습니다. 또한 Experience Platform UI에서는 `delay` 경고만 설정할 수 있습니다. 이러한 이유로 `delay`은(는) 여기에 설명되어 있지 않습니다. 사용 가능한 경고는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li><li>`quarantine`: 예약된 쿼리 실행이 격리된 상태가 되면 활성화됩니다.</li></ul> |
| `subscriptions` | 경고와 연관된 Adobe 등록 이메일 ID 및 사용자가 경고를 수신할 채널을 전달하는 데 사용되는 객체입니다. |
| `subscriptions.inContextNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. `true` 값은 UI를 통해 경고를 제공해야 함을 확인합니다. `false` 값을 사용하면 해당 채널을 통해 사용자에게 알림이 전송되지 않습니다. |
| `subscriptions.emailNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. `true` 값은 경고가 이메일로 제공되어야 함을 확인합니다. `false` 값을 사용하면 해당 채널을 통해 사용자에게 알림이 전송되지 않습니다. |

## 경고 만들기 및 사용자 구독 {#subscribe-users}

경고를 만들고 사용자를 구독하여 수신하려면 `/alert-subscriptions` 끝점에 대해 `POST` 요청을 만듭니다. 이 요청은 `assetId` 속성을 사용하여 쿼리를 새로 만든 경고에 연결하고 `emailIds`을(를) 사용하여 해당 쿼리에 대한 경고에 사용자를 구독합니다.

>[!IMPORTANT]
>
>단일 요청에서 최대 5개의 Adobe 등록 이메일 ID를 전달할 수 있습니다. 경고에 5명 이상의 사용자를 구독하려면 후속 요청을 수행해야 합니다.

**API 형식**

```http
POST /alert-subscriptions
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `assetId` | 경고는 이 ID와 연결됩니다. ID는 쿼리 ID 또는 예약 ID일 수 있습니다. |
| `alertType` | 경고 유형. 임시 쿼리에 사용할 수 있는 경고 상태는 4개이지만 예약된 쿼리에 사용할 수 있는 경고 상태는 5개입니다. `quarantine` 경고는 예약된 쿼리에만 사용할 수 있습니다. 또한 Experience Platform UI에서는 `delay` 경고만 설정할 수 있습니다. 이러한 이유로 `delay`은(는) 여기에 설명되어 있지 않습니다. 사용 가능한 경고는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li><li>`quarantine`: 예약된 쿼리 실행이 격리된 상태가 되면 활성화됩니다.</li></ul> |
| `subscriptions` | 경고와 연관된 Adobe 등록 이메일 ID 및 사용자가 경고를 수신할 채널을 전달하는 데 사용되는 객체입니다. |
| `subscriptions.emailIds` | 경고를 수신해야 하는 사용자를 식별하는 이메일 주소 배열. 전자 메일 주소 **must**&#x200B;을(를) Adobe 계정에 등록해야 합니다. |
| `subscriptions.inContextNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. `true` 값은 UI를 통해 경고를 제공해야 함을 확인합니다. `false` 값을 사용하면 해당 채널을 통해 사용자에게 알림이 전송되지 않습니다. |
| `subscriptions.emailNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. `true` 값은 경고가 이메일로 제공되어야 함을 확인합니다. `false` 값을 사용하면 해당 채널을 통해 사용자에게 알림이 전송되지 않습니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 생성된 경고의 세부 사항과 함께 HTTP 상태 202(허용됨)를 반환합니다.

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 경고의 이름입니다. 이 이름은 경고 서비스에서 생성되며 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType` 및 흐름 ID로 구성됩니다. 사용 가능한 경고에 대한 정보는 [Experience Platform 경고 대시보드 설명서](../../observability/alerts/ui.md)에서 찾을 수 있습니다. |
| `_links` | 이 경고 ID와 관련된 정보를 검색, 업데이트, 편집 또는 삭제하는 데 사용할 수 있는 사용 가능한 메서드 및 끝점에 대한 정보를 제공합니다. |

## 경고 활성화 또는 비활성화 {#enable-or-disable-alert}

이 요청은 쿼리 또는 일정 ID와 경고 유형을 사용하여 특정 경고를 참조하고 경고 상태를 `enable` 또는 `disable`(으)로 업데이트합니다. `/alert-subscriptions/{queryId}/{alertType}` 또는 `/alert-subscriptions/{scheduleId}/{alertType}` 끝점에 대해 `PATCH` 요청을 수행하여 경고 상태를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `ALERT_TYPE` | 경고 유형. 임시 쿼리에 사용할 수 있는 경고 상태는 4개이지만 예약된 쿼리에 사용할 수 있는 경고 상태는 5개입니다. `quarantine` 경고는 예약된 쿼리에만 사용할 수 있습니다. 또한 Experience Platform UI에서는 `delay` 경고만 설정할 수 있습니다. 이러한 이유로 `delay`은(는) 여기에 설명되어 있지 않습니다. 사용 가능한 경고는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li><li>`quarantine`: 예약된 쿼리 실행이 격리된 상태가 되면 활성화됩니다.</li></ul>변경하려면 끝점 네임스페이스에 현재 경고 유형을 지정해야 합니다. |
| `QUERY_ID` | 업데이트할 쿼리의 고유 식별자입니다. |
| `SCHEDULE_ID` | 업데이트할 예약된 쿼리의 고유 식별자입니다. |

**요청**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `op` | 수행할 작업입니다. 현재 허용되는 값은 `replace`뿐입니다. |
| `path` | 이 값은 끝점의 네임스페이스와 관련이 있습니다. 현재 허용되는 값은 `/status`뿐입니다. |
| `value` | 성공적인 PATCH 요청에서 경고의 `status` 값이 변경됩니다. 현재 허용되는 값은 `enable` 또는 `disable`입니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 경고 상태, 유형, ID와 관련된 쿼리에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 경고의 이름입니다. 이 이름은 경고 서비스에서 생성되며 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType` 및 흐름 ID로 구성됩니다. 사용 가능한 경고에 대한 정보는 [Experience Platform 경고 대시보드 설명서](../../observability/alerts/ui.md)에서 찾을 수 있습니다. |
| `assetId` | 경고는 이 ID와 연결됩니다. ID는 쿼리 ID 또는 예약 ID일 수 있습니다. |
| `alertType` | 각 경고에는 세 가지 서로 다른 경고 유형이 있을 수 있습니다. 이는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `status` | 경고에는 `enabled`, `enabling`, `disabled` 및 `disabling`의 네 가지 상태 값이 있습니다. 경고는 관련 모든 구독자 및 설정을 유지하면서 나중에 사용할 수 있도록 일시 중지되었거나, 이러한 상태 간에 전환되면서 이벤트를 적극적으로 수신하고 있습니다. |

## 특정 쿼리 및 경고 유형에 대한 경고 삭제 {#delete-alert-info-by-id-and-alert-type}

`/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 또는 `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` 끝점에 대한 DELETE 요청을 수행하여 특정 쿼리 또는 일정 ID 및 경고 유형에 대한 경고를 삭제합니다.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `ALERT_TYPE` | 경고 유형. 임시 쿼리에 사용할 수 있는 경고 상태는 4개이지만 예약된 쿼리에 사용할 수 있는 경고 상태는 5개입니다. `quarantine` 경고는 예약된 쿼리에만 사용할 수 있습니다. 또한 Experience Platform UI에서는 `delay` 경고만 설정할 수 있습니다. 이러한 이유로 `delay`은(는) 여기에 설명되어 있지 않습니다. 사용 가능한 경고는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li><li>`quarantine`: 예약된 쿼리 실행이 격리된 상태가 되면 활성화됩니다.</li></ul> DELETE 요청은 제공된 특정 경고 유형에만 적용됩니다. |
| `QUERY_ID` | 업데이트할 쿼리의 고유 식별자입니다. |
| `SCHEDULE_ID` | 업데이트할 예약된 쿼리의 고유 식별자입니다. |

**요청**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**응답**

성공적인 응답은 HTTP 200 상태와 삭제된 경고의 자산 ID 및 경고 유형을 포함하는 확인 메시지를 반환합니다.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## 다음 단계

이 안내서에서는 쿼리 서비스 API에서 `/alert-subscriptions` 끝점을 사용하는 방법에 대해 다룹니다. 이 안내서를 읽은 후에는 쿼리에 대한 경고를 만들고, 경고에 사용자를 구독하는 방법, 사용 가능한 경고 유형 및 경고 구독 정보를 검색, 업데이트 및 삭제하는 방법을 더 잘 이해할 수 있습니다.

사용 가능한 다른 기능 및 작업에 대한 자세한 내용은 [쿼리 서비스 API 안내서](./getting-started.md)를 참조하세요.
