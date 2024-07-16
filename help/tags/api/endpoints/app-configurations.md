---
title: 앱 구성 끝점
description: Reactor API에서 /app_configurations 끝점을 호출하는 방법을 알아봅니다.
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 4%

---

# 앱 구성 끝점

>[!WARNING]
>
>기능이 추가, 제거 및 다시 만들어짐에 따라 `/app_configurations` 끝점의 구현이 유동적입니다.

앱 구성을 사용하면 자격 증명을 저장하고 나중에 사용할 수 있도록 검색할 수 있습니다. Reactor API의 `/app_configurations` 끝점을 사용하면 경험 응용 프로그램 내에서 앱 구성을 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 가이드에 사용된 끝점은 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)의 일부입니다. 계속하기 전에 [시작 안내서](../getting-started.md)에서 API 인증 방법에 대한 중요한 정보를 검토하십시오.

## 앱 구성 목록 검색 {#list}

**API 형식**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| 매개변수 | 설명 |
| --- | --- |
| `COMPANY_ID` | 앱 구성을 소유한 [회사](./companies.md)의 `id`입니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 앱 구성을 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>자세한 내용은 [응답 필터링](../guides/filtering.md)에 대한 안내서를 참조하세요.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 앱 구성 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 앱 구성 조회 {#lookup}

GET 요청의 경로에 ID를 제공하여 앱 구성을 조회할 수 있습니다.

**API 형식**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 조회할 앱 구성의 `id`입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 앱 구성의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 앱 구성 만들기 {#create}

POST 요청을 하여 새 앱 구성을 만들 수 있습니다.

**API 형식**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| 매개변수 | 설명 |
| --- | --- |
| `COMPANY_ID` | 아래에 앱 구성을 정의하는 [company](./companies.md)의 `id`입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `platform` | 애플리케이션이 실행되는 플랫폼(웹 또는 모바일)입니다. 사용 가능한 메시징 서비스를 결정합니다. |
| `messaging_service` | 앱과 연결된 메시징 서비스(예: [APNs(Apple 푸시 알림 서비스)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) 및 [FCM(Firebase Cloud Messaging)](https://firebase.google.com/docs/cloud-messaging)). 사용할 수 있는 키 유형을 결정합니다. |
| `key_type` | 푸시 서비스 공급업체가 지원하는 프로토콜을 나타내며 `push_credential` 개체의 형식을 결정합니다. 메시징 서비스에 대한 프로토콜이 발전함에 따라 업데이트된 프로토콜을 지원하도록 새 `key_type` 값이 만들어집니다. |
| `push_credential` | 사용하지 않을 때 암호화된 실제 자격 증명 값입니다. 이 필드는 정상적으로 해독되거나 API 응답에 포함되지 않습니다. 특정 Adobe 서비스만 복호화된 푸시 자격 증명이 포함된 응답을 가져올 수 있습니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 생성된 앱 구성의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 앱 구성 업데이트

PATCH 요청의 경로에 ID를 포함하여 앱 구성을 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 업데이트할 앱 구성의 `id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 기존 앱 구성에 대한 `app_id`을(를) 업데이트합니다.

```shell
curl -X PATCH \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 속성이 앱 구성에 대해 업데이트할 속성을 나타내는 개체입니다. 각 키는 업데이트해야 하는 해당 값과 함께 업데이트할 특정 앱 구성 속성을 나타냅니다.<br><br>앱 구성에 대해 다음 특성을 업데이트할 수 있습니다.<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | 업데이트할 앱 구성의 `id`입니다. 요청 경로에 제공된 `{APP_CONFIGURATION_ID}` 값과 일치해야 합니다. |
| `type` | 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 `app_configurations`이어야 합니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 업데이트된 앱 구성의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 앱 구성 삭제

DELETE 요청의 경로에 ID를 포함하여 앱 구성을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 삭제할 앱 구성의 `id`입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 응답 본문이 없는 HTTP 상태 204(콘텐츠 없음)를 반환하여 앱 구성이 삭제되었음을 나타냅니다.
