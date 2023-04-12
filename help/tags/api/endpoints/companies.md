---
title: 회사 끝점
description: Reactor API에서 /companies 종단점을 호출하는 방법을 알아봅니다.
exl-id: ee435358-ed34-4e0c-93af-796133fb11fc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---

# 회사 끝점

회사는 고객 조직(일반적으로 비즈니스)을 나타냅니다. Reactor API에서 이러한 회사는 조직 ID와 1:1을 연결합니다. API 사용자는 액세스 권한이 있는 회사만 볼 수 있습니다. 한 회사에 많은 것이 있을 수 있습니다 [속성](./properties.md). 재산은 정확히 하나의 회사에 속합니다.

다음 `/companies` reactor API의 종단점을 사용하면 experience 애플리케이션 내에서 액세스할 수 있는 회사를 프로그래밍 방식으로 검색할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 [시작 안내서](../getting-started.md) 를 참조하십시오.

## 회사 목록 검색 {#list}

에 GET 요청을 작성하여 사용할 수 있는 회사를 나열할 수 있습니다 `/companies` 엔드포인트. 대부분의 경우 정확히 하나가 있습니다.

**API 형식**

```http
GET /companies
```

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 회사를 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>다음 안내서를 참조하십시오. [응답 필터링](../guides/filtering.md) 추가 정보.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답에는 액세스 권한이 있는 회사 목록이 반환됩니다.

```json
{
  "data": [
    {
      "id": "COdb0cd64ad4524440be94b8496416ec7d",
      "type": "companies",
      "attributes": {
        "created_at": "2020-08-13T17:13:30.667Z",
        "name": "Example Company",
        "org_id": "{ORG_ID}",
        "updated_at": "2020-08-13T17:13:30.667Z",
        "token": "d5a4f682bbae",
        "cjm_enabled": false,
        "edge_enabled": false,
        "edge_events_allotment": null,
        "edge_fanout_ratio": null
      },
      "relationships": {
        "properties": {
          "links": {
            "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
        "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
      },
      "meta": {
        "rights": [
          "develop_extensions",
          "manage_properties"
        ],
        "platform_rights": {
          "web": [
            "develop_extensions",
            "manage_properties"
          ],
          "mobile": [
            "develop_extensions",
            "manage_properties"
          ]
        }
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

## 회사 찾기 {#lookup}

GET 요청 경로에 해당 ID를 포함하여 특정 회사를 조회할 수 있습니다.

**API 형식**

```http
GET /companies/{COMPANY_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{COMPANY_ID}` | 다음 `id` 조회하려는 회사의 가치 |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 회사의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "COdb0cd64ad4524440be94b8496416ec7d",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.667Z",
      "name": "Example Company",
      "org_id": "{ORG_ID}",
      "updated_at": "2020-08-13T17:13:30.667Z",
      "token": "d5a4f682bbae",
      "cjm_enabled": false,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
      "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties"
        ]
      }
    }
  }
}
```
