---
title: 확장 끝점
description: Reactor API에서 /extensions 종단점을 호출하는 방법을 알아봅니다.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 8%

---

# 확장 끝점

Reactor API에서 확장은 [확장 패키지](./extension-packages.md)의 설치된 인스턴스를 나타냅니다. 확장은 확장 패키지에 정의된 기능을 [속성](./properties.md)에 사용할 수 있도록 합니다. 이러한 기능은 [확장](./data-elements.md) 및 [규칙 구성 요소](./rule-components.md)를 만들 때 활용됩니다.

확장은 정확히 하나의 속성에 속합니다. 속성에는 여러 개의 확장이 있을 수 있지만 주어진 확장 패키지의 설치된 인스턴스를 두 개 이하로 포함할 수 없습니다.

## 시작하기

이 안내서에 사용된 끝점은 [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)의 일부입니다. 계속하기 전에 API 인증 방법에 대한 중요한 정보가 필요하면 [시작 안내서](../getting-started.md)를 검토하십시오.

## 확장 목록 검색 {#list}

GET 요청을 만들어 속성에 대한 확장 목록을 검색할 수 있습니다.

**API 형식**

```http
GET properties/{PROPERTY_ID}/extensions
```

| 매개 변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 확장을 나열할 속성의 `id` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 확장을 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`dirty`</li><li>`display_name`</li><li>`enabled`</li><li>`name`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li><li>`version`</li></ul>자세한 내용은 [응답 필터링](../guides/filtering.md)에 대한 안내서를 참조하십시오.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 속성에 정의된 확장 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "EXd9d80c87afb6432ba823a58d3e78299b",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:40:21.000Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:40:21.000Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/property"
          },
          "data": {
            "id": "PRee071cb5b7794f42b74c913e1ad2e325",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/origin"
          },
          "data": {
            "id": "EXd9d80c87afb6432ba823a58d3e78299b",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325",
        "origin": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "self": "https://reactor.adobe.io/extensions/EXd9d80c87afb6432ba823a58d3e78299b",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
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
      "total_count": 1
    }
  }
}
```

## 확장 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 확장을 조회할 수 있습니다.

>[!NOTE]
>
>확장이 삭제되면 시스템에서 삭제된 것으로 플래그가 지정되지만 실제로 제거되지 않습니다. 따라서 삭제된 확장을 검색할 수 있습니다. 삭제된 확장은 반환된 확장 데이터의 `meta`에 `deleted_at` 속성이 있어도 식별할 수 있습니다.

**API 형식**

```http
GET /extensions/{EXTENSION_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `EXTENSION_ID` | 조회할 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 확장의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "EX2ba586f436ac48e390a1ee7e8c9a8f6e",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:40:09.823Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:40:09.823Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/property"
        },
        "data": {
          "id": "PR2254ac6a096c4df38508700093d3e153",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/origin"
        },
        "data": {
          "id": "EX2ba586f436ac48e390a1ee7e8c9a8f6e",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR2254ac6a096c4df38508700093d3e153",
      "origin": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e",
      "self": "https://reactor.adobe.io/extensions/EX2ba586f436ac48e390a1ee7e8c9a8f6e",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## 확장 만들기 또는 업데이트 {#create}

확장은 [확장 패키지](./extension-packages.md)를 참조하여 설치된 확장을 속성에 추가하여 만듭니다. 설치 작업이 완료되면 확장이 성공적으로 설치되었는지 여부를 나타내는 응답이 반환됩니다.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/extensions
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 확장을 설치할 속성의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRee071cb5b7794f42b74c913e1ad2e325/extensions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "example-package::extensionConfiguration::config",
            "enabled": true,
            "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
          },
          "relationships": {
            "extension_package": {
              "data": {
                "id": "EP75db2452065b44e2b8a38ca883ce369a",
                "type": "extension_packages"
              }
            }
          },
          "type": "extensions"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `relationships.extension_package` | **(필수)**  설치 중인 확장 패키지의 ID를 참조하는 개체입니다. |
