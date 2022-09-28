---
title: 규칙 구성 요소 끝점
description: Reactor API에서 /rule_components 끝점을 호출하는 방법을 알아봅니다.
exl-id: 8a878a89-7f41-45fc-88f3-17f0f743e29c
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 6%

---

# 규칙 구성 요소 끝점

데이터 수집 태그에서, [규칙](./rules.md) 배포에서 리소스의 동작을 제어합니다 [라이브러리](./libraries.md). **규칙 구성 요소** 규칙을 구성하는 개별 부품입니다. 규칙이 배합식인 경우 규칙 구성요소는 재료 중 하나입니다. 다음 `/rule_components` reactor API의 종단점을 사용하면 규칙 구성 요소를 프로그래밍 방식으로 관리할 수 있습니다.

>[!NOTE]
>
>이 문서에서는 Reactor API에서 규칙 구성 요소를 관리하는 방법을 다룹니다. UI에서 규칙 및 규칙 구성 요소와 상호 작용하는 방법에 대한 자세한 내용은 [UI 안내서](../../ui/managing-resources/rules.md).

규칙 구성 요소에는 세 가지 기본 유형이 있습니다.

| 규칙 구성 요소 유형 | 설명 |
| --- | --- |
| 이벤트 | 이벤트는 규칙의 트리거입니다. 규칙은 클라이언트 장치에서 런타임 시 이벤트가 발생할 때 시작됩니다. &quot;[!UICONTROL 라이브러리 로드]&quot;, &quot;[!UICONTROL 페이지 상단]&quot; 및 &quot;[!UICONTROL 클릭]&quot;는 이벤트의 예입니다. |
| 조건 | 조건은 작업이 실행되기 전에 특정 기준을 충족하는지 여부를 평가하는 것입니다. 이벤트가 발생하면 조건이 평가됩니다. 규칙의 작업은 모든 조건이 충족되는 경우에만 실행됩니다. |
| 작업 | Adobe Analytics 비콘 보내기, 사용자 지정 방문자 ID 검색 또는 특정 mbox 실행 등 규칙이 실제로 수행하려는 작업입니다. |

{style=&quot;table-layout:auto&quot;}

규칙 구성 요소는 정확히 하나의 규칙에 속합니다. 규칙에는 많은 규칙 구성 요소가 있을 수 있습니다.

규칙 구성 요소는 정확히 하나의 [확장](./extensions.md). 확장은 다양한 규칙 구성 요소 유형을 제공할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 [시작 안내서](../getting-started.md) 를 참조하십시오.

## 규칙 구성 요소 목록 검색 {#list}

