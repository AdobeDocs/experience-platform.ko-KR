---
title: 감사 이벤트 엔드포인트
description: Reactor API에서 /audit_events 끝점을 호출하는 방법을 알아봅니다.
exl-id: 59cd58dc-4085-47b7-846f-d3937740dd9b
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# 감사 이벤트 엔드포인트

>[!WARNING]
>
>기능이 추가, 제거 및 다시 만들어짐에 따라 `/audit_events` 끝점의 구현이 유동적입니다.

감사 이벤트는 변경 시 생성된 Reactor API의 다른 리소스에 대한 특정 변경 사항의 기록입니다. [callback](./callbacks.md)을 사용하여 구독할 수 있는 시스템 이벤트입니다. Reactor API의 `/audit_events` 끝점을 사용하면 경험 응용 프로그램 내에서 감사 이벤트를 프로그래밍 방식으로 관리할 수 있습니다.

감사 이벤트는 `build.created` 또는 `rule.updated`과(와) 같이 `{RESOURCE_TYPE}.{EVENT}` 형식으로 구성되어 있습니다.

리소스 유형은 다음 중 하나일 수 있습니다.

* `property`
* `extension`
* `data_element`
* `rule`
* `rule_component`
* `library`
* `build`
* `environment`
* `host`

각 리소스 유형에 대해 지원되는 이벤트는 다음과 같습니다.

* `created`
* `updated`
* `deleted`

## 시작하기

이 가이드에 사용된 끝점은 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)의 일부입니다. 계속하기 전에 [시작 안내서](../getting-started.md)에서 API 인증 방법에 대한 중요한 정보를 검토하십시오.

## 감사 이벤트 목록 검색 {#list}

`/audit_events` 끝점에 대한 GET 요청을 통해 조직에서 소유한 모든 속성의 감사 이벤트 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /audit_events
```

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답이 감사 이벤트 목록을 반환합니다. 아래 예제 응답은 공백으로 잘렸습니다.

```json
{
  "data": [
    {
      "id": "AEa98742de8ef044d8b86767aa6a15a674",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:21.836Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.updated",
        "updated_at": "2020-12-14T17:31:21.836Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app_2\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:21.787Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674"
      }
    },
    {
      "id": "AE7320b6c1c3f84bb69405fcfe9cb58189",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:10.672Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.created",
        "updated_at": "2020-12-14T17:31:10.672Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:10.626Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AE7320b6c1c3f84bb69405fcfe9cb58189"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=129&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## 감사 이벤트 조회 {#lookup}

GET 요청 경로에 ID를 제공하여 감사 이벤트를 조회할 수 있습니다.

**API 형식**

```http
GET /audit_events/{AUDIT_EVENT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `AUDIT_EVENT_ID` | 조회할 감사 이벤트의 `id`입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 감사 이벤트의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "AEd6a3b381fb8241818d7520001f8bd459",
    "type": "audit_events",
    "attributes": {
      "attributed_to_display_name": "John Smith",
      "attributed_to_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:31:46.956Z",
      "display_name": "Example Rule",
      "type_of": "rule.created",
      "updated_at": "2020-12-14T17:31:46.956Z",
      "entity": "{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"meta\":{\"latest_revision_number\":0},\"type\":\"rules\",\"links\":{\"self\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"origin\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"property\":\"https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"rule_components\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"},\"attributes\":{\"name\":\"Example Rule\",\"dirty\":true,\"enabled\":true,\"published\":false,\"created_at\":\"2020-12-14T17:31:46.883Z\",\"deleted_at\":null,\"updated_at\":\"2020-12-14T17:31:46.883Z\",\"published_at\":null,\"review_status\":\"unsubmitted\",\"revision_number\":0},\"relationships\":{\"notes\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes\"}},\"origin\":{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"type\":\"rules\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin\"}},\"property\":{\"data\":{\"id\":\"PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"type\":\"properties\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property\"}},\"libraries\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries\"}},\"revisions\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions\"}},\"rule_components\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"}}}}}"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "entity": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/rule"
        },
        "data": {
          "type": "rules",
          "id": "RL52d156a9074844b89ca20c987dbafd3b"
        }
      }
    },
    "links": {
      "entity": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "self": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459"
    },
    "meta": {
      "property_name": "Kessel Example Property"
    }
  }
}
```
