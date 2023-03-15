---
title: 규칙 엔드포인트
description: Reactor API에서 /rules 끝점을 호출하는 방법을 알아봅니다.
exl-id: 79ef4389-e4b7-461e-8579-16a1a78cdd43
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 5%

---

# 규칙 엔드포인트

데이터 수집 태그의 컨텍스트에서 규칙은 배포된 라이브러리의 리소스 동작을 제어합니다. 규칙은 하나 이상으로 구성됩니다 [규칙 구성 요소](./rule-components.md)는 규칙 구성 요소를 논리적 방식으로 서로 연결하기 위해 존재합니다. 다음 `/rules` Reactor API의 끝점을 사용하면 태그 규칙을 프로그래밍 방식으로 관리할 수 있습니다.

>[!NOTE]
>
>이 문서에서는 Reactor API에서 규칙을 관리하는 방법을 다룹니다. UI에서 규칙과 상호 작용하는 방법에 대한 자세한 내용은 [UI 안내서](../../ui/managing-resources/rules.md).

규칙은 정확히 하나의 규칙에 속함 [속성](./properties.md). 속성에는 여러 규칙이 있을 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [반응기 API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) API 인증 방법에 대한 중요한 정보를 제공합니다.

## 규칙 목록 검색 {#list}

를 포함하여 속성에 속하는 규칙 목록을 GET 요청으로 검색할 수 있습니다.

**API 형식**