| `attributes.delegate_descriptor_id` | 확장에는 사용자 지정 설정이 필요한 경우 위임 설명자 ID도 필요합니다. 자세한 내용은 [위임 설명자 ID](../guides/delegate-descriptor-ids.md)의 안내서를 참조하십시오. |
| `attributes.enabled` | 확장이 활성화되어 있는지 여부를 나타내는 부울. |
| `attributes.settings` | 문자열로 표시되는 설정 JSON 개체. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 새로 만든 확장의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "EX8ce7ced633f34bd48d33089ff8fad082",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:32:56.137Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:32:56.137Z",
      "delegate_descriptor_id": "example-package::extensionConfiguration::config",
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property"
        },
        "data": {
          "id": "PRcf1f3e4c218b4caab8191fab003a8355",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin"
        },
        "data": {
          "id": "EX8ce7ced633f34bd48d33089ff8fad082",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
      "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "self": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

## 확장 수정 {#revise}

PATCH 요청 경로에 해당 ID를 포함하여 확장을 수정할 수 있습니다.

**API 형식**

```http
PATCH /extensions/{EXTENSION_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `EXTENSION_ID` | 수정할 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

[확장을 만들 때처럼 수정된 패키지의 로컬 버전을 양식 데이터를 통해 업로드해야 합니다.](#create)

```shell
curl -X POST \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "enabled": false,
          },
          "meta": {
            "action": "revise"
          },
          "id": "EX85509bc7baea4f8599bc44024ed3f110",
          "type": "extensions"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 수정할 속성입니다. 확장의 경우 `delegate_descriptor_id`, `enabled` 및 `settings` 속성을 수정할 수 있습니다. |
| `meta.action` | 개정을 만들 때 `revise` 값에 포함해야 합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적으로 응답하면 `meta.latest_revision_number` 속성이 1만큼 증가하면서 수정된 확장의 세부 사항이 반환됩니다.

```json
{
  "data": {
    "id": "EX8ce7ced633f34bd48d33089ff8fad082",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:32:56.137Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": false,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:32:56.137Z",
      "delegate_descriptor_id": "example-package::extensionConfiguration::config",
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property"
        },
        "data": {
          "id": "PRcf1f3e4c218b4caab8191fab003a8355",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin"
        },
        "data": {
          "id": "EX8ce7ced633f34bd48d33089ff8fad082",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcf1f3e4c218b4caab8191fab003a8355",
      "origin": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "self": "https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 2
    }
  }
}
```

## 확장 삭제 {#private-release}

