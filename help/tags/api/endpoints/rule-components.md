---
title: 규칙 구성 요소 끝점
description: Reactor API에서 /rule_components 끝점을 호출하는 방법을 알아봅니다.
exl-id: 8a878a89-7f41-45fc-88f3-17f0f743e29c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 3%

---

# 규칙 구성 요소 끝점

데이터 수집 태그에서 [규칙](./rules.md)은(는) 배포된 [라이브러리](./libraries.md)에 있는 리소스의 동작을 제어합니다. **규칙 구성 요소**&#x200B;는 규칙을 구성하는 개별 부분입니다. 규칙이 레시피인 경우 규칙 구성 요소는 구성 요소 중 하나입니다. Reactor API의 `/rule_components` 끝점을 사용하면 규칙 구성 요소를 프로그래밍 방식으로 관리할 수 있습니다.

>[!NOTE]
>
>이 문서에서는 Reactor API에서 규칙 구성 요소를 관리하는 방법을 다룹니다. UI에서 규칙 및 규칙 구성 요소와 상호 작용하는 방법에 대한 자세한 내용은 [UI 안내서](../../ui/managing-resources/rules.md)를 참조하십시오.

규칙 구성 요소에는 세 가지 기본 유형이 있습니다.

| 규칙 구성 요소 유형 | 설명 |
| --- | --- |
| 이벤트 | 이벤트는 규칙에 대한 트리거입니다. 이 규칙은 이벤트가 클라이언트 장치에서 런타임에 발생할 때 시작됩니다. &quot;[!UICONTROL 라이브러리 로드]&quot;, &quot;[!UICONTROL 페이지 상단]&quot; 및 &quot;[!UICONTROL 클릭]&quot;은(는) 이벤트의 예입니다. |
| 조건 | 조건은 작업이 실행되기 전에 특정 기준이 충족되는지 여부를 평가하는 것입니다. 이벤트가 발생하면 조건이 평가됩니다. 규칙의 작업은 모든 조건이 충족되는 경우에만 실행됩니다. |
| 작업 | Adobe Analytics 비콘 보내기, 사용자 지정 방문자 ID 검색 또는 특정 mbox 실행과 같이 규칙이 실제로 수행할 작업입니다. |

{style="table-layout:auto"}

규칙 구성 요소는 정확히 하나의 규칙에 속합니다. 규칙에는 많은 규칙 구성 요소가 포함될 수 있습니다.

규칙 구성 요소는 정확히 하나의 [확장](./extensions.md)에 의해 제공됩니다. 확장은 많은 규칙 구성 요소 유형을 제공할 수 있습니다.

## 시작하기

이 가이드에 사용된 끝점은 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)의 일부입니다. 계속하기 전에 [시작 안내서](../getting-started.md)에서 API 인증 방법에 대한 중요한 정보를 검토하십시오.

## 규칙 구성 요소 목록 검색 {#list}