```http
GET /properties/{PROPERTY_ID}/rules
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 다음 `id` 구성 요소를 나열할 속성의 입니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 규칙을 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>다음 안내서를 참조하십시오 [응답 필터링](../guides/filtering.md) 추가 정보.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 속성에 대한 규칙 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "RL8429f3fee98b44c68f7a538e68e21747",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:56:44.109Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:56:44.109Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/property"
          },
          "data": {
            "id": "PR41f64d2a9d9b4862b0582c5ff6a07504",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/origin"
          },
          "data": {
            "id": "RL8429f3fee98b44c68f7a538e68e21747",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR41f64d2a9d9b4862b0582c5ff6a07504",
        "origin": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "self": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747",
        "rule_components": "https://reactor.adobe.io/rules/RL8429f3fee98b44c68f7a538e68e21747/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
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

## 규칙 조회 {#lookup}

GET 요청 경로에 ID를 제공하여 규칙을 조회할 수 있습니다.

>[!NOTE]
>
>규칙이 삭제되면 삭제된 것으로 표시되지만 실제로 시스템에서 제거되지 않습니다. 따라서 삭제된 규칙을 검색할 수 있습니다. 삭제된 규칙은 의 존재로 식별할 수 있습니다. `meta.deleted_at` 속성.

**API 형식**

```http
GET /rules/{RULE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_ID` | 다음 `id` 조회하려는 규칙에 대해 자세히 알아보십시오. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 규칙의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:33.188Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:33.188Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/property"
        },
        "data": {
          "id": "PRfa164e39b0d74eb5b093ab963b1f1200",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/origin"
        },
        "data": {
          "id": "RL14dc6a8c37b14b619ddb2b3ba489a1f5",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRfa164e39b0d74eb5b093ab963b1f1200",
      "origin": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "self": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5",
      "rule_components": "https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f5/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 규칙 만들기 {#create}

POST 요청을 하여 새 규칙을 만들 수 있습니다.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/rules
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 다음 `id` 을 사용하여 규칙을 정의할 수 있습니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Rule",
            "enabled": true,
          },
          "type": "rules"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes.name` | **(필수)** 사람이 인식할 수 있는 규칙 이름. |
| `attributes.enabled` | 규칙이 사용되는지 여부를 나타내는 부울 값입니다. |
| `type` | 만들어지는 리소스의 유형입니다. 이 끝점의 경우 값은 다음과 같아야 합니다. `rules`. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 생성된 규칙의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "RL52d156a9074844b89ca20c987dbafd3b",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:31:46.883Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:31:46.883Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin"
        },
        "data": {
          "id": "RL52d156a9074844b89ca20c987dbafd3b",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "origin": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "self": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "rule_components": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 규칙에 이벤트, 조건 및 작업 추가 {#components}

다음 작업을 완료하면 [이(가) 규칙을 만들었습니다.](#create), 이벤트, 조건 및 작업(통칭하여 규칙 구성 요소라고 함)을 추가하여 논리 구성을 시작할 수 있습니다. 의 섹션을 참조하십시오. [규칙 구성 요소 만들기](./rule-components.md#create) 다음에서 `/rule_components` Reactor API에서 이를 수행하는 방법에 대해 알아보려면 endpoint guide를 참조하십시오.

## 규칙 업데이트 {#update}

PATCH 요청의 경로에 해당 ID를 포함하여 규칙의 속성을 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /rules/{RULE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_ID` | 다음 `id` 업데이트할 규칙의 일부입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 `name` 기존 규칙의 경우입니다.

```shell
curl -X PATCH \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
  "data": {
    "attributes": {
      "name": "Test Rule"
    },
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules"
  }
}'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 규칙이 규칙에 대해 업데이트될 속성을 나타내는 객체입니다. 규칙에 대해 다음 속성을 업데이트할 수 있습니다. <ul><li>`name`</li><li>`enabled`</li></ul> |
| `id` | 다음 `id` 을(를) 업데이트하려고 합니다. 다음과 일치해야 합니다. `{RULE_ID}` 요청 경로에 제공된 값입니다. |
| `type` | 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 다음과 같아야 합니다. `rules`. |

{style="table-layout:auto"}

**응답**

성공한 응답은 업데이트된 규칙의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "RLd2528a53c21a468f93cfd85244f16fdd",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:56:55.026Z",
      "deleted_at": null,
      "dirty": true,
      "enabled": true,
      "name": "Test Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:56:55.717Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/property"
        },
        "data": {
          "id": "PR7e37a33354cc4aa7880f2a550c4f844f",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/origin"
        },
        "data": {
          "id": "RLd2528a53c21a468f93cfd85244f16fdd",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR7e37a33354cc4aa7880f2a550c4f844f",
      "origin": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "self": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd",
      "rule_components": "https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/rule_components"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 규칙 삭제

DELETE 요청의 경로에 ID를 포함하여 규칙을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /rules/{RULE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_ID` | 다음 `id` 삭제할 규칙의 일부입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공한 응답은 응답 본문이 없는 HTTP 상태 204(콘텐츠 없음)를 반환하며, 이는 규칙이 삭제되었음을 나타냅니다.

## 규칙에 대한 메모 관리 {#notes}

규칙은 &quot;주목할 만한&quot; 리소스입니다. 즉, 각 개별 리소스에 대해 텍스트 기반 메모를 만들고 검색할 수 있습니다. 다음을 참조하십시오. [notes 엔드포인트 안내서](./notes.md) 규칙 및 기타 호환 리소스에 대한 메모를 관리하는 방법에 대한 자세한 정보.

## 규칙에 대한 관련 리소스 검색 {#related}

다음 호출은 규칙에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. 날짜 [규칙 조회](#lookup), 이러한 관계는 아래에 나열됩니다. `relationships` 규칙.

다음을 참조하십시오. [관계 안내서](../guides/relationships.md) Reactor API의 관계에 대한 자세한 정보입니다.

### 규칙의 관련 라이브러리 나열 {#libraries}

를 추가하여 특정 규칙을 활용하는 라이브러리를 나열할 수 있습니다 `/libraries` 조회 요청의 경로에 매핑됩니다.

**API 형식**

```http
GET  /rules/{RULE_ID}/libraries
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RULE_ID}` | 다음 `id` 라이브러리를 나열할 규칙의 일부입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLd2528a53c21a468f93cfd85244f16fdd/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 규칙을 사용하는 라이브러리 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "LB62d20ad807a949e6b13b0a2c7299eb65",
      "type": "libraries",
      "attributes": {
        "created_at": "2020-12-14T17:50:19.589Z",
        "name": "My Library",
        "published_at": null,
        "state": "development",
        "updated_at": "2020-12-14T17:50:19.589Z",
        "build_required": true
      },
      "relationships": {
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/builds"
          }
        },
        "environment": {
          "links": {
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/environment"
          },
          "data": null
        },
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/data_elements",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/extensions",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/notes"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/rules",
            "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/relationships/rules"
          }
        },
        "upstream_library": {
          "data": null
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/property"
          },
          "data": {
            "id": "PR241ba9cd56324ac192de68d658f20cb0",
            "type": "properties"
          }
        },
        "last_build": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65/last_build"
          },
          "data": null
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR241ba9cd56324ac192de68d658f20cb0",
        "self": "https://reactor.adobe.io/libraries/LB62d20ad807a949e6b13b0a2c7299eb65"
      },
      "meta": {
        "build_status": null,
        "build_required_detail": "No build found since last state change"
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

### 규칙의 관련 개정 나열 {#revisions}

를 추가하여 규칙의 개정 버전을 나열할 수 있습니다 `/revisions` 조회 요청의 경로에 매핑됩니다.

**API 형식**

```http
GET  /rules/{RULE_ID}/revisions
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RULE_ID}` | 다음 `id` 개정 내용을 나열할 규칙의 일부입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 규칙을 사용하는 개정 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:29.835Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:57:29.835Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "rule_components": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:57:30.528Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:57:30.528Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/property"
          },
          "data": {
            "id": "PR391208e5ea96442ea7903fe3f33f50e7",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/origin"
          },
          "data": {
            "id": "RL67de76e5bff9413aa8ad14e55172d8dc",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR391208e5ea96442ea7903fe3f33f50e7",
        "origin": "https://reactor.adobe.io/rules/RL67de76e5bff9413aa8ad14e55172d8dc",
        "self": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae",
        "rule_components": "https://reactor.adobe.io/rules/RL6e5cb0d1c74542d6a3d04d08c6bb97ae/rule_components"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
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

### 규칙에 대한 관련 원본 조회 {#origin}

를 추가하여 규칙의 출처(이전 버전)를 조회할 수 있습니다 `/origin` 조회 요청의 경로에 매핑됩니다.

**API 형식**

```http
GET /rules/{RULE_ID}/origin
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RULE_ID}` | 다음 `id` 조회하려는 출처의 규칙. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

응답이 성공하면 지정된 규칙 확장의 세부 사항이 반환됩니다.

```json
{
  "data": {
    "id": "RLb83ed2278dc045628c069ab7eb9bb866",
    "type": "rules",
    "attributes": {
      "created_at": "2020-12-14T17:57:41.517Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "Example Rule",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:57:41.517Z",
      "review_status": "unsubmitted"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/property"
        },
        "data": {
          "id": "PR169d832d20ea4243b5a5db0ccc5aae9c",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/origin"
        },
        "data": {
          "id": "RLb83ed2278dc045628c069ab7eb9bb866",
          "type": "rules"
        }
      },
      "rule_components": {
        "links": {
          "related": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR169d832d20ea4243b5a5db0ccc5aae9c",
      "origin": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "self": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866",
      "rule_components": "https://reactor.adobe.io/rules/RLb83ed2278dc045628c069ab7eb9bb866/rule_components"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 규칙에 대한 관련 속성 조회 {#property}

규칙을 소유하는 속성을 추가하여 조회할 수 있습니다 `/property` 조회 요청의 경로에 매핑됩니다.

**API 형식**

```http
GET /rules/{RULE_ID}/property
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RULE_ID}` | 다음 `id` 조회할 속성의 규칙. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RC3d0805fde85d42db8988090bc074bb44/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 규칙의 속성에 대한 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "PR8ac25b57d5c24ebab68ffe5c630fc690",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:53:19.088Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:53:19.088Z",
      "platform": "web",
      "development": false,
      "token": "97b2cb1177df",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/environments",
      "extensions": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/extensions",
      "rules": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690/rules",
      "self": "https://reactor.adobe.io/properties/PR8ac25b57d5c24ebab68ffe5c630fc690"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