DELETE 요청 경로에 해당 ID를 포함하여 확장을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /extensions/{EXTENSION_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `EXTENSION_ID` | 삭제할 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적으로 응답하면 응답 본문이 없는 HTTP 상태 204(컨텐츠 없음)를 반환하여 확장이 삭제되었음을 나타냅니다.

## 확장 참고 사항 관리 {#notes}

확장은 &quot;주목할 만한&quot; 리소스입니다. 즉, 각 개별 리소스에서 텍스트 기반 메모를 만들고 검색할 수 있습니다. 확장 및 기타 호환 리소스에 대한 메모를 관리하는 방법에 대한 자세한 내용은 [참고 엔드포인트 안내서](./notes.md)를 참조하십시오.

## 확장에 대한 관련 리소스 검색 {#related}

다음 호출에서는 확장에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. [확장을 찾을 때 ](#lookup) 속성 아래에 이러한 관계가 나열됩니다.`relationships`

Reactor API의 관계에 대한 자세한 내용은 [관계 안내서](../guides/relationships.md)를 참조하십시오.

### 확장에 대한 관련 라이브러리 나열 {#libraries}

조회 요청의 경로에 `/libraries`을 추가하여 확장을 활용하는 라이브러리를 나열할 수 있습니다.

**API 형식**

```http
GET  /extensions/{EXTENSION_ID}/libraries
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXTENSION_ID}` | 라이브러리를 나열할 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/libraries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 확장을 사용하는 라이브러리 목록을 반환합니다.

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

### 확장의 관련 개정 버전 나열 {#revisions}

조회 요청의 경로에 `/revisions`을 추가하여 확장의 이전 버전을 나열할 수 있습니다.

**API 형식**

```http
GET  /extensions/{EXTENSION_ID}/revisions
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXTENSION_ID}` | 개정을 나열할 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/revisions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 확장의 수정 버전 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "EXbfcca9f3ce9d40318b9115159a951e09",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:41:09.023Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:41:09.023Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/property"
          },
          "data": {
            "id": "PR92de152ae31e48a692142ea65c1efeb9",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/origin"
          },
          "data": {
            "id": "EXd485e07fb3d3429b997768ae40de8f02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR92de152ae31e48a692142ea65c1efeb9",
        "origin": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
        "self": "https://reactor.adobe.io/extensions/EXbfcca9f3ce9d40318b9115159a951e09",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
      },
      "meta": {
        "latest_revision_number": 1
      }
    },
    {
      "id": "EXd485e07fb3d3429b997768ae40de8f02",
      "type": "extensions",
      "attributes": {
        "created_at": "2020-12-14T17:41:09.002Z",
        "deleted_at": null,
        "dirty": false,
        "enabled": true,
        "name": "kessel-test",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:41:09.002Z",
        "delegate_descriptor_id": null,
        "display_name": "Kessel Test",
        "review_status": "unsubmitted",
        "version": "1.2.0",
        "settings": "{}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/property"
          },
          "data": {
            "id": "PR92de152ae31e48a692142ea65c1efeb9",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/origin"
          },
          "data": {
            "id": "EXd485e07fb3d3429b997768ae40de8f02",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02/extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR92de152ae31e48a692142ea65c1efeb9",
        "origin": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
        "self": "https://reactor.adobe.io/extensions/EXd485e07fb3d3429b997768ae40de8f02",
        "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
        "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
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

### 확장에 대한 관련 확장 패키지 조회 {#extension}

GET 요청 경로에 `/extension_package`을 추가하여 확장이 기반으로 하는 확장 패키지를 찾을 수 있습니다.

**API 형식**

```http
GET  /extensions/{EXTENSION_ID}/extension_package
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXTENSION_ID}` | 확장을 조회하려는 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 확장의 기반이 되는 확장 패키지의 세부 정보를 반환합니다. 아래 예제 응답은 스페이스에 대해 잘렸습니다.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

### 확장의 관련 원본 조회 {#origin}

GET 요청의 경로에 `/origin`을 추가하여 확장의 출처를 조회할 수 있습니다. 확장의 원본은 현재 개정을 만들기 위해 업데이트된 이전 개정입니다.

**API 형식**

```http
GET  /extensions/{EXTENSION_ID}/origin
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXTENSION_ID}` | 원본을 조회하려는 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 확장의 원본 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "EX524f2cd22ae4490eaf73cc9214eb217d",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:41:21.397Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:41:21.397Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/property"
        },
        "data": {
          "id": "PR88d6b8ee423b44a49de1dee26391e25b",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/origin"
        },
        "data": {
          "id": "EX524f2cd22ae4490eaf73cc9214eb217d",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR88d6b8ee423b44a49de1dee26391e25b",
      "origin": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d",
      "self": "https://reactor.adobe.io/extensions/EX524f2cd22ae4490eaf73cc9214eb217d",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 확장의 관련 속성 조회 {#property}

GET 요청 경로에 `/property`을 추가하여 확장을 소유하는 속성을 찾을 수 있습니다.

**API 형식**

```http
GET  /extensions/{EXTENSION_ID}/property
```

| 매개 변수 | 설명 |
| --- | --- |
| `{EXTENSION_ID}` | 속성을 조회하려는 확장의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extensions/EX8ce7ced633f34bd48d33089ff8fad082/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 확장을 소유하는 속성의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "PR96fd3675be144ddc8c4540d79430355a",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:53:06.993Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:53:06.993Z",
      "platform": "web",
      "development": false,
      "token": "bf75a40b3c34",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/environments",
      "extensions": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/extensions",
      "rules": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a/rules",
      "self": "https://reactor.adobe.io/properties/PR96fd3675be144ddc8c4540d79430355a"
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
