---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;경고
title: 경고 구독 API 끝점
description: 이 안내서에서는 Query Service API를 사용하여 경고 구독 종단점에 대해 수행할 수 있는 다양한 API 호출에 대한 샘플 HTTP 요청 및 응답을 제공합니다.
hide: true
hidefromtoc: true
source-git-commit: df894d8b52aff3708aa06e73d4c5ba3e1e501f10
workflow-type: tm+mt
source-wordcount: '2289'
ht-degree: 2%

---

# 경고 구독 API 끝점

Adobe Experience Platform Query Service를 사용하면 애드혹 쿼리 및 예약된 쿼리 모두에 대한 경고를 구독할 수 있습니다. 경고는 이메일, Platform UI 또는 두 가지 모두로 수신할 수 있습니다. 알림 콘텐츠는 인플랫폼 경고 및 이메일 경고와 동일합니다. 현재 쿼리 경고는 [쿼리 서비스 API](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>이메일 경고를 수신하려면 먼저 UI 내에서 이 설정을 활성화해야 합니다. 다음 문서를 참조하십시오. [이메일 경고를 활성화하는 방법에 대한 지침](../../observability/alerts/ui.md#enable-email-alerts).

아래 표에서는 다양한 유형의 쿼리에 대해 지원되는 경고 유형에 대해 설명합니다.

| 쿼리 유형 | 지원되는 경고 유형 |
|---|---|
| 애드혹 쿼리 | `success` 또는 `failed` 실행. |
| 예약된 쿼리 | `start`, `success`, 또는 `failed` 실행. |

>[!NOTE]
>
>SELECT가 아닌 모든 쿼리는 경고 가입을 지원하며, 경고를 구독하기 위해 쿼리 작성자가 될 필요가 없습니다. 다른 사용자는 만들지 않은 쿼리에 경고를 등록할 수도 있습니다.

다음 경고는 경고 구독 없이 적용됩니다.

* 배치 쿼리 작업이 완료되면 사용자가 알림을 받습니다.
* 배치 질의 작업의 기간이 임계값을 초과하는 경우 쿼리를 예약한 사람에게 경고가 트리거됩니다.

>[!NOTE]
>
>테스트에 사용되는 쿼리는 적절하게 구성된 경우 이러한 경고에서 제외할 수 있습니다.

## 샘플 API 호출

다음 섹션에서는 Query Service API를 사용하여 수행할 수 있는 다양한 API 호출을 살펴봅니다. 각 호출에는 일반 API 형식, 필수 헤더를 보여주는 샘플 요청 및 샘플 응답이 포함되어 있습니다.

## 조직 및 샌드박스에 대한 모든 경고 목록 검색 {#get-list-of-org-alert-subs}

에 GET 요청을 수행하여 조직 샌드박스에 대한 모든 경고 목록을 검색합니다. `/alert-subscriptions` 엔드포인트.

**API 형식**

```http
GET /alert-subscriptions
```

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

성공적인 응답은 HTTP 200 상태와 `alerts` 페이지 매김 및 버전 정보가 있는 배열입니다. 다음 `alerts` 배열에는 조직 및 특정 샌드박스에 대한 모든 경고의 세부 정보가 포함되어 있습니다. 응답당 최대 3개의 경고를 사용할 수 있으며, 각 경고 유형당 하나의 경고가 응답 본문에 포함됩니다.

>[!NOTE]
>
>다음 `alerts._links` 의 개체 `alerts` 표시하지 않도록 배열이 잘렸습니다. 전체 예 `alerts._links` 개체는 [POST 요청의 응답](#subscribe-users).

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
| `alerts.assetId` | 특정 쿼리와 경고를 연결한 쿼리 ID입니다. |
| `alerts.id` | 경고의 이름입니다. 이 이름은 경고 서비스에 의해 생성되며, 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType`, 및 흐름 ID. 사용 가능한 경고에 대한 정보는 [Platform 경고 대시보드 설명서](../../observability/alerts/ui.md). |
| `alerts.status` | 경고에는 네 가지 상태 값이 있습니다. `enabled`, `enabling`, `disabled`, 및 `disabling`. 경고는 이벤트를 적극적으로 수신하거나, 관련 구독자와 설정을 모두 유지하고 나중에 사용할 수 있도록 일시 중지되거나, 이러한 상태 간에 전환됩니다. |
| `alerts.alertType` | 경고 유형입니다. 경고에 대한 세 가지 가능한 값이 있습니다. 이러한 값은 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `alerts._links` | 이 경고 ID와 관련된 정보를 검색, 업데이트, 편집 또는 삭제하는 데 사용할 수 있는 메서드 및 끝점에 대한 정보를 제공합니다. |
| `_page` | 객체에는 순서, 크기, 총 페이지 수 및 현재 페이지를 설명하는 속성이 포함되어 있습니다. |
| `_links` | 객체에는 리소스의 다음 페이지나 이전 페이지를 가져오는 데 사용할 수 있는 URI 참조가 포함되어 있습니다. |

## 특정 쿼리 또는 예약 ID에 대한 경고 구독 정보를 검색합니다 {#retrieve-all-alert-subscriptions-by-id}

에 GET 요청을 수행하여 특정 쿼리 ID 또는 예약 ID에 대한 경고 구독 정보를 검색합니다. `/alert-subscriptions/{QUERY_ID}` 또는 `/alert-subscriptions/{SCHEDULE_ID}` 엔드포인트.

**API 형식**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{QUERY_ID}` | 구독 정보를 반환할 쿼리의 ID입니다. |
| `{SCHEDULE_ID}` | 구독 정보를 반환할 예약된 쿼리의 ID입니다. |

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

성공적인 응답은 200이라는 HTTP 상태와 `alerts` 제공된 쿼리 또는 예약 ID에 대한 구독 정보가 포함된 배열입니다.

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
| `assetId` | 경고가 이 ID와 연결됩니다. ID는 쿼리 ID 또는 예약 ID일 수 있습니다. |
| `id` | 경고의 이름입니다. 이 이름은 경고 서비스에 의해 생성되며, 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType`, 및 흐름 ID. 사용 가능한 경고에 대한 정보는 [Platform 경고 대시보드 설명서](../../observability/alerts/ui.md). |
| `status` | 경고에는 네 가지 상태 값이 있습니다. `enabled`, `enabling`, `disabled`, 및 `disabling`. 경고는 이벤트를 적극적으로 수신하거나, 관련 구독자와 설정을 모두 유지하고 나중에 사용할 수 있도록 일시 중지되거나, 이러한 상태 간에 전환됩니다. |
| `alertType` | 각 경고에는 세 가지 서로 다른 경고 유형이 있을 수 있습니다. 절차는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `subscriptions.emailNotifications` | 경고에 대한 전자 메일을 받도록 구독한 사용자에 대해 등록된 Adobe 이메일 주소의 배열입니다. |
| `subscriptions.inContextNotifications` | 경고에 대한 UI 알림을 구독한 사용자에 대해 등록된 Adobe 이메일 주소의 배열입니다. |

## 특정 쿼리 또는 예약 ID 및 경고 유형에 대한 경고 구독 정보를 검색합니다 {#get-alert-info-by-id-and-alert-type}

에 GET 요청을 수행하여 특정 ID 및 경고 유형에 대한 경고 구독 정보를 검색합니다. `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 엔드포인트. 쿼리 또는 예약된 쿼리 ID 모두에 적용할 수 있습니다.

**API 형식**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `ALERT_TYPE` | 각 경고에는 세 가지 서로 다른 경고 유형이 있을 수 있습니다. 절차는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
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

성공적으로 응답하면 200이라는 HTTP 상태와 구독한 모든 경고를 반환합니다. 여기에는 경고 ID, 경고 유형, 가입자의 등록된 이메일 ID Adobe 및 기본 알림 채널이 포함됩니다.

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
| `assetId` | 특정 쿼리와 경고를 연결한 쿼리 ID입니다. |
| `alertType` | 경고 유형입니다. 경고에 대한 세 가지 가능한 값이 있습니다. 이러한 값은 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `subscriptions` | 경고와 연관된 Adobe 등록 이메일 ID와 사용자가 경고를 받을 채널을 전달하는 데 사용되는 객체입니다. |
| `subscriptions.inContextNotifications` | 경고에 대한 UI 알림을 구독한 사용자에 대해 등록된 Adobe 이메일 주소의 배열입니다. |
| `subscriptions.emailNotifications` | 경고에 대한 전자 메일을 받도록 구독한 사용자에 대해 등록된 Adobe 이메일 주소의 배열입니다. |

## 사용자가 가입한 모든 경고 목록을 검색합니다 {#get-alert-subscription-list}

에 GET 요청을 수행하여 사용자가 가입한 모든 경고 목록을 검색합니다. `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` 엔드포인트. 응답에는 경고 이름, ID, 상태, 경고 유형 및 알림 채널이 포함됩니다.

**API 형식**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{EMAIL_ID}` | Adobe 계정에 등록된 이메일 주소는 경고를 구독한 사용자를 식별하는 데 사용됩니다. |

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

성공적인 응답은 HTTP 상태 200 및 `items` 을 구독한 경고의 세부 정보가 있는 배열 `emailId` 제공됩니다.

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
| `name` | 경고의 이름입니다. 이 이름은 경고 서비스에 의해 생성되며, 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType`, 및 흐름 ID. 사용 가능한 경고에 대한 정보는 [Platform 경고 대시보드 설명서](../../observability/alerts/ui.md). |
| `assetId` | 특정 쿼리와 경고를 연결한 쿼리 ID입니다. |
| `status` | 경고에는 네 가지 상태 값이 있습니다. `enabled`, `enabling`, `disabled`, 및 `disabling`. 경고는 이벤트를 적극적으로 수신하거나, 관련 구독자와 설정을 모두 유지하고 나중에 사용할 수 있도록 일시 중지되거나, 이러한 상태 간에 전환됩니다. |
| `alertType` | 경고 유형입니다. 경고에 대한 세 가지 가능한 값이 있습니다. 이러한 값은 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `subscriptions` | 경고와 연관된 Adobe 등록 이메일 ID와 사용자가 경고를 받을 채널을 전달하는 데 사용되는 객체입니다. |
| `subscriptions.inContextNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. A `true` 값은 UI를 통해 경고를 제공해야 함을 확인합니다. A `false` 값은 사용자에게 해당 채널을 통해 알림을 주지 않도록 합니다. |
| `subscriptions.emailNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. A `true` 값은 이메일을 통해 경고를 제공해야 함을 확인합니다. A `false` 값은 사용자에게 해당 채널을 통해 알림을 주지 않도록 합니다. |

## 경고 만들기 및 사용자 가입 {#subscribe-users}

경고를 생성하고 사용자를 가입하여 수신하려면 `POST` 에 요청 `/alert-subscriptions` 엔드포인트. 이 요청은 쿼리를 `assetId` 속성을 사용하여 해당 쿼리에 대한 경고를 사용자에게 구독합니다. `emailIds`.

>[!IMPORTANT]
>
>단일 Adobe에 최대 5개의 등록된 이메일 ID를 전달할 수 있습니다. 경고에 5명 이상의 사용자를 가입하려면 후속 요청을 수행해야 합니다.

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
| `assetId` | 경고가 이 ID와 연결됩니다. ID는 쿼리 ID 또는 예약 ID일 수 있습니다. |
| `alertType` | 경고 유형입니다. 경고에 대한 세 가지 가능한 값이 있습니다. 이러한 값은 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `subscriptions` | 경고와 연관된 Adobe 등록 이메일 ID와 사용자가 경고를 받을 채널을 전달하는 데 사용되는 객체입니다. |
| `subscriptions.emailIds` | 경고를 받아야 하는 사용자를 식별하는 이메일 주소 배열입니다. 이메일 주소 **반드시** Adobe 계정에 등록됩니다. |
| `subscriptions.inContextNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. A `true` 값은 UI를 통해 경고를 제공해야 함을 확인합니다. A `false` 값은 사용자에게 해당 채널을 통해 알림을 주지 않도록 합니다. |
| `subscriptions.emailNotifications` | 사용자가 경고 알림을 받는 방법을 결정하는 부울 값입니다. A `true` 값은 이메일을 통해 경고를 제공해야 함을 확인합니다. A `false` 값은 사용자에게 해당 채널을 통해 알림을 주지 않도록 합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 새로 만든 경고의 세부 정보와 함께 HTTP 상태 202(수락됨)를 반환합니다.

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
| `id` | 경고의 이름입니다. 이 이름은 경고 서비스에 의해 생성되며, 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType`, 및 흐름 ID. 사용 가능한 경고에 대한 정보는 [Platform 경고 대시보드 설명서](../../observability/alerts/ui.md). |
| `_links` | 이 경고 ID와 관련된 정보를 검색, 업데이트, 편집 또는 삭제하는 데 사용할 수 있는 메서드 및 끝점에 대한 정보를 제공합니다. |

## 경고 활성화 또는 비활성화 {#enable-or-disable-alert}

이 요청은 쿼리 또는 예약 ID 및 경고 유형을 사용하여 특정 경고를 참조하고 경고 상태를 다음 중 하나로 업데이트합니다 `enable` 또는 `disable`. 경고를 작성하여 경고 상태를 업데이트할 수 있습니다 `PATCH` 에 요청 `/alert-subscriptions/{queryId}/{alertType}` 또는 `/alert-subscriptions/{scheduleId}/{alertType}` 엔드포인트.

**API 형식**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `ALERT_TYPE` | 경고 유형입니다. 경고에 대한 세 가지 가능한 값이 있습니다. 이러한 값은 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul>변경하려면 끝점 네임스페이스에 현재 경고 유형을 지정해야 합니다. |
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
| `op` | 수행할 작업입니다. 현재 허용되는 값은 `replace`. |
| `path` | 이 값은 끝점의 네임스페이스와 관련이 있습니다. 현재 허용되는 값은 `/status`. |
| `value` | 성공적인 PATCH 요청에서 이렇게 하면 `status` 경고 값입니다. 현재 허용되는 값은 다음과 같습니다 `enable` 또는 `disable`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 경고 상태, 유형 및 ID와 관련된 쿼리의 세부 사항이 포함된 HTTP 상태 200을 반환합니다.

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
| `id` | 경고의 이름입니다. 이 이름은 경고 서비스에 의해 생성되며, 경고 대시보드에서 사용됩니다. 경고 이름은 경고를 저장하는 폴더, `alertType`, 및 흐름 ID. 사용 가능한 경고에 대한 정보는 [Platform 경고 대시보드 설명서](../../observability/alerts/ui.md). |
| `assetId` | 경고가 이 ID와 연결됩니다. ID는 쿼리 ID 또는 예약 ID일 수 있습니다. |
| `alertType` | 각 경고에는 세 가지 서로 다른 경고 유형이 있을 수 있습니다. 절차는 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> |
| `status` | 경고에는 네 가지 상태 값이 있습니다. `enabled`, `enabling`, `disabled`, 및 `disabling`. 경고는 이벤트를 적극적으로 수신하거나, 관련 구독자와 설정을 모두 유지하고 나중에 사용할 수 있도록 일시 중지되거나, 이러한 상태 간에 전환됩니다. |

## 특정 쿼리 및 경고 유형에 대한 경고를 삭제합니다 {#delete-alert-info-by-id-and-alert-type}

에 DELETE 요청을 수행하여 특정 쿼리 또는 예약 ID 및 경고 유형에 대한 경고를 삭제합니다. `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 또는 `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` 엔드포인트.

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `ALERT_TYPE` | 경고 유형입니다. 경고에 대한 세 가지 가능한 값이 있습니다. 이러한 값은 다음과 같습니다. <ul><li>`start`: 쿼리 실행이 시작되면 사용자에게 알립니다.</li><li>`success`: 쿼리가 완료되면 사용자에게 알립니다.</li><li>`failure`: 쿼리가 실패하면 사용자에게 알립니다.</li></ul> DELETE 요청은 제공된 특정 경고 유형에만 적용됩니다. |
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

성공적으로 응답하면 자산 ID 및 삭제된 경고의 경고 유형을 포함하는 확인 메시지와 HTTP 200 상태가 반환됩니다.

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## 다음 단계

이 안내서에서는 `/alert-subscriptions` 쿼리 서비스 API의 끝점입니다. 이 안내서를 읽은 후에는 쿼리에 대한 경고를 생성하고, 사용자를 경고에 가입하며, 사용 가능한 경고 유형과 경고 구독 정보를 검색, 업데이트 및 삭제하는 방법을 보다 잘 이해할 수 있습니다.

자세한 내용은 [Query Service API 안내서](./getting-started.md) 사용 가능한 다른 기능 및 작업에 대해 자세히 알아보십시오.