GET 요청의 경로에 규칙 ID를 포함하여 규칙에 속하는 규칙 구성 요소 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /rules/{RULE_ID}/rule_components
```

| 매개변수 | 설명 |
| --- | --- |
| `RULE_ID` | 나열할 구성 요소가 있는 규칙의 `id`입니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 규칙 구성 요소를 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`negate`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>자세한 내용은 [응답 필터링](../guides/filtering.md)에 대한 안내서를 참조하세요.

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

성공한 응답은 지정된 규칙에 대한 규칙 구성 요소 목록을 반환합니다.

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

GET 요청의 경로에 ID를 제공하여 규칙 구성 요소를 조회할 수 있습니다.

**API 형식**

```http
GET /rule_components/{RULE_COMPONENT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `RULE_COMPONENT_ID` | 조회할 규칙 구성 요소의 `id`입니다. |

{style="table-layout:auto"}

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

POST 요청을 수행하여 새 규칙 구성 요소를 만들 수 있습니다.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/rule_components
```

| 매개변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 아래에 규칙 구성 요소를 정의하는 속성의 `id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 새 규칙 구성 요소를 만듭니다. 페이로드에서 `relationships` 속성은 구성 요소를 특정 규칙 및 기존 확장과 연결합니다. 자세한 내용은 [관계](../guides/relationships.md)에 대한 안내서를 참조하세요.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97596432a82549ceb8e2a5d9df05c0e1/rule_components \
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
| `attributes.delegate_descriptor_id` | **(필수)** 정의할 수 있는 규칙 구성 요소 유형은 [확장 패키지](./extension-packages.md)에서 제공합니다. 새 규칙 구성 요소를 만들 때 이 규칙 구성 요소의 기반이 되는 확장 패키지, 구성 요소의 유형(이벤트, 조건 또는 작업) 및 확장에서 정의한 특정 구성 요소(예: 핵심 확장의 &quot;Click&quot; 이벤트)의 이름을 나타내는 위임 설명자 ID를 제공해야 합니다.<br><br>자세한 내용은 [설명자 ID 위임](../guides/delegate-descriptor-ids.md)의 안내서를 참조하십시오. |
| `attributes.name` | **(필수)** 사람이 인식할 수 있는 규칙 구성 요소 이름입니다. |
| `attributes.delay_next` | 이후 작업을 지연할지 여부를 나타내는 부울입니다. |
| `attributes.order` | 유형별로 구성 요소를 로드하는 순서를 나타내는 정수. |
| `attributes.rule_order` | 실행할 관련 규칙의 우선 순위를 나타내는 정수입니다. |
| `attributes.settings` | 문자열로 표시되는 설정 JSON 개체입니다. |
| `attributes.timeout` | 순서대로 실행되는 작업의 시간 제한을 나타내는 정수. |
| `relationships` | 규칙 구성 요소에 필요한 관계를 설정하는 객체입니다. 두 가지 관계를 설정해야 합니다. <ol><li>`extension`: 이 규칙 구성 요소를 정의하는 확장입니다. 확장 패키지가 `delegate_descriptor_id`(으)로 표시된 확장과 동일해야 합니다.</li><li>`rules`: 이 구성 요소를 정의하는 규칙입니다.</li></ol>관계에 대한 일반적인 정보는 [관계 안내서](../guides/relationships.md)를 참조하세요. |
| `type` | 만들어지는 리소스의 유형입니다. 이 끝점의 경우 값은 `rule_components`이어야 합니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 생성된 규칙 구성 요소의 세부 정보를 반환합니다.

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

규칙 요청의 경로에 ID를 포함하여 PATCH 구성 요소를 업데이트할 수 있습니다.

>[!NOTE]
>
>규칙 구성 요소를 업데이트하면 상위 규칙의 `updated_at` 타임스탬프도 업데이트됩니다.

**API 형식**

```http
PATCH /rule_components/{RULE_COMPONENT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `RULE_COMPONENT_ID` | 업데이트할 규칙 구성 요소의 `id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 기존 규칙 구성 요소에 대한 `order` 및 `settings` 특성을 업데이트합니다.

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
| `attributes` | 규칙 구성 요소가 규칙 구성 요소에 대해 업데이트될 속성을 나타내는 객체입니다. 규칙 구성 요소에 대해 다음 속성을 업데이트할 수 있습니다. <ul><li>`delay_next`</li><li>`delegate_descriptor_id`</li><li>`name`</li><li>`order`</li><li>`rule_order`</li><li>`settings`</li><li>`timeout`</li></ul> |
| `id` | 업데이트할 규칙 구성 요소의 `id`입니다. 요청 경로에 제공된 `{RULE_COMPONENT_ID}` 값과 일치해야 합니다. |
| `type` | 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 `rule_components`이어야 합니다. |

{style="table-layout:auto"}

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

DELETE 요청의 경로에 ID를 포함하여 규칙 구성 요소를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /rule_components/{RULE_COMPONENT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `RULE_COMPONENT_ID` | 삭제할 규칙 구성 요소의 `id`입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공한 응답은 응답 본문이 없는 HTTP 상태 204(콘텐츠 없음)를 반환하며, 이는 규칙 구성 요소가 삭제되었음을 나타냅니다.

## 규칙 구성 요소에 대한 참고 사항 관리 {#notes}

규칙 구성 요소는 &quot;주목할 만한&quot; 리소스입니다. 즉, 각 개별 리소스에 대해 텍스트 기반 메모를 만들고 검색할 수 있습니다. 규칙 구성 요소 및 기타 호환되는 리소스에 대한 메모를 관리하는 방법에 대한 자세한 내용은 [메모 끝점 안내서](./notes.md)를 참조하십시오.

## 규칙 구성 요소에 대한 관련 리소스 검색 {#related}

다음 호출은 규칙 구성 요소에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. [규칙 구성 요소를 조회](#lookup)할 때 이러한 관계는 `relationships` 규칙 구성 요소 아래에 나열됩니다.

Reactor API의 관계에 대한 자세한 내용은 [관계 안내서](../guides/relationships.md)를 참조하십시오.

### 규칙 구성 요소에 대한 관련 규칙 나열 {#rules}

조회 요청의 경로에 `/rules`을(를) 추가하여 특정 규칙 구성 요소를 활용하는 규칙을 나열할 수 있습니다.

**API 형식**

```http
GET  /rule_components/{RULE_COMPONENT_ID}/rules
```

| 매개변수 | 설명 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 규칙을 나열할 규칙 구성 요소의 `id`입니다. |

{style="table-layout:auto"}

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

성공한 응답은 지정된 규칙 구성 요소를 사용하는 규칙 목록을 반환합니다.

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

조회 요청의 경로에 `/extension`을(를) 추가하여 규칙 구성 요소를 제공하는 확장을 조회할 수 있습니다.

**API 형식**

```http
GET /rule_components/{RULE_COMPONENT_ID}/extension
```

| 매개변수 | 설명 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 확장을 조회할 규칙 구성 요소의 `id`입니다. |

{style="table-layout:auto"}

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

성공한 응답은 지정된 규칙 구성 요소의 확장 세부 정보를 반환합니다.

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

조회 요청의 경로에 `/origin`을(를) 추가하여 규칙 구성 요소의 원본(이전 버전)을 조회할 수 있습니다.

**API 형식**

```http
GET /rule_components/{RULE_COMPONENT_ID}/origin
```

| 매개변수 | 설명 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 원본을 조회할 규칙 구성 요소의 `id`입니다. |

{style="table-layout:auto"}

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

성공한 응답은 지정된 규칙 구성 요소의 원본에 대한 세부 정보를 반환합니다.

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