GET 요청 경로에 규칙의 ID를 포함하여 규칙에 속하는 규칙 구성 요소 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /rules/{RULE_ID}/rule_components
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_ID` | 다음 `id` 구성 요소를 나열할 규칙의 규칙입니다. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 규칙 구성 요소를 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`negate`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>다음 안내서를 참조하십시오. [응답 필터링](../guides/filtering.md) 추가 정보.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f51/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 규칙에 대한 규칙 구성 요소 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "RC45944086902c4828b6e14ffbb40017f4",
      "type": "rule_components",
      "attributes": {
        "created_at": "2020-12-14T17:54:34.976Z",
        "delegate_descriptor_id": "kessel-test::events::click",
        "deleted_at": null,
        "dirty": true,
        "name": "My Example Click Event",
        "negate": false,
        "order": 0,
        "rule_order": 50.0,
        "timeout": 2000,
        "delay_next": true,
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:54:34.976Z",
        "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
      },
      "relationships": {
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension"
          },
          "data": {
            "id": "EX6312cea676de47ad9f70b42f7c0fbf02",
            "type": "extensions"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/extension"
          },
          "data": {
            "id": "EXbfd099788024423ebdd49cf06b52e50a",
            "type": "extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/notes"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/origin"
          },
          "data": {
            "id": "RC45944086902c4828b6e14ffbb40017f4",
            "type": "rule_components"
          }
        },
        "rule component": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PRb1090b7443e948ac91650964b490e622"
          },
          "data": {
            "id": "PRb1090b7443e948ac91650964b490e622",
            "type": "properties"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules"
          }
        }
      },
      "links": {
        "extension": "https://reactor.adobe.io/extensions/EXbfd099788024423ebdd49cf06b52e50a",
        "origin": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4",
        "rules": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules",
        "self": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4"
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

## 규칙 구성 요소 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 규칙 구성 요소를 찾을 수 있습니다.

**API 형식**

```http
GET /rule_components/{RULE_COMPONENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_COMPONENT_ID` | 다음 `id` 조회하려는 규칙 구성 요소의 예입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 규칙 구성 요소의 세부 사항을 반환합니다.

```json
{
  "data": {
    "id": "RC7be169fcfd534ffc82acc7bffdc50128",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:18.551Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:18.551Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension"
        },
        "data": {
          "id": "EXa11e168f2ff2485197a493095269f964",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/extension"
        },
        "data": {
          "id": "EXa76eb16dd86849318b743494e75c33a1",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/origin"
        },
        "data": {
          "id": "RC7be169fcfd534ffc82acc7bffdc50128",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR00a35a74381443dc994e6b30b7152106"
        },
        "data": {
          "id": "PR00a35a74381443dc994e6b30b7152106",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXa76eb16dd86849318b743494e75c33a1",
      "origin": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128",
      "rules": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules",
      "self": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 규칙 구성 요소 만들기 {#create}

POST 요청을 만들어 새 규칙 구성 요소를 만들 수 있습니다.

**API 형식**

```http
POST /rules/{RULE_ID}/rule_components
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_ID` | 다음 `id` 규칙 구성 요소를 정의하는 규칙의 예입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 지정된 규칙에 대한 새 규칙 구성 요소를 만듭니다. 또한 호출은 규칙 구성 요소를 `relationships` 속성을 사용합니다. 다음 안내서를 참조하십시오. [관계](../guides/relationships.md) 추가 정보.

```shell
curl -X POST \
  https://reactor.adobe.io/rules/RLf7b4f416b2e04ae1ba857ae681fee5bc/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "delay_next": true,
            "order": 0,
            "rule_order": 50.0,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}",
            "timeout": 2000
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX31b8c49f134b4307924d71a64204099e",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLf7b4f416b2e04ae1ba857ae681fee5bc",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes.delegate_descriptor_id` | **(필수)** 정의할 수 있는 규칙 구성 요소의 유형은 다음과 같습니다. [확장 패키지](./extension-packages.md). 새 규칙 구성 요소를 만들 때 이 규칙 구성 요소가 기반으로 하는 확장 패키지, 구성 요소의 유형(이벤트, 조건 또는 작업) 및 확장에서 정의한 특정 구성 요소의 이름(예: 코어 확장의 &quot;클릭&quot; 이벤트)을 나타내는 위임 설명자 ID를 제공해야 합니다.<br><br>다음 안내서를 참조하십시오. [위임 설명자 ID](../guides/delegate-descriptor-ids.md) 추가 정보. |
| `attributes.name` | **(필수)** 규칙 구성 요소의 사람이 읽을 수 있는 이름입니다. |
| `attributes.delay_next` | 나중에 작업을 지연할지 여부를 나타내는 부울입니다. |
| `attributes.order` | 유형별로 구성 요소를 로드하는 순서를 나타내는 정수입니다. |
| `attributes.rule_order` | 연결된 규칙이 실행될 우선순위를 나타내는 정수입니다. |
| `attributes.settings` | 문자열로 표시되는 설정 JSON 개체. |
| `attributes.timeout` | 시퀀스에서 실행되는 작업의 시간 제한을 나타내는 정수입니다. |
| `relationships` | 규칙 구성 요소에 필요한 관계를 설정하는 객체입니다. 두 가지 관계를 설정해야 합니다. <ol><li>`extension`: 이 규칙 구성 요소를 정의하는 확장입니다. 확장 패키지가 `delegate_descriptor_id`.</li><li>`rules`: 이 구성 요소가 정의되는 규칙입니다. 요청 경로에 제공된 것과 동일한 규칙 ID여야 합니다.</li></ol>관계에 대한 자세한 내용은 [관계 안내서](../guides/relationships.md). |
| `type` | 만들어지는 리소스 유형입니다. 이 끝점의 경우 값은 `rule_components`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 새로 만든 규칙 구성 요소의 세부 사항을 반환합니다.

```json
{
  "data": {
    "id": "RC78c44af3cf7644e5927fc0ad61e88940",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:00.232Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:00.232Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension"
        },
        "data": {
          "id": "EX0019a115a74f401fa0b9bb8f57a0196b",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/extension"
        },
        "data": {
          "id": "EX31b8c49f134b4307924d71a64204099e",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/origin"
        },
        "data": {
          "id": "RC78c44af3cf7644e5927fc0ad61e88940",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR97596432a82549ceb8e2a5d9df05c0e1"
        },
        "data": {
          "id": "PR97596432a82549ceb8e2a5d9df05c0e1",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EX31b8c49f134b4307924d71a64204099e",
      "origin": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940",
      "rules": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules",
      "self": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 규칙 구성 요소 업데이트 {#update}

PATCH 요청 경로에 해당 ID를 포함하여 규칙 구성 요소를 업데이트할 수 있습니다.

>[!NOTE]
>
>규칙 구성 요소를 업데이트하면 상위 규칙의 `updated_at` timestamp.

**API 형식**

```http
PATCH /rule_components/{RULE_COMPONENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_COMPONENT_ID` | 다음 `id` 업데이트하려는 규칙 구성 요소입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 를 업데이트합니다 `order` 및 `settings` 기존 규칙 구성 요소의 속성입니다.

```shell
curl -X PATCH \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "order": 1,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
          },
          "type": "rule_components",
          "id": "RC9af052ee231346f28d1e44865ab62c04"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 규칙 구성 요소가 규칙 구성 요소에 대해 업데이트할 속성을 나타내는 객체입니다. 규칙 구성 요소에 대해 다음 속성을 업데이트할 수 있습니다. <ul><li>`delay_next`</li><li>`delegate_descriptor_id`</li><li>`name`</li><li>`order`</li><li>`rule_order`</li><li>`settings`</li><li>`timeout`</li></ul> |
| `id` | 다음 `id` 업데이트하려는 규칙 구성 요소의 예입니다. 이 옵션은 와 일치해야 합니다. `{RULE_COMPONENT_ID}` 요청 경로에 제공된 값입니다. |
| `type` | 업데이트할 리소스 유형입니다. 이 끝점의 경우 값은 `rule_components`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 업데이트된 규칙 구성 요소의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "RC9af052ee231346f28d1e44865ab62c04",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:50.887Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 1,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:52.553Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension"
        },
        "data": {
          "id": "EX468796dd09d743858f17d4c5ca52f3e0",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension"
        },
        "data": {
          "id": "EXcedb08a8265c488e8bb98b46245b2486",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/origin"
        },
        "data": {
          "id": "RC9af052ee231346f28d1e44865ab62c04",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR986402dc07834fbeb4789c56060dbf41"
        },
        "data": {
          "id": "PR986402dc07834fbeb4789c56060dbf41",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXcedb08a8265c488e8bb98b46245b2486",
      "origin": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04",
      "rules": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules",
      "self": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 규칙 구성 요소 삭제

DELETE 요청 경로에 해당 ID를 포함하여 규칙 구성 요소를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /rule_components/{RULE_COMPONENT_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `RULE_COMPONENT_ID` | 다음 `id` 삭제할 규칙 구성 요소입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답은 규칙 구성 요소가 삭제되었음을 나타내는 응답 본문이 없는 HTTP 상태 204(컨텐츠 없음)를 반환합니다.

## 규칙 구성 요소에 대한 노트 관리 {#notes}

규칙 구성 요소는 &quot;주목할 만한&quot; 리소스입니다. 즉, 각 개별 리소스에 대해 텍스트 기반 메모를 만들고 검색할 수 있습니다. 자세한 내용은 [참고 끝점 안내서](./notes.md) 를 참조하십시오.

## 규칙 구성 요소에 대한 관련 리소스 검색 {#related}

다음 호출에서는 규칙 구성 요소에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. When [규칙 구성 요소 조회](#lookup)로 설정되면 이러한 관계는 `relationships` 규칙 구성 요소입니다.

자세한 내용은 [관계 안내서](../guides/relationships.md) 를 참조하십시오.

### 규칙 구성 요소에 대한 관련 규칙 나열 {#rules}

다음을 추가하여 특정 규칙 구성 요소를 활용하는 규칙을 나열할 수 있습니다 `/rules` 조회 요청의 경로에 추가할 수 없습니다.

**API 형식**

```http
GET  /rule_components/{RULE_COMPONENT_ID}/rules
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 다음 `id` 규칙을 나열할 규칙 구성 요소입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 규칙 구성 요소를 사용하는 규칙 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "RLf1baa571748941db88f54de8efd119aa",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:58:36.072Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:58:37.452Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/property"
          },
          "data": {
            "id": "PR966c4a501e1a43a48cb55e104b4de935",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/origin"
          },
          "data": {
            "id": "RLf1baa571748941db88f54de8efd119aa",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR966c4a501e1a43a48cb55e104b4de935",
        "origin": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "self": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "rule_components": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ]
}
```

### 규칙 구성 요소에 대한 관련 확장 조회 {#extension}

다음을 추가하여 규칙 구성 요소를 제공하는 확장을 찾을 수 있습니다 `/extension` 조회 요청의 경로에 추가할 수 없습니다.

**API 형식**

```http
GET /rule_components/{RULE_COMPONENT_ID}/extension
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 다음 `id` 확장을 조회하려는 규칙 구성 요소의 예입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 규칙 구성 요소의 확장에 대한 세부 사항을 반환합니다.

```json
{
  "data": {
    "id": "EX5644c3eed97d46b39cb2279ea11dde29",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:55:22.634Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:22.634Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/property"
        },
        "data": {
          "id": "PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/origin"
        },
        "data": {
          "id": "EX5644c3eed97d46b39cb2279ea11dde29",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
      "origin": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "self": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 규칙 구성 요소에 대한 관련 원본 조회 {#origin}

를 추가하여 규칙 구성 요소의 원본(이전 개정)을 조회할 수 있습니다 `/origin` 조회 요청의 경로에 추가할 수 없습니다.

**API 형식**

```http
GET /rule_components/{RULE_COMPONENT_ID}/origin
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 다음 `id` 규칙을 검색하는 데 사용할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 규칙 구성 요소의 원본 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "RC3d0805fde85d42db8988090bc074bb44",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:55:40.016Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": false,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:40.016Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension"
        },
        "data": {
          "id": "EXb713fc209ce344c996bdeb377685e2c4",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/extension"
        },
        "data": {
          "id": "EXd6e1dce006b2412f874301e24d58ce24",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin"
        },
        "data": {
          "id": "RC3d0805fde85d42db8988090bc074bb44",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR89c66a560ec44928889b439333255efe"
        },
        "data": {
          "id": "PR89c66a560ec44928889b439333255efe",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXd6e1dce006b2412f874301e24d58ce24",
      "origin": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44",
      "rules": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules",
      "self": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```
